# EtherChannel Using PAgP

## Objective

Configure and verify a Layer 2 EtherChannel between distribution switches using Cisco PAgP (Port Aggregation Protocol).

## Interfaces

The EtherChannel uses:

- FastEthernet0/5
- FastEthernet0/6
- Port-Channel1

## PAgP Configuration

Example configuration:

```cisco
interface range FastEthernet0/5 - 6
 channel-protocol pagp
 channel-group 1 mode desirable
