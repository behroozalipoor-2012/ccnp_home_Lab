# CCNP Spanning Tree - MST Lab

## Topics Covered

- Multiple Spanning Tree (MST)
- MST region configuration
- MST revision number
- VLAN-to-MST instance mapping
- Root bridge configuration
- Primary and secondary root bridges
- Root, designated, and alternate port roles
- Forwarding and blocking states
- MST verification and troubleshooting

## MST Configuration

### MST Region

```cisco
spanning-tree mode mst
spanning-tree mst configuration
 name group1
 revision 1
 instance 1 vlan 1-3
 instance 2 vlan 4-6
 exit
