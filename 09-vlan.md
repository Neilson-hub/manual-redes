**vlan.md**
```markdown
# Configuração de VLANs

Exemplo prático para criar VLAN 10 para rede administrativa:

```shell
/interface vlan add name=vlan10 vlan-id=10 interface=ether2
/ip address add address=192.168.20.1/24 interface=vlan10
