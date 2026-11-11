EIGRP Basic Configuration — CCNP Home Lab

Lab Overview

This lab demonstrates the configuration and verification of Enhanced Interior Gateway Routing Protocol (EIGRP) on two Cisco routers.

The objective is to establish EIGRP neighbor adjacency, advertise connected networks, exchange routing information, and verify end-to-end IP connectivity.

Lab Objectives

* Configure IPv4 addresses on Cisco router interfaces.
* Enable EIGRP using Autonomous System 10.
* Advertise connected networks using EIGRP network statements.
* Establish EIGRP neighbor adjacency.
* Verify EIGRP-learned routes in the routing table.
* Examine EIGRP interfaces, neighbors, and topology information.
* Verify connectivity using ICMP ping.

Network Topology

HostA — Router1 — Router2 — HostB

IP Addressing Table

Device	Interface	IP Address	Subnet Mask
Router1	FastEthernet0/0	192.168.101.1	255.255.255.0
Router1	Serial0/0	192.168.1.1	255.255.255.0
Router2	Serial0/0	192.168.1.2	255.255.255.0
Router2	FastEthernet0/0	192.168.100.1	255.255.255.0

Router1 Configuration

enable
configure terminal
hostname Router1
interface FastEthernet0/0
 ip address 192.168.101.1 255.255.255.0
 no shutdown
 exit
interface Serial0/0
 ip address 192.168.1.1 255.255.255.0
 clock rate 64000
 no shutdown
 exit
router eigrp 10
 network 192.168.101.0 0.0.0.255
 network 192.168.1.0 0.0.0.255
end

Note: The clock rate command is applied on the DCE side of the serial connection.

Router2 Configuration

enable
configure terminal
hostname Router2
interface Serial0/0
 ip address 192.168.1.2 255.255.255.0
 no shutdown
 exit
interface FastEthernet0/0
 ip address 192.168.100.1 255.255.255.0
 no shutdown
 exit
router eigrp 10
 network 192.168.1.0 0.0.0.255
 network 192.168.100.0 0.0.0.255
end

EIGRP Verification Commands

show ip route
show eigrp protocols
show ip eigrp interfaces
show ip eigrp interfaces detail
show ip eigrp neighbors
show ip eigrp topology
show ip eigrp traffic

Verification Results

1. EIGRP Neighbor Adjacency

Both routers successfully established an EIGRP neighbor relationship through Serial0/0.

* EIGRP Autonomous System: 10
* Router1 Neighbor: 192.168.1.2
* Router2 Neighbor: 192.168.1.1
* EIGRP Neighbor Count: 1 on each router

2. EIGRP Routing Table

Router1 learned the remote network:

D 192.168.100.0/24 [90/2172416] via 192.168.1.2, Serial0/0

Router2 learned the remote network:

D 192.168.101.0/24 [90/2172416] via 192.168.1.1, Serial0/0

The letter D identifies an EIGRP-learned route.

The administrative distance of internal EIGRP routes is 90.

3. EIGRP Topology Table

The EIGRP topology table displayed:

* Connected networks
* EIGRP-learned networks
* Successor routes
* Feasible Distance (FD)
* Passive route states

The remote networks were successfully installed as successor routes.

4. Connectivity Verification

Router1 successfully pinged 192.168.100.2.

Router1#ping 192.168.100.2
Success rate is 100 percent (5/5)

This confirms successful IP connectivity to the remote host.

Key Concepts Demonstrated

* EIGRP Dynamic Routing
* Autonomous System Configuration
* EIGRP Neighbor Discovery
* EIGRP DUAL Algorithm
* EIGRP Routing Table
* Successor Routes
* Feasible Distance
* EIGRP Metrics
* Administrative Distance
* Network Advertisement
* EIGRP Troubleshooting and Verification

Lab Results

* EIGRP AS 10 configured successfully.
* Neighbor adjacency established.
* Remote networks learned dynamically.
* Routing tables updated successfully.
* EIGRP topology verified.
* ICMP connectivity test passed.

Conclusion

This lab demonstrates successful implementation of EIGRP dynamic routing between two Cisco routers.

The configuration and verification process demonstrates practical networking skills in routing protocols, IP addressing, neighbor adjacency, route advertisement, routing table analysis, and network troubleshooting.

Lab Category: Cisco CCNP Enterprise — Routing and Switching

Repository: CCNP Home Lab
