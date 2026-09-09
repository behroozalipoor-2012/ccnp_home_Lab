# CCNP Spanning Tree Protocol (STP) Lab

## Overview

This lab demonstrates the configuration, verification, and troubleshooting of Spanning Tree Protocol in a Cisco switched network.

The lab focuses on STP/RSTP operation, root bridge election, port roles, path-cost manipulation, Rapid-PVST+, PortFast, BPDU Guard, and BPDU Filter.

## Lab Topics

- Spanning Tree Protocol (STP)
- Rapid Spanning Tree Protocol (RSTP)
- Rapid-PVST+
- Root bridge election
- Primary and secondary root bridge configuration
- Bridge priority
- Root ports
- Designated ports
- Alternate/blocked ports
- STP path cost
- Short and long path-cost methods
- PortFast
- BPDU Guard
- BPDU Filter
- Err-disabled ports
- STP verification and troubleshooting

## VLANs Used

- VLAN 421
- VLAN 422
- VLAN 423
- VLAN 424

## STP Verification

```cisco
show spanning-tree
show spanning-tree vlan 421
show spanning-tree vlan 423
```

These commands were used to identify the root bridge and examine STP port roles, states, priorities, and path costs.

## Rapid-PVST+ Configuration

```cisco
configure terminal
spanning-tree mode rapid-pvst
```

Verification:

```cisco
show spanning-tree
```

## Root Bridge Configuration

Example primary root configuration:

```cisco
spanning-tree vlan 421-422 root primary
```

Example secondary root configuration:

```cisco
spanning-tree vlan 423-424 root secondary
```

Root bridge roles were distributed between the distribution switches for different VLANs.

## STP Bridge Priority

Bridge priority can be manually changed to influence root bridge election.

Example:

```cisco
spanning-tree vlan 421 priority 0
```

Verification:

```cisco
show spanning-tree vlan 421
```

## STP Path Cost

The STP path-cost calculation method was changed to long:

```cisco
spanning-tree pathcost method long
```

Interface STP cost was also manually modified:

```cisco
interface GigabitEthernet1/0/45
spanning-tree vlan 421 cost 5
```

Multiple interfaces can be configured using an interface range:

```cisco
interface range GigabitEthernet1/0/45-48
spanning-tree vlan 421 cost 8
```

## PortFast

PortFast was configured on an access interface:

```cisco
interface GigabitEthernet1/0/45
switchport mode access
switchport access vlan 421
spanning-tree portfast
```

PortFast allows an edge/access port to transition rapidly to the forwarding state.

## BPDU Guard

BPDU Guard was enabled on the PortFast interface:

```cisco
spanning-tree bpduguard enable
```

When the interface received a BPDU, the switch placed the port into an err-disabled state.

Verification:

```cisco
show interfaces status err-disabled
show errdisable recovery
```

## BPDU Filter

BPDU Filter was also tested:

```cisco
interface GigabitEthernet1/0/45
spanning-tree bpdufilter enable
```

Verification:

```cisco
show running-config interface GigabitEthernet1/0/45
```

## Key Observations

- STP prevents Layer 2 switching loops.
- The switch with the lowest Bridge ID becomes the root bridge.
- Bridge priority can be manipulated to control root bridge election.
- Root ports provide the best path toward the root bridge.
- Alternate ports provide redundant paths and can remain blocked.
- STP path cost influences path selection.
- Rapid-PVST+ provides faster convergence than traditional STP.
- PortFast should normally be used on end-device-facing access ports.
- BPDU Guard protects PortFast interfaces from unexpected BPDUs.
- BPDU Guard can place an interface into an err-disabled state.
- BPDU Filter controls the sending and receiving of BPDUs.

## Skills Demonstrated

- Cisco IOS STP configuration
- Rapid-PVST+ configuration
- Root bridge manipulation
- STP path selection
- ST
