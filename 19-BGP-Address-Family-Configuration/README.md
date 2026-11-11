# Lab 19 – BGP Address Family Configuration

## Lab Overview

This lab demonstrates the configuration and verification of Border Gateway Protocol (BGP) using the IPv4 Unicast Address Family on Cisco routers.

The topology consists of two enterprise routers (RouterA and RouterB) operating within AS 65002 and an ISP router operating within AS 65001. The lab focuses on BGP neighbor relationships, address-family activation, network advertisement, route learning, and BGP routing table verification.

## Lab Objectives

- Configure internal BGP (iBGP) between RouterA and RouterB.
- Configure external BGP (eBGP) between enterprise routers and the ISP.
- Implement the IPv4 Unicast Address Family.
- Activate BGP neighbors under the address-family configuration.
- Advertise IPv4 networks using BGP network statements.
- Verify BGP-learned routes and best-path selection.
- Observe BGP session resets and neighbor state changes.
- Review BGP route attributes, including AS Path, Weight, and Next Hop.

## Network Topology

The topology includes:

- ISP Router – AS 65001
- RouterA – AS 65002
- RouterB – AS 65002
- SwitchA and SwitchB
- VLAN 100 and VLAN 200
- Four client PCs
- External server

### BGP Neighbor Relationships

| Device | Neighbor IP | Neighbor AS | BGP Type |
|---|---|---|---|
| RouterA | 198.51.100.2 | 65002 | iBGP |
| RouterA | 203.0.113.1 | 65001 | eBGP |
| RouterB | 198.51.100.1 | 65002 | iBGP |
| RouterB | 203.0.113.5 | 65001 | eBGP |

## RouterA – IPv4 Address Family Configuration

```cisco
router bgp 65002
 bgp log-neighbor-changes
 neighbor 198.51.100.2 remote-as 65002
 neighbor 198.51.100.2 weight 100
 neighbor 203.0.113.1 remote-as 65001
 neighbor 203.0.113.1 weight 100
 !
 address-family ipv4 unicast
  network 172.16.1.1 mask 255.255.255.255
  network 198.51.100.0 mask 255.255.255.252
  network 203.0.113.0 mask 255.255.255.252
  neighbor 198.51.100.2 activate
  neighbor 203.0.113.1 activate
 exit-address-family
```

## RouterB – IPv4 Address Family Configuration

```cisco
router bgp 65002
 bgp log-neighbor-changes
 neighbor 198.51.100.1 remote-as 65002
 neighbor 203.0.113.5 remote-as 65001
 !
 address-family ipv4 unicast
  network 172.16.0.2 mask 255.255.255.255
  network 198.51.100.0 mask 255.255.255.252
  network 203.0.113.4 mask 255.255.255.252
  neighbor 198.51.100.1 activate
  neighbor 203.0.113.5 activate
 exit-address-family
```

**Note:** The RouterB network statements above reproduce the addresses shown in the lab screenshots. The loopback network statement must match an existing route exactly to originate it into BGP. The screenshots also show RouterB's network statements under the main BGP process, rather than under the address-family section.

## BGP Verification Commands

```cisco
show ip bgp
show ip bgp summary
show running-config | section router bgp
show ip route bgp
```

The screenshots demonstrate BGP routes learned from AS 65001, local BGP routes, and IPv4 Unicast neighbor activation.

The BGP table uses the following indicators:

- * – Valid route
- > – Best path
- i – Route learned through iBGP when shown as a status code
- 0.0.0.0 – Locally originated next hop
- AS Path – Autonomous systems traversed by the route

## Troubleshooting and Observations

During configuration, several commands required correction:

1. RouterA initially used 198.51.100.0 as a BGP neighbor address. The correct peer interface address is 198.51.100.2.
2. BGP was removed and reconfigured on RouterA to introduce address-family configuration.
3. Neighbor activation commands must be entered under address-family configuration mode.
4. The clear ip bgp * command was used to reset BGP sessions after configuration changes.
5. BGP neighbor state changes were observed during the resets.
6. RouterA's final running configuration shows IPv4 address-family neighbor activation and network statements.
7. RouterB's running configuration shows IPv4 address-family neighbor activation.

## Verification Results

- RouterA's BGP table displays locally originated and ISP-learned routes.
- RouterB's BGP table displays locally originated and ISP-learned routes.
- IPv4 Unicast address-family activation is present in the final router configurations.
- The BGP tables identify valid and best routes.
- The screenshots do not establish complete end-to-end client connectivity or confirm every BGP session's final state.

## Skills Demonstrated

- Cisco IOS CLI Configuration
- BGP Routing Protocol
- iBGP and eBGP
- IPv4 Unicast Address Family
- BGP Neighbor Configuration
- Network Advertisement
- BGP Routing Table Analysis
- BGP Best Path Selection
- BGP Troubleshooting
- Enterprise Routing Fundamentals

## Conclusion

This lab demonstrates practical configuration and analysis of BGP IPv4 Unicast Address Families in a multi-router enterprise topology.

The exercise highlights the importance of correctly defining BGP neighbors, activating address-family peers, advertising matching network prefixes, and verifying routing information.

**Lab Category:** CCNP Enterprise – Advanced Routing

**Lab Number:** 19

**Technology:** BGP IPv4 Unicast Address Family
