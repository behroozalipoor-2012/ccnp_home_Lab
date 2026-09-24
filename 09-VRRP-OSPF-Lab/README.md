# VRRP with OSPF Lab

## Objective

The purpose of this lab is to configure and verify VRRP (Virtual Router Redundancy Protocol) in an OSPF-based network.

VRRP provides first-hop gateway redundancy by allowing multiple Layer 3 switches to share a virtual default gateway.

## Technologies Used

- VRRP
- OSPF
- Layer 3 Switching
- VLANs
- SVIs
- First Hop Redundancy
- Gateway Redundancy
- Traceroute
- ICMP/Ping

## VLANs and VRRP Groups

| VLAN | VRRP Group | Virtual IP |
|------|------------|------------|
| VLAN 100 | 100 | 10.10.100.1 |
| VLAN 200 | 200 | 10.10.200.1 |

## Distribution Switch Addresses

### DSW1

- VLAN 100: 10.10.100.10
- VLAN 200: 10.10.200.10

### DSW2

- VLAN 100: 10.10.100.20
- VLAN 200: 10.10.200.20

## VRRP Configuration

Example configuration:

### DSW1

```cisco
interface vlan 100
 vrrp 100 ip 10.10.100.1
 vrrp 100 priority 120

interface vlan 200
 vrrp 200 ip 10.10.200.1
 vrrp 200 priority 90
