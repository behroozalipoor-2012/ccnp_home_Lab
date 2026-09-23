# HSRP (Hot Standby Router Protocol) Lab

## Overview

This lab demonstrates the configuration and verification of HSRP on two Cisco distribution switches to provide first-hop gateway redundancy.

HSRP allows multiple Layer 3 devices to share a virtual default gateway. If the active device becomes unavailable, the standby device can take over the gateway role.

## Lab Objectives

- Configure HSRP on two distribution switches
- Configure a shared virtual default gateway
- Configure HSRP priority
- Configure preemption
- Verify Active and Standby roles
- Test HSRP failover
- Verify end-to-end connectivity using ping and traceroute

## HSRP Configuration

**HSRP Group:** 3  
**Virtual IP Address:** 172.16.3.1

### DSW1

```cisco
interface vlan 1
 standby 3 ip 172.16.3.1
 standby 3 priority 90
 standby 3 preempt
```

DSW1 SVI address:

```text
172.16.3.3
```

### DSW2

```cisco
interface vlan 1
 standby 3 ip 172.16.3.1
 standby 3 priority 120
 standby 3 preempt
```

DSW2 SVI address:

```text
172.16.3.2
```

## HSRP Roles

Because DSW2 has the higher HSRP priority, it becomes the **Active** router.

- DSW2 — Priority 120 — Active
- DSW1 — Priority 90 — Standby
- Virtual Gateway — 172.16.3.1

Preemption allows the device with the higher priority to regain the Active role when it becomes available again.

## Verification

The HSRP state was verified with:

```cisco
show standby
```

The output confirmed the Active and Standby HSRP devices and the virtual IP address.

## Failover Testing

Failover was tested by shutting down the VLAN interface on the Active HSRP device and observing the HSRP state transition.

```cisco
interface vlan 1
 shutdown
```

The redundant switch assumed the Active role.

The interface was then restored:

```cisco
interface vlan 1
 no shutdown
```

With preemption enabled, the higher-priority switch was able to regain the Active role.

## Connectivity Testing

Connectivity was verified using:

```text
ping
tracert
```

The client successfully reached the remote network with 0% packet loss.

Traceroute was also used to observe the Layer 3 path and verify gateway redundancy during the HSRP testing.

## Skills Demonstrated

- Cisco HSRP
- First Hop Redundancy Protocols (FHRP)
- Layer 3 Switching
- Default Gateway Redundancy
- HSRP Priority
- HSRP Preemption
- Network Failover Testing
- Ping and Traceroute Verification
- Cisco IOS Troubleshooting

## Conclusion

This lab demonstrates how HSRP provides a redundant default gateway in a switched network. By using HSRP priorities and preemption, the distribution switches can automatically determine Active and Standby roles and provide gateway availability during a device or interface failure.
