# Topología del laboratorio

## Dispositivos

| Dispositivo | Modelo | Rol |
| --- | --- | --- |
| `R1` | Cisco 2911 | Router-on-a-stick e inter-VLAN routing |
| `SW1` | Cisco 2960-24TT | Switch principal |
| `SW2` | Cisco 2960-24TT | Switch secundario |
| `PC-A1`, `PC-A2`, `PC-A3` | PC genérico | Clientes VLAN 10 |
| `PC-U1`, `PC-U2`, `PC-U3` | PC genérico | Clientes VLAN 20 |
| `SRV1`, `SRV2`, `SRV3` | Servidor genérico | Servidores VLAN 30 |

## Conexiones

| Origen | Puerto | Destino | Puerto | Tipo |
| --- | --- | --- | --- | --- |
| `R1` | `Gig0/0` | `SW1` | `Gig0/1` | Trunk 802.1Q |
| `SW1` | `Fa0/24` | `SW2` | `Fa0/24` | Trunk 802.1Q |
| `SW1` | `Fa0/1` | `PC-A1` | `FastEthernet0` | Access VLAN 10 |
| `SW1` | `Fa0/2` | `PC-A2` | `FastEthernet0` | Access VLAN 10 |
| `SW1` | `Fa0/3` | `PC-U1` | `FastEthernet0` | Access VLAN 20 |
| `SW1` | `Fa0/4` | `PC-U2` | `FastEthernet0` | Access VLAN 20 |
| `SW1` | `Fa0/5` | `SRV1` | `FastEthernet0` | Access VLAN 30 |
| `SW1` | `Fa0/6` | `SRV2` | `FastEthernet0` | Access VLAN 30 |
| `SW2` | `Fa0/1` | `PC-A3` | `FastEthernet0` | Access VLAN 10 |
| `SW2` | `Fa0/2` | `PC-U3` | `FastEthernet0` | Access VLAN 20 |
| `SW2` | `Fa0/3` | `SRV3` | `FastEthernet0` | Access VLAN 30 |

## Enlaces troncales

- `R1 G0/0` transporta las VLANs 10, 20, 30 y 99 hacia `SW1`.
- `SW1 Fa0/24` transporta las mismas VLANs hacia `SW2`.
- La VLAN nativa es la VLAN 1 por defecto; no se transportan otras VLANs fuera de la lista permitida.

## Puertos de acceso

Los puertos de acceso se configuran con `switchport mode access`, `switchport access vlan`, `spanning-tree portfast` y se deshabilita la negociación DTP.

## VLAN de gestión

La VLAN 99 se usa únicamente para administración. `SW1` y `SW2` tienen una SVI en `10.99.99.0/24`; el router tiene la subinterfaz `Gig0/0.99` como gateway.
