# Lab 17 – Multi-Area OSPF & Route Summarization

## Overview

This lab demonstrates the configuration and verification of Multi-Area OSPF and OSPF route summarization.

The topology uses multiple OSPF areas and routers to demonstrate how OSPF exchanges routes between areas and how route summarization reduces the number of routes advertised.

## Technologies

- Cisco IOS
- OSPFv2
- Multi-Area OSPF
- OSPF Area 0
- OSPF Area 1
- OSPF Area 2
- OSPF Route Summarization
- Loopback Interfaces
- Serial Interfaces
- FastEthernet Interfaces
- OSPF Neighbor Adjacencies

## OSPF Configuration

OSPF was configured using multiple areas.

Example:

```text

router ospf 1
 network 10.100.100.0 0.0.0.255 area 0
 network 192.168.1.0 0.0.0.255 area 1


## Route Summarization

router ospf 1
 area 1 range 192.168.1.0 255.255.255.192

router ospf 1
 area 2 range 192.168.2.0 255.255.255.192


## Verification Commands
show ip route
show ip ospf
show ip ospf neighbor
show ip ospf interface
show ip ospf database
ping

# Routing Table
O
O IA

## Route Summarization
192.168.1.0/26
192.168.2.0/26
