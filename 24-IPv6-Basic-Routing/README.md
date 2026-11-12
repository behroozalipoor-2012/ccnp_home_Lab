Lab 24 - IPv6 Basic Routing Configuration and Verification

CCNP Enterprise Home Lab

Lab Objective

Configure and verify basic IPv6 connectivity across four Cisco routers using IPv6 unicast routing, interface addressing, loopback interfaces, and ICMPv6 connectivity testing.

Network Topology

The lab consists of:

* 4 Cisco routers: P1R1, P1R2, P1R3, P1R4
* 2 additional routers: BB1 and BB2
* 1 Layer 2 switch
* 1 TFTP server
* Serial and FastEthernet connections
* IPv6 loopback interfaces
* Frame Relay infrastructure

IPv6 Addressing Table

Router	Interface	IPv6 Address
P1R1	Serial0	2001:0:1:0::1/64
P1R1	FastEthernet0/0	2001:0:1:1::1/64
P1R1	Loopback0	1:1:1:1::1/64
P1R2	Serial0	2001:0:1:0::2/64
P1R2	FastEthernet0/0	2001:0:1:2::2/64
P1R2	Loopback0	1:1:2:2::2/64
P1R3	Serial0	2001:0:1:3::3/64
P1R3	FastEthernet0/0	2001:0:1:1::3/64
P1R3	Loopback0	1:1:3:3::3/64
P1R4	Serial0	2001:0:1:3::4/64
P1R4	FastEthernet0/0	2001:0:1:2::4/64
P1R4	Loopback0	1:1:4:4::4/64

Configuration Steps

1. Enable IPv6 Routing

Applied on all four routers:

configure terminal
ipv6 unicast-routing
ipv6 cef

2. Configure IPv6 Interfaces

Example configuration on P1R1:

interface Serial0
 ipv6 address 2001:0:1:0::1/64
 no shutdown
interface FastEthernet0/0
 ipv6 address 2001:0:1:1::1/64
 no shutdown
interface Loopback0
 ipv6 address 1:1:1:1::1/64
 no shutdown

Similar configurations were applied on P1R2, P1R3, and P1R4 using their assigned IPv6 addresses.

Verification Commands

The following Cisco IOS commands were used:

show ipv6 route
ping ipv6 2001:0:1:1::1
ping ipv6 2001:0:1:0::1
ping ipv6 1:1:1:1::1

Routing Table Verification

Verified directly connected IPv6 networks and local interface routes.

Routing table codes:

* C - Connected
* L - Local
* S - Static
* O - OSPF
* D - EIGRP
* B - BGP

IPv6 Connectivity Testing

ICMPv6 echo requests were successfully tested on the configured interfaces.

Observed results:

* P1R1: 100% success (5/5) on three local interface addresses
* P1R3: 100% success (5/5) on its FastEthernet address
* P1R4: 100% success (5/5) on its Serial interface address

Key Concepts Practiced

* IPv6 global unicast addressing
* IPv6 prefix length /64
* IPv6 unicast routing
* Cisco Express Forwarding for IPv6
* IPv6 interface configuration
* IPv6 loopback interfaces
* Connected and local IPv6 routes
* IPv6 routing table verification
* ICMPv6 connectivity testing

Lab Results

Status: Basic IPv6 configuration and local connectivity verification successful.

IPv6 addressing was configured on four routers. The screenshots demonstrate connected and local IPv6 routing table entries and successful interface connectivity tests.

End-to-end routing between non-directly connected IPv6 networks was not yet demonstrated.

Skills Demonstrated

Cisco IOS CLI | IPv6 | CCNP Enterprise | Network Configuration | Routing Table Analysis | Network Verification | Troubleshooting

⸻

Lab 24 - CCNP Enterprise Home Lab Portfolio
