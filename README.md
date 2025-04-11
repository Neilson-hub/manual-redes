# Manual-redes


manual-mikrotik-rede

# Manual Completo - Configuração Mikrotik Rede LAN de Alto Desempenho e Baixo Custo

Este manual detalha a implementação prática de uma rede LAN utilizando equipamentos Mikrotik para 48 hosts cabeados e 20 dispositivos Wi-Fi, priorizando alto desempenho, segurança e economia.

## Sumário

- [Introdução](introducao.md)
- [Topologia da Rede](topologia.md)
- [Configuração Básica do Mikrotik](configuracao-basica.md)
- [Configuração de VLANs](vlan.md)
- [Regras de Firewall e Segurança](firewall.md)
- [Configuração Wi-Fi](wifi.md)
- [Monitoramento e Avaliação](monitoramento.md)
- [Segurança Física](seguranca-fisica.md)
- [Referências Técnicas](referencias.md)


# Configuração Básica do Mikrotik

1. **Definir IP e Gateway:**
```shell
/ip address add address=192.168.10.1/24 interface=ether1
/ip route add gateway=192.168.10.254
/ip dhcp-server setup



**vlan.md**
```markdown
# Configuração de VLANs

Exemplo prático para criar VLAN 10 para rede administrativa:

```shell
/interface vlan add name=vlan10 vlan-id=10 interface=ether2
/ip address add address=192.168.20.1/24 interface=vlan10



### 🔗 Referências:
Sempre utilize links diretos para documentação oficial Mikrotik:

- [Manual completo RouterOS - Mikrotik](https://help.mikrotik.com/docs/display/ROS/)
- [Configurações avançadas Firewall RouterOS](https://help.mikrotik.com/docs/display/ROS/Firewall)
- [Configuração de Wireless](https://help.mikrotik.com/docs/display/ROS/Wireless)

---

## 🚀 Como publicar no GitHub:

1. **Crie uma conta no GitHub:**  
[GitHub - Sign Up](https://github.com/signup)

2. **Crie um novo repositório:**  
- Clique em "New repository".  
- Dê um nome claro (ex.: `manual-mikrotik-rede`).  
- Escolha "Public" para disponibilizar a todos.

3. **Suba seus arquivos:**
- Clone o repositório no seu computador usando Git:
```shell
git clone https://github.com/seu-usuario/manual-mikrotik-rede.git



## 🚀 Como publicar no GitHub:

1. **Crie uma conta no GitHub:**  
[GitHub - Sign Up](https://github.com/signup)

2. **Crie um novo repositório:**  
- Clique em "New repository".  
- Dê um nome claro (ex.: `manual-mikrotik-rede`).  
- Escolha "Public" para disponibilizar a todos.

3. **Suba seus arquivos:**
- Clone o repositório no seu computador usando Git:
```shell
git clone https://github.com/seu-usuario/manual-mikrotik-rede.git


### 🔗 Referências:
Sempre utilize links diretos para documentação oficial Mikrotik:

- [Manual completo RouterOS - Mikrotik](https://help.mikrotik.com/docs/display/ROS/)
- [Configurações avançadas Firewall RouterOS](https://help.mikrotik.com/docs/display/ROS/Firewall)
- [Configuração de Wireless](https://help.mikrotik.com/docs/display/ROS/Wireless)

---