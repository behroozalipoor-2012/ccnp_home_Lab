# Layer 3 EtherChannel with EIGRP

## Overview

This lab demonstrates the configuration and verification of a Layer 3 EtherChannel between Cisco multilayer switches.

Two physical FastEthernet interfaces are bundled into a single routed Port-Channel. EIGRP is used to exchange routing information across the Layer 3 EtherChannel.

## Technologies Used

- Cisco IOS
- Layer 3 EtherChannel
- Routed Ports
- Port-Channel
- EIGRP
- IPv4 Routing
- EtherChannel Load Balancing
- Connectivity Testing

## Layer 3 EtherChannel Configuration

Physical interfaces Fa0/5 and Fa0/6 were converted from Layer 2 switchports to Layer 3 routed interfaces and bundled into Port-Channel 1.

```cisco
interface range FastEthernet0/5 - 6
 no switchport
 channel-group 1 mode on
 no shutdown
```

The logical Port-Channel interface was also configured as a routed interface.

```cisco
interface Port-channel1
 no switchport
 ip address 172.16.1.1 255.255.255.252
 no shutdown
```

## Enable Layer 3 Routing

```cisco
ip routing
```

## EIGRP Configuration

EIGRP AS 100 was configured to advertise the 172.16.0.0 network.

```cisco
router eigrp 100
 network 172.16.0.0
```

An EIGRP neighbor relationship was successfully established across Port-Channel1.

## EtherChannel Verification

```cisco
show etherchannel summary
show interfaces port-channel 1
show ip route
```

The EtherChannel summary displayed:

```text
Po1(RU)   Fa0/5(P)   Fa0/6(P)
```

Where:

- **R** = Layer 3 Port-Channel
- **U** = Port-Channel in use
- **P** = Physical interface successfully bundled in the Port-Channel

## Load Balancing

The EtherChannel load-balancing algorithm was changed to use source and destination IP addresses.

```cisco
port-channel load-balance src-dst-ip
```

Verification:

```cisco
show etherchannel load-balance
```

## Routing Verification

The routing table confirmed that the remote network was learned dynamically through EIGRP over Port-Channel1.

Example:

```text
D 172.16.12.0/24 via 172.16.1.2, Port-channel1
```

## Connectivity Testing

End-to-end ping tests were performed between networks. Initial unsuccessful tests were used during troubleshooting, followed by successful connectivity after the Layer 3 EtherChannel and routing configuration were completed.

## Skills Demonstrated

- Configuring routed physical interfaces
- Building a static Layer 3 EtherChannel
- Configuring Layer 3 Port-Channels
- Enabling IP routing on multilayer switches
- Configuring EIGRP
- Verifying EIGRP-learned routes
- Configuring EtherChannel load balancing
- Verifying EtherChannel member interfaces
- Testing and troubleshooting end-to-end connectivity

## Lab Screenshots

Screenshots in this directory document the configuration, verification, routing table, EtherChannel status, load-balancing configuration, and connectivity testing.
