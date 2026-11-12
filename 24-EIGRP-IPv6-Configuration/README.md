EIGRP IPv6 Configuration and Verification

CCNP Enterprise Home Lab — Lab 24

Lab Overview

This lab demonstrates the configuration and verification of Enhanced Interior Gateway Routing Protocol (EIGRP) for IPv6 across three Cisco routers.

The objective is to establish EIGRP IPv6 neighbor relationships, exchange IPv6 routing information, verify the EIGRP topology table, and confirm end-to-end IPv6 connectivity.

Lab Objectives

* Enable IPv6 unicast routing.
* Configure EIGRP for IPv6 using Autonomous System 10.
* Assign unique EIGRP router IDs.
* Enable EIGRP on router interfaces.
* Establish IPv6 EIGRP neighbor adjacencies.
* Verify dynamically learned IPv6 routes.
* Examine the EIGRP topology table.
* Verify IPv6 connectivity using ICMPv6.

Network Topology

Three routers are connected in the following arrangement:

Router2 (Fa0/0) — Router1 (Fa0/0)

Router1 (S0/0) — Router3 (S0/0)

IPv6 Addressing

Network	IPv6 Prefix
Router1–Router2	2001:DB8:1:1::/64
Router1–Router3	2001:DB8:2:1::/64
Router1 Loopback0	2001:DB8:1:3::/64
Router2 Loopback0	2001:DB8:1:2::/64
Router3 Loopback0	2001:DB8:2:2::/64

EIGRP Configuration

Router1

configure terminal
ipv6 unicast-routing
ipv6 router eigrp 10
 router-id 1.1.1.1
 no shutdown
exit
interface serial 0/0
 ipv6 eigrp 10
exit
interface fastEthernet 0/0
 ipv6 eigrp 10
exit
interface loopback 0
 ipv6 eigrp 10
end

Router2

configure terminal
ipv6 unicast-routing
ipv6 router eigrp 10
 router-id 2.2.2.2
 no shutdown
exit
interface fastEthernet 0/0
 ipv6 eigrp 10
exit
interface loopback 0
 ipv6 eigrp 10
end

Router3

configure terminal
ipv6 unicast-routing
ipv6 router eigrp 10
 router-id 3.3.3.3
 no shutdown
exit
interface serial 0/0
 ipv6 eigrp 10
exit
interface loopback 0
 ipv6 eigrp 10
end

Note: IPv6 interface addresses were already assigned in the lab environment. The configurations above document the EIGRP-related commands.

Verification Commands

show ipv6 protocols
show ipv6 eigrp neighbors
show ipv6 eigrp topology
show ipv6 eigrp topology all-links
show ipv6 eigrp traffic
show ipv6 route

Verification Results

1. EIGRP Neighbor Adjacencies

Router1 successfully established two EIGRP IPv6 neighbor relationships:

* Router2 through FastEthernet0/0.
* Router3 through Serial0/0.

Router2 and Router3 each established an EIGRP neighbor relationship with Router1.

2. IPv6 Routing Table

Router1 successfully learned:

* 2001:DB8:1:2::/64 through Router2.
* 2001:DB8:2:2::/64 through Router3.

EIGRP routes were identified by the D code with administrative distance 90.

3. EIGRP Topology Table

The EIGRP topology table displayed connected and learned IPv6 networks, successor routes, feasible distances, and next-hop information.

Routes were in the Passive state, indicating stable EIGRP topology entries.

4. IPv6 Connectivity Testing

Successful ICMPv6 tests included:

* Router2 to 2001:DB8:1:1::2 — 100% success (5/5).
* Router3 to 2001:DB8:1:1::2 — 100% success (5/5).

Technical Concepts Demonstrated

* EIGRP for IPv6
* IPv6 link-local neighbor discovery
* EIGRP Autonomous System configuration
* EIGRP router IDs
* DUAL routing algorithm
* Successor route selection
* Feasible Distance (FD)
* IPv6 routing table analysis
* ICMPv6 connectivity testing
* EIGRP neighbor and topology verification

Lab Outcome

Successfully configured and verified EIGRP IPv6 routing across a three-router Cisco network.

The lab demonstrates practical skills in dynamic IPv6 routing, EIGRP neighbor establishment, route advertisement, topology analysis, and network connectivity verification.

Technology: Cisco IOS | EIGRP IPv6 | IPv6 Routing | CCNP Enterprise

Repository: CCNP Enterprise Home Labs
