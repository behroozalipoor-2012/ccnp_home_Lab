# HSRP Multiple Groups Lab

## Overview

This lab demonstrates the configuration of multiple HSRP groups across two Cisco distribution switches.

Two HSRP groups are configured with different virtual IP addresses and priorities. This allows the distribution switches to provide redundant default gateways while also sharing the active gateway role.

## Lab Objectives

- Configure multiple HSRP groups
- Configure separate virtual gateway addresses
- Configure different HSRP priorities
- Configure HSRP preemption
- Distribute Active gateway roles between DSW1 and DSW2
- Verify HSRP Active and Standby states
- Test client connectivity
- Verify traffic paths using traceroute

## HSRP Groups

### Group 10

**Virtual IP:** `172.16.3.252`

DSW1:

```cisco
interface vlan 1
 standby 10 ip 172.16.3.252
 standby 10 priority 120
 standby 10 preempt
```

DSW2:

```cisco
interface vlan 1
 standby 10 ip 172.16.3.252
 standby 10 priority 90
 standby 10 preempt
```

For Group 10, **DSW1 is preferred as Active** because it has the higher priority.

---

### Group 20

**Virtual IP:** `172.16.3.254`

DSW1:

```cisco
interface vlan 1
 standby 20 ip 172.16.3.254
 standby 20 priority 90
 standby 20 preempt
```

DSW2:

```cisco
interface vlan 1
 standby 20 ip 172.16.3.254
 standby 20 priority 120
 standby 20 preempt
```

For Group 20, **DSW2 is preferred as Active** because it has the higher priority.

## HSRP Load Sharing

The HSRP priorities were intentionally configured differently between the two groups.

| HSRP Group | Virtual IP | DSW1 Priority | DSW2 Priority | Preferred Active |
|---|---|---:|---:|---|
| 10 | 172.16.3.252 | 120 | 90 | DSW1 |
| 20 | 172.16.3.254 | 90 | 120 | DSW2 |

This allows both distribution switches to participate as Active gateways instead of having one switch remain Active for all HSRP groups.

## Preemption

HSRP preemption was enabled using:

```cisco
standby 10 preempt
standby 20 preempt
```

Preemption allows the switch with the higher configured priority to regain the Active role when it becomes available.

## Verification

HSRP operation was verified using:

```cisco
show standby
```

The output was used to confirm:

- HSRP group numbers
- Virtual IP addresses
- Active router
- Standby router
- HSRP priorities
- Preemption status
- HSRP state transitions

## Client Testing

Client connectivity was tested using ping to the distribution switches, virtual gateways, and remote network addresses.

Example:

```text
ping 172.16.3.252
ping 172.16.3.254
ping 172.16.253.2
```

The successful tests showed **0% packet loss**.

## Path Verification

Traceroute was used to verify which distribution switch was forwarding traffic.

```text
tracert 172.16.253.2
```

The observed first-hop gateway changed depending on the HSRP gateway being used, demonstrating traffic distribution between the two distribution switches.

## Skills Demonstrated

- HSRP
- Multiple HSRP Groups
- First Hop Redundancy Protocols (FHRP)
- Gateway Redundancy
- HSRP Priority
- HSRP Preemption
- Gateway Load Sharing
- Layer 3 Switching
- Cisco IOS Configuration
- Ping and Traceroute Testing
- Network Troubleshooting

## Conclusion

This lab demonstrates how multiple HSRP groups can provide both gateway redundancy and traffic distribution. By assigning different priorities to DSW1 and DSW2 for each HSRP group, each distribution switch can serve as the preferred Active gateway for a different group while maintaining a redundant Standby device.
