
# Lab 26 – Dynamic NAT (Many-to-Many)

## Objective
Configure and verify Dynamic NAT using a pool of global IPv4 addresses on Cisco Router4.

## Technologies Used
- Cisco IOS
- Dynamic NAT (Many-to-Many)
- Standard ACL
- NAT Address Pool
- EIGRP AS 100
- ICMP Connectivity Testing

## Network Information

| Component | Configuration |
|---|---|
| Inside Network | 192.168.1.0/24 |
| PC1 | 192.168.1.2/24 |
| PC1 Default Gateway | 192.168.1.1 |
| NAT Router | Router4 |
| NAT Inside Interface | FastEthernet0/1 |
| NAT Outside Interface | Serial0/0 |
| NAT Pool | NAT-Pool |
| Pool Range | 180.10.1.5 – 180.10.1.15 |
| Pool Subnet Mask | 255.255.255.224 |
| ACL | 2 |
| EIGRP AS | 100 |
| Test Destination | 180.10.1.1 |

## Router4 Configuration

```cisco
configure terminal
access-list 2 permit 192.168.1.0 0.0.0.255
ip nat pool NAT-Pool 180.10.1.5 180.10.1.15 netmask 255.255.255.224
ip nat inside source list 2 pool NAT-Pool

interface FastEthernet0/1
 ip nat inside
exit

interface Serial0/0
 ip nat outside
exit
end
```

## EIGRP Configuration Observed

```cisco
router eigrp 100
 network 180.10.0.0
 auto-summary
```

## Verification Commands

```cisco
show ip nat translations
show running-config | section router
```

## NAT Translation Observed

```text
Pro   Inside global      Inside local       Outside local       Outside global
icmp  180.10.1.5:2446    192.168.1.3:2446   180.10.1.1:2446     180.10.1.1:2446
---   180.10.1.5         192.168.1.3        ---                 ---
```

## Connectivity Testing

- Initial PC1 ping to 180.10.1.1: 100% packet loss.
- Subsequent PC1 ping to 180.10.1.1: 5 replies, 0% packet loss.
- PC3 ping to 180.10.1.1: 5 replies, 0% packet loss.
- Router4 NAT translation output confirmed a dynamic mapping for 192.168.1.3.

## Results

Dynamic NAT was configured using ACL 2 and a pool of 11 IPv4 addresses.

The NAT table confirmed that 192.168.1.3 was translated to 180.10.1.5. Successful ICMP connectivity was also demonstrated.

## Key Learning Outcomes

- Configure Dynamic NAT without overload.
- Identify inside and outside NAT interfaces.
- Define eligible source networks using a standard ACL.
- Create and associate a NAT address pool.
- Verify NAT translations and test end-to-end connectivity.

## Evidence

See the screenshots uploaded in this folder for the Router4 configuration, NAT translation table, and PC1/PC3 ping tests.
  
