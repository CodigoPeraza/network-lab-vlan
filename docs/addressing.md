# Direccionamiento IP

## Subredes

| VLAN | Nombre | Subred | Máscara | Gateway |
| --- | --- | --- | --- | --- |
| 10 | ADMINISTRACION | 10.10.10.0/24 | 255.255.255.0 | 10.10.10.1 |
| 20 | USUARIOS | 10.20.20.0/24 | 255.255.255.0 | 10.20.20.1 |
| 30 | SERVIDORES | 10.30.30.0/24 | 255.255.255.0 | 10.30.30.1 |
| 99 | GESTION | 10.99.99.0/24 | 255.255.255.0 | 10.99.99.1 |

## Asignaciones estáticas

| Dispositivo | Interfaz | IP | Máscara | Gateway |
| --- | --- | --- | --- | --- |
| `R1` | `Gig0/0.10` | 10.10.10.1 | 255.255.255.0 | N/A |
| `R1` | `Gig0/0.20` | 10.20.20.1 | 255.255.255.0 | N/A |
| `R1` | `Gig0/0.30` | 10.30.30.1 | 255.255.255.0 | N/A |
| `R1` | `Gig0/0.99` | 10.99.99.1 | 255.255.255.0 | N/A |
| `SW1` | `Vlan99` | 10.99.99.11 | 255.255.255.0 | 10.99.99.1 |
| `SW2` | `Vlan99` | 10.99.99.12 | 255.255.255.0 | 10.99.99.1 |
| `SRV1` | `FastEthernet0` | 10.30.30.11 | 255.255.255.0 | 10.30.30.1 |
| `SRV2` | `FastEthernet0` | 10.30.30.12 | 255.255.255.0 | 10.30.30.1 |
| `SRV3` | `FastEthernet0` | 10.30.30.13 | 255.255.255.0 | 10.30.30.1 |

## DHCP

Los clientes de VLAN 10 y VLAN 20 obtienen IP por DHCP. Los servidores y los switches usan direccionamiento estático.

| Pool | Red | Rango útil | Exclusiones | DNS |
| --- | --- | --- | --- | --- |
| `VLAN10` | 10.10.10.0/24 | 10.10.10.100 a 10.10.10.150 | 10.10.10.1 a 10.10.10.20 | 10.30.30.11 |
| `VLAN20` | 10.20.20.0/24 | 10.20.20.100 a 10.20.20.150 | 10.20.20.1 a 10.20.20.20 | 10.30.30.11 |
| `VLAN30` | 10.30.30.0/24 | 10.30.30.100 a 10.30.30.150 | 10.30.30.1 a 10.30.30.20 | 10.30.30.11 |

El rango de exclusión evita conflictos con gateways, servidores y direcciones reservadas.
