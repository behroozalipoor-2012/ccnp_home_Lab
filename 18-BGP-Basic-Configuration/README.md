# Basic BGP Configuration — eBGP and iBGP Lab

## Objective
Configure and verify Border Gateway Protocol (BGP) between two autonomous systems, including eBGP and iBGP neighbor relationships, network advertisements, routing verification, and connectivity testing.

## Network Topology
![BGP Topology](01-BGP-Topology.jpeg)

- AS 1: P1R1, P1R2, P1R3
- AS 2: P2R1, P2R2, P2R3
- Backbone: 10.100.100.0/24
- eBGP: P1R1 (AS 1) to P2R1 (AS 2)
- iBGP: P1R1 to P1R2 (AS 1)

## P1R1 — BGP Configuration
```cisco
router bgp 1
 neighbor 10.100.100.2 remote-as 2
 neighbor 192.168.1.34 remote-as 1
 network 10.100.100.0 mask 255.255.255.0
 network 192.168.1.1 mask 255.255.255.255
 network 192.168.1.32 mask 255.255.255.252
```

## P1R2 — BGP Configuration
```cisco
router bgp 1
 neighbor 192.168.1.33 remote-as 1
 network 192.168.1.32 mask 255.255.255.252
 network 192.168.1.48 mask 255.255.255.240
 network 192.168.1.17 mask 255.255.255.255
```

## Verification Commands
```cisco
show ip bgp summary
show ip bgp
show ip bgp neighbors
show ip route
ping 192.168.2.1
ping 192.168.2.17
```

## Results
- eBGP adjacency between AS 1 and AS 2 successfully established.
- iBGP adjacency between P1R1 and P1R2 successfully established.
- BGP routes learned and installed in the routing table.
- AS-path and next-hop attributes verified.
- ICMP connectivity tests completed successfully (5/5).

## Screenshots
1. [BGP Network Topology](01-BGP-Topology.jpeg)
2. [P1R1 Configuration](02-P1R1-Configuration.jpeg)
3. [P1R1 BGP Verification](03-P1R1-BGP-Verification.jpeg)
4. [P1R1 iBGP Verification](04-P1R1-iBGP-Verification.jpeg)
5. [P1R2 Configuration](05-P1R2-Configuration.jpeg)
6. [P1R2 Routing Verification](06-P1R2-Routing-Verification.jpeg)

## Skills Demonstrated
- Cisco IOS router configuration
- BGP neighbor establishment
- eBGP and iBGP
- IPv4 network advertisements
- BGP routing table analysis
- AS-path and next-hop verification
- End-to-end connectivity testing

## Next Steps
Practice BGP path selection, Local Preference, MED, Weight, AS-path prepending, and route filtering.

*CCNP ENCOR / ENARSI Hands-on Lab*
