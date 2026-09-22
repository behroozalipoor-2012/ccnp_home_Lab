# LACP EtherChannel Lab

## Objective

The purpose of this lab is to configure and verify a Layer 2 EtherChannel using Link Aggregation Control Protocol (LACP) between Cisco switches.

EtherChannel combines multiple physical Ethernet links into one logical Port-Channel, providing increased bandwidth and redundancy.

## Technologies Used

- Cisco IOS
- EtherChannel
- LACP (IEEE 802.3ad / 802.1AX)
- Layer 2 Switching
- 802.1Q Trunking
- CDP

## LACP Modes

LACP supports two negotiation modes:

- Active – Actively sends LACP packets to negotiate the EtherChannel.
- Passive – Waits for LACP packets from the neighboring switch.

Valid combinations:

- Active + Active = EtherChannel forms
- Active + Passive = EtherChannel forms
- Passive + Passive = EtherChannel does not form

## Configuration

### Configure LACP EtherChannel

```cisco
configure terminal

interface range fastEthernet 0/1 - 10
 channel-protocol lacp
 channel-group 1 mode active
exit
