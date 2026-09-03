# CCNP VLAN Lab

## Lab Objective

Configure and verify VLANs, access VLAN assignments, voice VLANs, and Dynamic Trunking Protocol (DTP) behavior on a Cisco switch.

## Topics Covered
- VLAN creation
- VLAN naming
- Access ports
- Acess vs Voice VLANs
- Allowed VLANs
- VLAN verification
- Troubleshooting


## VLAN Table

| VLAN | Name |
|------|---------|
| 10 | HR |
| 20 | FINANCE |
| 30 | IT |
| 200 | VOICE |

## 1. Create VLANs

```cisco
enable
configure terminal

vlan 10
 name HR

vlan 20
 name FINANCE

vlan 30
 name IT

vlan 200
 name VOICE

exit
```

## 2. Verify VLAN Creation

```cisco
show vlan brief
```

Because I was working from global configuration mode, I also used:

```cisco
do show vlan brief
```

The verification showed VLANs 10, 20, 30, and 200 active on the switch.

## 3. Assign Access VLANs

### GigabitEthernet1/0/1 — HR

```cisco
interface GigabitEthernet1/0/1
 switchport access vlan 10
exit
```

### GigabitEthernet1/0/2 — FINANCE

```cisco
interface GigabitEthernet1/0/2
 switchport access vlan 20
exit
```

### GigabitEthernet1/0/3 — IT

```cisco
interface GigabitEthernet1/0/3
 switchport access vlan 30
exit
```

## 4. Configure Voice VLAN

Configure Voice VLAN 200 on ports Gi1/0/4 through Gi1/0/20:

```cisco
interface range GigabitEthernet1/0/4-20
 switchport voice vlan 200
exit
```

Voice VLAN 200 was also configured on the first three access interfaces:

```cisco
interface GigabitEthernet1/0/1
 switchport voice vlan 200
exit

interface GigabitEthernet1/0/2
 switchport voice vlan 200
exit

interface GigabitEthernet1/0/3
 switchport voice vlan 200
exit
```

## 5. Verify VLAN Assignments

```cisco
show vlan brief
```

From configuration mode:

```cisco
do show vlan brief
```

Verification showed:

- Gi1/0/1 assigned to VLAN 10 (HR)
- Gi1/0/2 assigned to VLAN 20 (FINANCE)
- Gi1/0/3 assigned to VLAN 30 (IT)
- Gi1/0/4 through Gi1/0/20 associated with Voice VLAN 200

## 6. Verify Individual Switchports

### Gi1/0/1

```cisco
show interfaces GigabitEthernet1/0/1 switchport
```

Observed:

```text
Access Mode VLAN: 10 (HR)
Voice VLAN: 200 (VOICE)
Trunking Native Mode VLAN: 1 (default)
```

### Gi1/0/2

```cisco
show interfaces GigabitEthernet1/0/2 switchport
```

Observed:

```text
Access Mode VLAN: 20 (FINANCE)
Voice VLAN: 200 (VOICE)
Trunking Native Mode VLAN: 1 (default)
```

### Gi1/0/3

```cisco
show interfaces GigabitEthernet1/0/3 switchport
```

Observed:

```text
Access Mode VLAN: 30 (IT)
Voice VLAN: 200 (VOICE)
Trunking Native Mode VLAN: 1 (default)
```

## 7. Verify Running Configuration

```cisco
show running-config interface GigabitEthernet1/0/1
show running-config interface GigabitEthernet1/0/2
show running-config interface GigabitEthernet1/0/3
```

The configuration confirmed:

```cisco
interface GigabitEthernet1/0/1
 switchport access vlan 10
 switchport voice vlan 200
 spanning-tree portfast

interface GigabitEthernet1/0/2
 switchport access vlan 20
 switchport voice vlan 200
 spanning-tree portfast

interface GigabitEthernet1/0/3
 switchport access vlan 30
 switchport voice vlan 200
 spanning-tree portfast
```

## 8. DTP / Dynamic Desirable Testing

Gi1/0/1 initially showed:

```text
Administrative Mode: dynamic auto
Negotiation of Trunking: On
```

The interface was changed to dynamic desirable:

```cisco
interface GigabitEthernet1/0/1
 switchport mode dynamic desirable
exit
```

Verification:

```cisco
show interfaces GigabitEthernet1/0/1 switchport
```

The output showed:

```text
Administrative Mode: dynamic desirable
Negotiation of Trunking: On
Access Mode VLAN: 10 (HR)
Voice VLAN: 200 (VOICE)
```

## Useful Verification Commands

```cisco
show vlan brief
show interfaces trunk
show interfaces switchport
show interfaces GigabitEthernet1/0/1 switchport
show interfaces GigabitEthernet1/0/2 switchport
show interfaces GigabitEthernet1/0/3 switchport
show running-config
```

## Troubleshooting Note

While configuring the interface range, this command was attempted:

```cisco
interface GigabitEthernet1/0/4-20
```

It returned an invalid input error because the `range` keyword was missing.

The correct command is:

```cisco
interface range GigabitEthernet1/0/4-20
```

This was corrected successfully.

## What I Learned

In this lab I practiced:

- Creating and naming VLANs
- Assigning access VLANs to switchports
- Configuring a voice VLAN
- Using interface ranges
- Verifying VLAN membership
- Verifying switchport parameters
- Checking interface running configurations
- Understanding native VLAN information
- Working with DTP dynamic auto and dynamic desirable modes
- Troubleshooting Cisco IOS command syntax
