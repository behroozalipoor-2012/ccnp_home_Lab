# GLBP (Gateway Load Balancing Protocol) Lab

## Objective

Configure and verify GLBP to provide first-hop gateway redundancy and load balancing between multiple routers.

## Lab Overview

In this lab, three routers (R1, R2, and R3) participate in GLBP Group 10.

GLBP provides a single virtual default gateway for the PCs while allowing multiple routers to forward traffic.

### GLBP Information

- GLBP Group: 10
- Virtual IP Address: 10.10.10.25
- R1 Priority: 110
- Preemption: Enabled
- Load-Balancing Method: Round-Robin
- Routers: R1, R2, R3

## Key Configuration

Example configuration used on R1:

    interface Ethernet0/3
     glbp 10 ip 10.10.10.25
     glbp 10 priority 110
     glbp 10 preempt
     glbp 10 load-balancing round-robin

The other routers participate in the same GLBP group and use the same virtual IP address.

## Verification

GLBP operation was verified using:

    show glbp
    show glbp brief

The output confirms the GLBP Active Virtual Gateway (AVG) and multiple Active Virtual Forwarders (AVFs).

The virtual MAC addresses used by the GLBP forwarders include:

    0007.b400.0a01
    0007.b400.0a02
    0007.b400.0a03

## Load-Balancing Test

The PCs use the GLBP virtual IP address as their default gateway:

    10.10.10.25

Traceroute tests to:

    203.0.113.56

show traffic being forwarded through different physical routers, demonstrating GLBP load balancing.

Examples of first-hop routers observed:

    10.10.10.1
    10.10.10.2
    10.10.10.3

## Skills Demonstrated

- GLBP configuration
- First-Hop Redundancy Protocols
- Gateway redundancy
- GLBP AVG/AVF operation
- GLBP priority and preemption
- Round-robin load balancing
- GLBP verification and troubleshooting
- Traceroute testing
