
# Layer 3 Switching with EIGRP

## Objective
This lab explores Layer 3 switching using Switch Virtual Interfaces (SVIs), IP routing, and EIGRP.

## Configuration Overview

### P1ASW1
- VLAN 1 IP: 172.16.1.10/24
- Default Gateway: 172.16.1.100

### P2ASW2
- VLAN 1 IP: 172.16.1.20/24
- Default Gateway: 172.16.1.200

### P1DSW1
- VLAN 1: 172.16.1.100/24
- VLAN 11: 172.16.11.100/24
- IP routing enabled
- EIGRP AS 100 enabled

### P2DSW2
- VLAN 1: 172.16.1.200/24
- VLAN 12: 172.16.12.200/24
- IP routing enabled
- EIGRP AS 100 enabled

## Layer 3 Switching

Layer 3 switching allows a multilayer switch to perform both switching and routing.

IP routing was enabled with:

```cisco
ip routing
