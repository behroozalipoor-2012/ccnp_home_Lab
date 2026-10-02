# Multi-Area OSPF with Layer 3 Switching

## Objective

This lab demonstrates the implementation of a multi-area OSPF network using routers and Layer 3 switches.

The network uses OSPF Area 0 as the backbone and Areas 1, 2, 3, and 4 for distribution networks.

## Technologies Used

- OSPFv2
- Multi-Area OSPF
- OSPF Area 0 Backbone
- Area Border Routers (ABRs)
- Layer 3 Switching
- IP Routing
- Switched Virtual Interfaces (SVIs)
- VLAN Routing
- OSPF Passive Interfaces
- OSPF DR/BDR Election
- /30 Point-to-Point Networks
- /26 VLAN Subnets
- OSPF Neighbor Adjacencies
- OSPF Link-State Database

## OSPF Design

### Backbone - Area 0

BBR1 provides the OSPF backbone connectivity to the core routers.

Core routers connect Area 0 to their respective OSPF areas:

- CoreR1: Area 0 ↔ Area 1
- CoreR2: Area 0 ↔ Area 2
- CoreR3: Area 0 ↔ Area 3
- CoreR4: Area 0 ↔ Area 4

The core routers operate as Area Border Routers (ABRs).

## Layer 3 Distribution Switches

Four Layer 3 switches provide routing for their local VLAN networks:

- DSW1 - Area 1
- DSW2 - Area 2
- DSW3 - Area 3
- DSW4 - Area 4

IP routing was enabled on the multilayer switches using:

ip routing

SVIs were configured to provide Layer 3 gateways for the VLAN networks.

## VLAN Addressing

Each distribution switch contains multiple /26 VLAN networks.

Example:

DSW1:
- VLAN 11 - 12.1.1.0/26
- VLAN 12 - 12.1.1.64/26
- VLAN 13 - 12.1.1.128/26
- VLAN 14 - 12.1.1.192/26

DSW2:
- VLAN 21 - 12.2.1.0/26
- VLAN 22 - 12.2.1.64/26
- VLAN 23 - 12.2.1.128/26
- VLAN 24 - 12.2.1.192/26

DSW3:
- VLAN 31 - 12.3.1.0/26
- VLAN 32 - 12.3.1.64/26
- VLAN 33 - 12.3.1.128/26
- VLAN 34 - 12.3.1.192/26

DSW4:
- VLAN 41 - 12.4.1.0/26
- VLAN 42 - 12.4.1.64/26
- VLAN 43 - 12.4.1.128/26
- VLAN 44 - 12.4.1.192/26

## Passive Interfaces

VLAN interfaces were configured as OSPF passive interfaces.

Example:

router ospf 1
 passive-interface vlan 21
 passive-interface vlan 22
 passive-interface vlan 23
 passive-interface vlan 24

This allows the VLAN networks to be advertised into OSPF without sending OSPF Hello packets toward end-user networks.

## Verification

The following commands were used to verify OSPF operation:

show ip ospf interface
show ip ospf interface brief
show ip ospf database
debug ip ospf hello
ping

Verification confirmed:

- OSPF neighbor adjacencies
- Area assignments
- DR/BDR operation
- OSPF LSDB population
- Inter-area route propagation
- Layer 3 VLAN advertisement
- End-to-end IP connectivity

## Key Concepts Practiced

This lab provided hands-on experience with:

- Designing a hierarchical OSPF topology
- Configuring OSPF Area 0
- Connecting multiple non-backbone areas
- Configuring ABRs
- Integrating Layer 3 switches with OSPF
- Configuring SVIs
- Advertising VLAN networks through OSPF
- Configuring passive interfaces
- Verifying OSPF neighbor relationships
- Examining the OSPF link-state database
- Troubleshooting OSPF configuration

## Result

The multi-area OSPF topology was successfully configured with Area 0 providing backbone connectivity between Areas 1, 2, 3, and 4.

Layer 3 distribution switches advertise their VLAN networks into OSPF, allowing routing information to propagate throughout the multi-area topology.
