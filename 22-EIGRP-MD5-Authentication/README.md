
# Lab 22 – EIGRP MD5 Authentication

## Objective
Configure and verify EIGRP MD5 authentication in a four-router Cisco network using EIGRP Autonomous System 100.

## Lab Topology
The topology consists of four Cisco routers connected through serial WAN links and FastEthernet LAN segments.

### Network Addressing
- R1–R2: 10.2.112.0/24
- R3–R4: 10.2.134.0/24
- R1–R3: 172.20.13.0/24
- R2–R4: 172.20.24.0/24

## Technologies Used
- Cisco IOS
- EIGRP AS 100
- EIGRP MD5 Authentication
- Key-Chain Configuration
- Authentication Key Lifetimes
- EIGRP Neighbor Verification
- EIGRP Packet Debugging
- Routing Table Verification
- ICMP Connectivity Testing

## Configuration

### 1. Configure EIGRP
```cisco
router eigrp 100
 network 10.2.0.0
 network 172.20.0.0
 no auto-summary
```

### 2. Configure LAN Authentication Key
```cisco
key chain LANKey
 key 1
  key-string BosonLAN
  accept-lifetime 01:00:00 Jan 1 2025 infinite
  send-lifetime 01:00:00 Jan 1 2025 infinite
```

### 3. Configure WAN Authentication Key
```cisco
key chain WANKey
 key 1
  key-string BosonWAN
  accept-lifetime 01:00:00 Jan 1 2025 infinite
  send-lifetime 01:00:00 Jan 1 2025 infinite
```

### 4. Enable MD5 Authentication on WAN
```cisco
interface Serial0/2
 ip authentication mode eigrp 100 md5
 ip authentication key-chain eigrp 100 WANKey
```

Note: Interface names differ between routers.

### 5. Enable MD5 Authentication on LAN
```cisco
interface FastEthernet1/0
 ip authentication mode eigrp 100 md5
 ip authentication key-chain eigrp 100 LANKey
```

## Verification Commands
```cisco
show key chain
show ip eigrp neighbors
show ip eigrp interface detail
show ip route
debug eigrp packets
no debug eigrp packets
ping 172.20.24.2
```

## Verification Results
- EIGRP AS 100 configured.
- LAN and WAN key chains created.
- MD5 authentication enabled on interfaces.
- Authentication key lifetimes verified.
- EIGRP neighbors established after configuration.
- Debug output confirmed receipt of MD5-authenticated packets.
- EIGRP-learned routes appeared in the routing table.
- ICMP connectivity test achieved 100% success (5/5).

## Troubleshooting
- Observed temporary neighbor adjacency changes during authentication configuration.
- Verified matching authentication settings and key chains.
- Confirmed EIGRP neighbors re-established.
- Used packet debugging to inspect authenticated EIGRP traffic.

## Skills Demonstrated
- EIGRP routing configuration
- Routing protocol authentication
- Cisco key-chain management
- EIGRP adjacency troubleshooting
- Cisco IOS debugging
- Network connectivity verification

## Lab Screenshots
See the screenshots uploaded in this folder for topology, configuration, authentication verification, debugging, neighbor tables, routing information, and ping results.

## Conclusion
Successfully configured and verified EIGRP MD5 authentication in a four-router Cisco lab environment.
