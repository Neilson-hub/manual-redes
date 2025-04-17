## 🌐 Topologia de Rede: Mikrotik RB4011 + UniFi Wi-Fi 6

A imagem abaixo mostra a topologia de conexão entre o roteador Mikrotik RB4011 e um Access Point UniFi Wi-Fi 6, com uso de VLANs para separar a rede corporativa e a rede de clientes.

- **VLAN99**: Rede Corporativa
- **VLAN20**: Rede de Clientes

![Topologia VLAN Mikrotik com UniFi](https://github.com/Neilson-hub/manual-redes/blob/main/mk-01.png)

> As VLANs são entregues via trunk até o UniFi, que distribui SSIDs com base nessas VLANs.
