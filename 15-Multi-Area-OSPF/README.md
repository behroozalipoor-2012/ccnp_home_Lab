# Multi-Area OSPF Lab

## Objective

The objective of this lab was to configure and verify a multi-area OSPF network using Cisco routers.

The network was divided into multiple OSPF areas to demonstrate hierarchical OSPF design, neighbor relationships, inter-area routing, ABR functionality, and OSPF Link-State Database operation.

## OSPF Areas

- Area 0 - Backbone Area
- Area 1
- Area 2

Router1 operates as the Area Border Router (ABR), connecting the backbone area to Areas 1 and 2.

## Configuration Tasks

- Configured IPv4 addressing on router interfaces
- Enabled OSPF process 1
- Manually configured OSPF Router IDs
- Configured Area 0 as the backbone
- Configured Area 1 and Area 2
- Established OSPF neighbor adjacencies
- Configured loopback interfaces
- Verified OSPF routing tables
- Examined the OSPF Link-State Database
- Verified inter-area routes
- Examined OSPF LSAs
- Verified end-to-end connectivity using ICMP ping

## Important Verification Commands

```text
show ip interface brief
show ip ospf
show ip ospf neighbor
show ip ospf database
show ip ospf database router
show ip ospf interface brief
show ip route
ping <destination-ip>
