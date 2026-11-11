
# Lab 21 - EIGRP Route Summarization

## Overview
This CCNP Enterprise lab demonstrates EIGRP configuration, neighbor adjacency, route learning, topology verification, and manual route summarization across two interconnected routing pods.

## Lab Objectives
- Configure EIGRP autonomous system 200.
- Establish EIGRP neighbor adjacencies.
- Verify EIGRP routing and topology tables.
- Configure manual EIGRP route summarization.
- Verify summarized routes and Null0 summary entries.
- Test end-to-end connectivity between pods.

## Network Topology
The lab contains six routers organized into two pods.

Pod 1: P1R1, P1R2, P1R3  
Pod 2: P2R1, P2R2, P2R3

Backbone: 10.100.100.0/24  
Pod 1 summary: 192.168.1.0/26  
Pod 2 summary: 192.168.2.0/26  
EIGRP AS: 200

## EIGRP Configuration

Example configuration on P1R1:

```cisco
router eigrp 200
 network 10.0.0.0
 network 192.168.1.0
```

Example configuration on P2R1:

```cisco
router eigrp 200
 network 10.0.0.0
 network 192.168.2.0
```

## Manual Route Summarization

On P1R1, advertise the Pod 1 summary toward the backbone:

```cisco
interface FastEthernet0/0
 ip summary-address eigrp 200 192.168.1.0 255.255.255.192
```

On P2R1, advertise the Pod 2 summary toward the backbone:

```cisco
interface FastEthernet0/0
 ip summary-address eigrp 200 192.168.2.0 255.255.255.192
```

## Verification Commands

```cisco
show ip route
show ip eigrp neighbors
show ip eigrp topology
show ip eigrp interfaces
show ip eigrp traffic
ping 192.168.2.50
```

## Verification Results

- EIGRP neighbors established on backbone and serial links.
- EIGRP routes learned with administrative distance 90.
- P1R1 generated a local 192.168.1.0/26 summary route to Null0.
- P2R1 generated a local 192.168.2.0/26 summary route to Null0.
- P2R1 learned the 192.168.1.0/26 summary through P1R1.
- P1R3 successfully pinged 192.168.2.50 with 100% success (5/5).

## Key Concepts

EIGRP manual summarization reduces advertised routing prefixes and can improve routing-table scalability.

A local Null0 summary route helps prevent routing loops for destinations within the summary that lack a more-specific route.

Summarization may briefly reset an EIGRP neighbor adjacency on some Cisco IOS implementations.

## Skills Demonstrated

- Cisco IOS CLI configuration
- EIGRP IPv4 routing
- Neighbor adjacency verification
- EIGRP DUAL topology analysis
- Manual route summarization
- Routing-table troubleshooting
- ICMP connectivity verification

## Evidence

Screenshots included in this folder document the topology, router configurations, EIGRP neighbors, topology tables, summarized routes, and connectivity tests.

**CCNP Enterprise Home Lab - Lab 21**
  
