# GLBP Object Tracking Lab

## Objective

Configure GLBP object tracking to monitor the WAN/uplink interfaces of the GLBP routers. If a tracked interface fails, GLBP reduces the router's weighting so that it can stop acting as an Active Virtual Forwarder (AVF), allowing another GLBP router to take over forwarding traffic.

## GLBP Information

- GLBP Group: 10
- Virtual IP Address: 10.10.10.25
- Load-Balancing Method: Round-Robin
- R1 Priority: 110
- R2/R3 Priority: 100
- Tracked Interface: Ethernet0/0
- Initial Weight: 100
- Lower Threshold: 91
- Upper Threshold: 100
- Weight Decrement: 10

## Object Tracking Configuration

The WAN interface Ethernet0/0 is monitored using a tracking object.

```cisco
track 1 interface Ethernet0/0 line-protocol
