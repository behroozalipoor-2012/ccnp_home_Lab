# Lab 20 - EIGRP Configuration and MD5 Authentication

## Lab Overview
This CCNP networking lab demonstrates EIGRP routing, neighbor adjacency formation, automatic route summarization, topology table verification, MD5 authentication, and EIGRP troubleshooting using four Cisco routers.

## Lab Objectives
- Configure EIGRP using Autonomous System 100.
- Advertise connected networks through EIGRP.
- Establish and verify EIGRP neighbor relationships.
- Examine EIGRP topology tables and traffic statistics.
- Observe automatic route summarization.
- Configure MD5 authentication using key chains.
- Troubleshoot EIGRP neighbor adjacency changes.
- Verify end-to-end connectivity using ICMP ping tests.

## Network Topology
The lab consists of four routers:

- Router1 connected to Router2 through 160.10.1.0/24.
- Router1 connected to Router3 through 175.10.1.0/24.
- Router3 connected to Router4 through 180.10.1.0/24.
- Router1 Loopback0: 160.10.2.0/24.
- Router3 network: 197.10.1.0/24.
- Router4 LAN: 192.168.1.0/24.

## EIGRP Configuration
EIGRP Autonomous System: 100

### Router1
```cisco
configure terminal
router eigrp 100
 auto-summary
 network 160.10.0.0
 network 175.10.0.0
end
```

### Router2
```cisco
configure terminal
router eigrp 100
 auto-summary
 network 160.10.0.0
end
```

### Router3
```cisco
configure terminal
router eigrp 100
 auto-summary
 network 175.10.0.0
 network 197.10.0.0
 network 180.10.0.0
end
```

### Router4
```cisco
configure terminal
router eigrp 100
 auto-summary
 network 180.10.0.0
 network 192.168.0.0
end
```

## EIGRP MD5 Authentication

MD5 authentication was configured on the serial connection between Router3 and Router4.

### Router3 - Serial0/1
```cisco
configure terminal
key chain eigrp-chain
 key 1
  key-string <shared-key>
exit
exit
interface serial 0/1
 ip authentication mode eigrp 100 md5
 ip authentication key-chain eigrp 100 eigrp-chain
end
```

### Router4 - Serial0/0
```cisco
configure terminal
key chain eigrp-chain
 key 1
  key-string <shared-key>
exit
exit
interface serial 0/0
 ip authentication mode eigrp 100 md5
 ip authentication key-chain eigrp 100 eigrp-chain
end
```

Note: Replace <shared-key> with the same lab-only secret on both routers. Do not publish real authentication keys.

## Verification Commands
```cisco
show ip protocols
show ip eigrp neighbors
show ip eigrp topology
show ip eigrp traffic
show ip route
debug eigrp neighbors
undebug all
```

## Troubleshooting and Testing
- Verified EIGRP neighbor relationships on all four routers.
- Examined successor routes and feasible distances in the topology tables.
- Observed automatic route summarization and Null0 summary routes.
- Configured matching MD5 authentication on Router3 and Router4.
- Observed EIGRP adjacency changes during authentication configuration.
- Shut down and re-enabled a serial interface to test adjacency recovery.
- Used EIGRP neighbor debugging to monitor the recovery process.
- Verified successful ICMP connectivity between Router4 and remote router interfaces.

## Lab Results
- EIGRP AS 100 neighbor adjacencies successfully established.
- EIGRP routes learned and installed in routing tables.
- MD5 authentication configured on the Router3-Router4 serial link.
- EIGRP adjacency successfully re-established after interface recovery.
- Successful ping tests to remote router interfaces.
- EIGRP troubleshooting and verification completed.

## Skills Demonstrated
- Cisco IOS CLI
- EIGRP Routing
- EIGRP DUAL and Topology Tables
- Automatic Route Summarization
- EIGRP MD5 Authentication
- Key Chain Configuration
- Neighbor Adjacency Troubleshooting
- Routing Table Verification
- Network Connectivity Testing

## Screenshots
Screenshots documenting the topology, router configurations, EIGRP neighbor tables, authentication configuration, troubleshooting, and connectivity tests are included in this folder.

## Note
This lab demonstrates classic EIGRP behavior using automatic summarization and MD5 authentication. Modern production networks commonly disable automatic summarization and may use stronger authentication mechanisms where supported.
