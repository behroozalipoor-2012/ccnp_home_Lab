# GLBP Authentication Lab

## Objective

Configure and verify GLBP authentication between multiple routers while maintaining gateway redundancy and load balancing.

## Lab Overview

This lab builds on the previous GLBP configuration by adding authentication to GLBP Group 10.

Three routers participate in the GLBP group:

- R1
- R2
- R3

GLBP virtual IP:

    10.10.10.25

GLBP Group:

    10

Load-balancing method:

    round-robin

## Initial GLBP Configuration

Example configuration on R1:

    interface Ethernet0/3
     glbp 10 ip 10.10.10.25
     glbp 10 priority 110
     glbp 10 preempt

R1 is configured with the higher GLBP priority of 110.

R2 and R3 use the default priority of 100.

## Plain-Text Authentication

GLBP authentication was first tested using plain-text authentication.

Example:

    interface Ethernet0/3
     glbp 10 authentication text my80$0nL485

The same authentication string must be configured on every router participating in the GLBP group.

## Authentication Mismatch Troubleshooting

When authentication was configured only on one router, GLBP generated authentication errors such as:

    %GLBP-4-BADAUTH: Bad authentication received

This happened because the GLBP authentication configuration did not match between the routers.

This demonstrated that GLBP neighbors must use matching authentication settings before they can successfully participate in the same GLBP group.

## Verification

GLBP operation was verified using:

    show glbp
    show glbp brief

After matching authentication was configured, the GLBP output showed the other group members as authenticated.

Example:

    10.10.10.2 authenticated
    10.10.10.3 authenticated

## MD5 Authentication

The lab also tested GLBP MD5 authentication.

The verification output showed:

    Authentication MD5, key-string

This confirms that GLBP authentication can also be configured using MD5 instead of plain text.

## GLBP Roles

The lab demonstrated:

- Active Virtual Gateway
- Standby GLBP router
- Active Virtual Forwarders
- Multiple GLBP virtual MAC addresses
- Priority-based AVG election
- Preemption
- Round-robin load balancing

## Connectivity Testing

PC connectivity was verified using traceroute to:

    203.0.113.56

Traffic was successfully forwarded through different GLBP routers including:

    10.10.10.1
    10.10.10.2

This confirmed continued gateway forwarding after authentication was configured.

## Commands Used

    show glbp
    show glbp brief

Example GLBP authentication commands:

    glbp 10 authentication text <password>

and MD5 authentication:

    glbp 10 authentication md5 key-string <password>

## Skills Demonstrated

- GLBP configuration
- GLBP authentication
- Plain-text authentication
- MD5 authentication
- Authentication mismatch troubleshooting
- GLBP AVG and AVF verification
- GLBP priority and preemption
- Round-robin load balancing
- Gateway redundancy
- First-Hop Redundancy Protocol troubleshooting
- Cisco IOS verification commands
