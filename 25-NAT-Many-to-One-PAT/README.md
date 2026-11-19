Lab 25 - Many-to-One NAT (PAT / NAT Overload)

Lab Overview

This lab demonstrates the configuration, implementation, and verification of Many-to-One Network Address Translation (NAT), also known as Port Address Translation (PAT) or NAT Overload, using Cisco routers.

The objective is to allow multiple private IP addresses from an internal LAN to share a single translated IP address when communicating with an external network.

The lab also uses RIPv2 to provide routing connectivity between two routers.

Lab Objectives

* Configure IP addressing on Cisco routers.
* Establish connectivity between Router1 and Router2.
* Configure RIPv2 dynamic routing.
* Configure a standard ACL to identify inside NAT addresses.
* Implement Many-to-One NAT using PAT Overload.
* Identify NAT inside and outside interfaces.
* Verify NAT translations and statistics.
* Test end-to-end connectivity using ICMP.

Network Topology

HostA — Router1 — Router2 — HostB

IP Addressing Table

Device	Interface	IP Address	Subnet Mask
Router1	Fa0/0	192.168.101.1	255.255.255.0
Router1	S0/0	192.168.1.1	255.255.255.252
Router2	S0/0	192.168.1.2	255.255.255.252
Router2	Fa0/0	192.168.100.1	255.255.255.0
HostA	LAN	192.168.101.0/24	
HostB	LAN	192.168.100.0/24	

Router1 Configuration

Configure Interfaces

enable
configure terminal
hostname Router1
interface serial 0/0
 ip address 192.168.1.1 255.255.255.252
 clock rate 64000
 no shutdown
exit
interface fastEthernet 0/0
 ip address 192.168.101.1 255.255.255.0
 no shutdown
exit

Configure RIPv2

router rip
 version 2
 network 192.168.101.0
 network 192.168.1.0
exit

Configure NAT Access Control List

access-list 12 permit 192.168.101.0 0.0.0.255

The ACL identifies the internal network whose source IP addresses are eligible for NAT translation.

Configure Many-to-One NAT (PAT)

ip nat inside source list 12 interface serial 0/0 overload

The overload keyword enables multiple inside hosts to share the IP address assigned to Router1’s Serial0/0 interface.

Identify NAT Interfaces

interface fastEthernet 0/0
 ip nat inside
exit
interface serial 0/0
 ip nat outside
exit

Router2 Configuration

Configure Interfaces

enable
configure terminal
hostname Router2
interface serial 0/0
 ip address 192.168.1.2 255.255.255.252
 clock rate 64000
 no shutdown
exit
interface fastEthernet 0/0
 ip address 192.168.100.1 255.255.255.0
 no shutdown
exit

Configure RIPv2

router rip
 version 2
 network 192.168.1.0
 network 192.168.100.0
exit

Router2 does not require NAT configuration for this lab. NAT is performed by Router1.

NAT Verification

Verify Access Control List

show access-lists
show access-lists 12

Observed result:

Standard IP access list 12
10 permit 192.168.101.0, wildcard bits 0.0.0.255

Verify NAT Translations

show ip nat translations

Observed ICMP translation:

Protocol:       icmp
Inside global:  192.168.1.1:3558
Inside local:   192.168.101.2:3558
Outside local:  192.168.100.2:3558
Outside global: 192.168.100.2:3558

This confirms that Router1 translated the source IP address of HostA from 192.168.101.2 to 192.168.1.1.

Verify NAT Statistics

show ip nat statistics

Observed statistics:

* Outside interface: Serial0/0
* Inside interface: FastEthernet0/0
* NAT hits: 5
* NAT misses: 5
* Expired translations: 5
* NAT ACL: 12
* NAT translation interface: Serial0/0

The screenshots also show zero active translations at one verification point because translations had expired.

Connectivity Testing

HostA successfully pinged HostB.

ping 192.168.100.2
Packets: Sent = 5, Received = 5, Lost = 0
Minimum = 1ms
Maximum = 57ms
Average = 12ms

Result: Successful end-to-end ICMP connectivity with 0% packet loss.

Troubleshooting Commands

show ip interface brief
show ip route
show ip protocols
show access-lists
show running-config
show ip nat translations
show ip nat statistics
ping 192.168.100.2

Common NAT Troubleshooting Checks

1. Verify inside and outside interface assignments.
2. Confirm that the ACL matches the internal subnet.
3. Check the NAT overload configuration.
4. Verify interface status.
5. Verify routing to the destination network.
6. Generate traffic and inspect the NAT translation table.
7. Check NAT statistics for translation activity.

Technical Summary

Successfully configured and verified Many-to-One NAT using PAT Overload on Router1.

The configuration translates internal source IP addresses from the 192.168.101.0/24 network to Router1’s Serial0/0 IP address, 192.168.1.1.

RIPv2 provides routing connectivity between the two LANs.

ICMP testing and NAT translation outputs demonstrate that the configured NAT policy is functioning.

Note: This lab demonstrates PAT functionality using one observed inside host. Testing simultaneous connections from multiple inside hosts would further demonstrate the Many-to-One capability.

Skills Demonstrated

* Cisco IOS CLI configuration
* NAT and PAT implementation
* ACL configuration
* RIPv2 dynamic routing
* IP addressing and subnetting
* NAT translation verification
* ICMP connectivity testing
* Network troubleshooting

Lab Category: CCNP Enterprise Networking
Lab Number: 25
Technology: NAT / PAT / NAT Overload
Platform: Cisco IOS
