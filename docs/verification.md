# Verificación del laboratorio

## Comandos en switches

```text
show vlan brief
show interfaces trunk
show interfaces status
show ip interface brief
show mac address-table
```

Resultados esperados:

- `VLAN10`, `VLAN20`, `VLAN30` y `VLAN99` aparecen en `show vlan brief`.
- Los puertos de acceso muestran su VLAN asignada.
- `Fa0/24` y `Gig0/1` aparecen como trunks en `show interfaces trunk`.
- La SVI de VLAN 99 está en estado `up/up`.
- `SW1` y `SW2` responden ping a `10.99.99.1`.

## Comandos en el router

```text
show ip interface brief
show ip route
show ip dhcp binding
show ip dhcp pool
show access-lists
```

Resultados esperados:

- Las subinterfaces `Gig0/0.10`, `Gig0/0.20`, `Gig0/0.30` y `Gig0/0.99` están en estado `up/up`.
- `show ip route` contiene rutas conectadas para `10.10.10.0/24`, `10.20.20.0/24`, `10.30.30.0/24` y `10.99.99.0/24`.
- Los clientes DHCP aparecen en `show ip dhcp binding`.
- La ACL `USERS_TO_SERVERS` muestra contadores cuando los usuarios acceden a servicios permitidos.

## Pruebas de conectividad

Desde un cliente de VLAN 10:

```text
ping 10.10.10.1
ping 10.30.30.11
ping 10.99.99.11
```

Desde un cliente de VLAN 20:

```text
ping 10.20.20.1
ping 10.30.30.11
ping 10.99.99.11
```

Desde un servidor de VLAN 30:

```text
ping 10.10.10.1
ping 10.20.20.1
ping 10.99.99.1
```

## Comportamiento esperado de la ACL

- Los clientes de VLAN 20 pueden acceder a `SRV1`, `SRV2` y `SRV3` por HTTP, HTTPS y DNS.
- Los clientes de VLAN 20 no pueden acceder a la subred de VLAN 10.
- La VLAN 10 puede acceder a servidores y a la VLAN de gestión.
- La VLAN 99 puede administrar los switches y enrutar hacia otras VLANs.

## Capturas recomendadas

- `show vlan brief` en `SW1`.
- `show interfaces trunk` en `SW1` y `SW2`.
- `show ip interface brief` en `R1`.
- Ping exitoso entre VLAN 20 y VLAN 30.
- Ping bloqueado entre VLAN 20 y VLAN 10 por la ACL.
