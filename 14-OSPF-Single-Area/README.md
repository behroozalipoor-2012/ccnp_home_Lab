# OSPF Single-Area Lab

## Objective
Configure and verify OSPFv2 in a single-area network using Area 0.

## Lab Overview
In this lab, I configured OSPF process ID 10 across multiple routers and placed the participating networks in OSPF Area 0.

The lab demonstrates:
- OSPF single-area configuration
- OSPF neighbor adjacency formation
- OSPF route learning
- Router ID selection
- OSPF DR/BDR behavior on broadcast networks
- OSPF point-to-point operation
- OSPF Link-State Database verification
- OSPF interface verification

## Configuration Example

```cisco
router ospf 10
 network 192.168.1.0 0.0.0.255 area 0
 network 10.100.100.0 0.0.0.255 area 0
show ip route
show ip protocols
show ip ospf
show ip ospf neighbor
show ip ospf database
show ip ospf interface
