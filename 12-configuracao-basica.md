# Configuração Básica do Mikrotik

1. **Definir IP e Gateway:**
```shell
/ip address add address=192.168.10.1/24 interface=ether1
/ip route add gateway=192.168.10.254
/ip dhcp-server setup
