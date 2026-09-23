# Layer 3 Switching with EIGRP Lab

## Objective

The purpose of this lab is to configure Layer 3 switching and establish dynamic routing between multilayer switches using EIGRP.

## Technologies Used

- Cisco Multilayer Switching
- Switch Virtual Interfaces (SVIs)
- Inter-VLAN Routing
- IP Routing
- EIGRP
- VLANs
- IPv4 Addressing
- Connectivity Testing

## Configuration Overview

### Access Switch P1ASW1

Management SVI:

172.16.1.10/24

Default Gateway:

172.16.1.100

### Distribution Switch P1DSW1

VLAN 1 SVI:

172.16.1.100/24

VLAN 11 SVI:

172.16.11.100/24

Layer 3 routing was enabled using:

ip routing

EIGRP was configured with:

router eigrp 100
network 172.16.0.0

### Access Switch P2ASW2

Management SVI:

172.16.1.20/24

Default Gateway:

172.16.1.200

### Distribution Switch P2DSW2

VLAN 1 SVI:

172.16.1.200/24

VLAN 12 SVI:

172.16.12.200/24

Layer 3 routing was enabled using:

ip routing

EIGRP was configured with:

router eigrp 100
network 172.16.0.0

## Verification

The following commands were used to verify the configuration:

show protocols

show ip route

ping

EIGRP neighbor formation was observed through the DUAL neighbor-change messages.

The routing tables were checked before and after enabling EIGRP.

End-to-end connectivity was tested using ICMP ping.

## Troubleshooting

During testing, some initial ping attempts failed. After routing convergence and verification of the Layer 3 configuration, connectivity was successfully established.

This demonstrated the importance of checking:

- SVI addressing
- IP routing
- Default gateways
- Routing tables
- EIGRP neighbor relationships
- End-to-end connectivity

## Skills Demonstrated

- Configuring Layer 3 switches
- Configuring SVIs
- Enabling IP routing
- Configuring EIGRP
- Verifying routing tables
- Testing network connectivity
- Troubleshooting Layer 3 connectivity
