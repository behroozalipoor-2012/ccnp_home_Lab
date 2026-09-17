# Layer 2 EtherChannel Lab

## Overview

This lab demonstrates the configuration and verification of a Layer 2 EtherChannel between two distribution switches, DSW1 and DSW2.

Two physical FastEthernet links were bundled into a single logical Port-Channel interface to provide increased bandwidth and link redundancy.

## Lab Objectives

- Configure a Layer 2 EtherChannel
- Bundle Fa0/5 and Fa0/6 into Port-Channel 1
- Configure static EtherChannel using `mode on`
- Configure Port-Channel 1 as an 802.1Q trunk
- Verify EtherChannel operation
- Verify trunking and Spanning Tree behavior

## EtherChannel Configuration

Configuration performed on the participating interfaces:

```cisco
interface range FastEthernet0/5 - 6
 shutdown
 channel-group 1 mode on
 no shutdown
