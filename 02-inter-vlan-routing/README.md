# Inter-VLAN Routing & Layer 3 Interfaces Lab

## Objective

Configure and verify Layer 3 connectivity using:

- VLANs and SVIs
- Inter-VLAN routing
- Routed switch ports
- /26 VLAN subnets
- /30 point-to-point links
- CDP neighbor discovery
- Ping connectivity testing

> OSPF configuration is intentionally excluded from this lab documentation.

---

## VLANs

VLANs used:

```text
VLAN 421
VLAN 422
VLAN 423
VLAN 424
```

Verify VLANs:

```cisco
show vlan brief
```

---

## DSW2 SVI Configuration

```cisco
configure terminal

interface vlan 421
 ip address 10.40.12.3 255.255.255.192

interface vlan 422
 ip address 10.40.12.67 255.255.255.192

interface vlan 423
 ip address 10.40.12.131 255.255.255.192

interface vlan 424
 ip address 10.40.12.195 255.255.255.192

end
```

Verify:

```cisco
show ip interface brief
```

---

## Routed Ports

Layer 3 switch ports were created using:

```cisco
configure terminal
interface gigabitEthernet 1/0/13
 no switchport
 ip address <IP-ADDRESS> 255.255.255.252
 no shutdown
end
```

The `no switchport` command converts the physical switch interface from a Layer 2 switchport into a Layer 3 routed interface.

### DSW1

```cisco
interface gigabitEthernet 1/0/13
 no switchport
 ip address 10.40.23.2 255.255.255.252

interface gigabitEthernet 1/0/14
 no switchport
 ip address 10.40.23.6 255.255.255.252
```

### DSW2

```cisco
interface gigabitEthernet 1/0/13
 no switchport
 ip address 10.40.23.10 255.255.255.252

interface gigabitEthernet 1/0/14
 no switchport
 ip address 10.40.23.14 255.255.255.252
```

---

## Router Interfaces

### R1

```cisco
configure terminal

interface gigabitEthernet 0/0
 ip address 10.40.23.1 255.255.255.252
 no shutdown

interface gigabitEthernet 0/1
 ip address 10.40.23.9 255.255.255.252
 no shutdown

end
```

### R2

```cisco
configure terminal

interface gigabitEthernet 0/0
 ip address 10.40.23.5 255.255.255.252
 no shutdown

interface gigabitEthernet 0/1
 ip address 10.40.23.13 255.255.255.252
 no shutdown

end
```

---

## CDP Neighbor Discovery

Used CDP to identify directly connected Cisco devices and interfaces.

```cisco
show cdp neighbors
```

---

## Verification Commands

```cisco
show vlan brief
show ip interface brief
show cdp neighbors
```

Connectivity was tested using:

```cisco
ping 10.40.12.2
ping 10.40.12.66
ping 10.40.12.130
ping 10.40.12.194
```

Point-to-point routed links were also tested with ping.

Successful output:

```text
Success rate is 100 percent (5/5)
```

---

## Skills Practiced

- Creating and verifying VLANs
- Configuring SVIs
- Inter-VLAN routing
- IPv4 subnetting
- Configuring /26 networks
- Configuring /30 point-to-point networks
- Converting Layer 2 switchports to Layer 3 routed ports
- Configuring router interfaces
- Using CDP for neighbor discovery
- Verifying interfaces
- Troubleshooting connectivity with ICMP ping
