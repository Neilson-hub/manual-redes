# Script de Failover para Mikrotik

Este script realiza failover automático para múltiplos links configurados nas interfaces `ether1`, `ether2` e `ether3` do Mikrotik.

## Instruções Iniciais

Antes de executar o script:
- Defina comentários nas rotas default identificando claramente cada link.
  - Exemplo: `Link1`, `Link2`, `Link-Vivo`, `Link-OI`

---

## Script para Configuração Inicial

Este script remove regras e scripts antigos e cria rotas de teste:

```shell
/ip route remove [find comment~"!==="]
/routing rule remove [find comment~"!==="]
/system script remove [find name=FAILOVER]
/system scheduler remove [find name="EXECUTA SCRIPT DE FAILOVER"]
/ip/vrf remove [find comment~"!==="]

:foreach i in=[/ip route find dst-address=0.0.0.0/0 routing-table<>""] do={
  :global gateway [/ip route get number=$i gateway]
  :global comentario [/ip route get number=$i comment]

  /ip/vrf/add interfaces=none name=("TEST-" . $comentario) comment="!=== VRF PARA TESTE"
  :delay 2
  /ip route add gateway=$gateway routing-table=("TEST-" . $comentario) comment=("!=== ROTA DE TESTE " . $comentario)
  /routing rule add action=lookup-only-in-table comment="!=== FORCE TESTE DE FAILOVER ==> $comentario" disabled=no routing-mark=("TEST-" . $comentario) table=("TEST-" . $comentario)
}
```

---

## Script para Execução Automática do Failover

Este script verifica periodicamente (a cada 30 segundos) a conectividade dos links e ativa ou desativa as rotas conforme o resultado dos testes:

```shell
/system scheduler
add interval=30s name="EXECUTA SCRIPT DE FAILOVER" on-event=FAILOVER policy=\
    ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon \
    start-time=startup

/system script
add dont-require-permissions=no name=FAILOVER owner=admin policy=\
ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon source="

# IPs para teste separados por vírgula (não usar nomes, pois se todas as rotas falharem, não resolverá DNS)
:global IPsParaTeste \"8.8.8.8,8.8.4.4,200.160.0.8,31.13.80.8\"
:global NumeroDePings 3
:global Intervalo 00:00:00.5

# Converte strings em arrays
:global IPsParaTeste [:toarray $IPsParaTeste];

# Seleciona as tabelas de roteamento para teste
:foreach i in=[/ip route find dst-address=0.0.0.0/0 routing-table=\"main\"] do={

  /ping 127.0.0.1 count=1
  :delay 1
  :global LinkState 0
  :global comentario [/ip route get number=$i comment]
  :global TabRoteAtual (\"TEST-\" . $comentario)

  :foreach IPAtualParaTeste in=$IPsParaTeste do={
    :global LinkState ($LinkState + [ping address=$IPAtualParaTeste vrf=$TabRoteAtual interval=$Intervalo count=$NumeroDePings])
  }

  # Ativa ou desativa as rotas conforme resultado dos testes
  if ($LinkState=0) do={
    if ([/ip route print count-only where comment=$comentario disabled]=0) do={
      /ip route disable [find comment=$comentario]
    }
  }

  if ($LinkState>0) do={
    if ([/ip route print count-only where comment=$comentario disabled]>0) do={
      /ip route enable [find comment=$comentario]
    }
  }
}
"
```

---

## Interfaces Utilizadas

Configure este script nas seguintes interfaces do Mikrotik:

- Interface 1 (`ether1`)
- Interface 2 (`ether2`)
- Interface 3 (`ether3`)