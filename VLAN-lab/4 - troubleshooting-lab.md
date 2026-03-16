
# VLAN & Inter-VLAN Routing Troubleshooting Lab
## Objective

Identify and resolve misconfigurations in a VLAN-based network topology involving two switches and a router.
The goal is to restore full connectivity between all PCs across VLANs.

## Topology
![Topology](2%20-%20topology.png)

## Scenario
The network was previously configured to support VLAN segmentation and inter-VLAN routing using the router-on-a-stick method.
However, several misconfigurations were intentionally introduced on the devices:
- R1
- SW1
- SW2
Each device contained 1–2 configuration errors that prevented full connectivity.
The task was to identify and correct these issues so that all PCs could successfully ping each other, including across VLANs.

## Network Design
| Device | IP Address   | VLAN    |
| ------ | ------------ | ------- |
| PC1    | 10.0.0.11/24 | VLAN 13 |
| PC2    | 10.0.1.12/24 | VLAN 24 |
| PC3    | 10.0.0.13/24 | VLAN 13 |
| PC4    | 10.0.1.14/24 | VLAN 24 |

Gateway configuration:
- VLAN 13 → 10.0.0.1
- VLAN 24 → 10.0.1.1

## Troubleshooting Methodology
The troubleshooting process followed a systematic approach:
1. Verify VLAN configuration on switches.
2. Verify trunk links between switches.
3. Verify router subinterfaces for inter-VLAN routing.
4. Verify port security configuration.
5. Test connectivity between hosts.

## Identified Issues
### Issue 1 – Port Security error
- SW1's interface Fa0/2 was statically configured with a MAC address which is not the MAC address of the connected PC.

Diagnosis:
- show run
- show port-security address

The outputs showed the secure MAC address was not the MAC address of connected PC1.

Fix:
- switchport access vlan 13
- switchport mode access
- switchport port-security
- switchport port-security mac-address sticky 
- switchport port-security violation restrict

### Issue 2 – Trunk Link Misconfiguration and assigning wrong VLAN information on access port
- SW2 trunk link of Fa0/1 connected to SW1 was set to access port
- Access port interface of Fa0/2 was set to wrong Vlan 23 instead of 13.

Diagnosis:
- show run
- show vlan brief
- show interface f0/1 switchport

The outputs showed the wrong VLAN is assigned on an access port and trunk port is misconfigured with access port.

Fix:
- interface FastEthernet0/1
- switchport mode trunk
!
- interface FastEthernet0/2
- switchport mode access
- switchport access vlan 13

### Issue 3 – Router Subinterface Configuration
- Inter-VLAN configuration requires matching subnets and correct VLAN tagging in dot1Q encapsulation.

Diagnosis:
- show run

The output shows the sub-interface was wrongly configured.

Fix:
- interface g0/0.13
- encapsulation dot1Q 13
- ip address 10.0.0.1 255.255.255.0

- interface g0/0.24
- encapsulation dot1Q 24
- ip address 10.0.1.1 255.255.255.0

## Verification
After correcting the misconfigurations, connectivity was verified.

Commands used:
- ping

Test results:
1. PC1 ↔ PC3 successful (same VLAN)
2. PC2 ↔ PC4 successful (same VLAN)
3. PC1 ↔ PC2 successful (inter-VLAN)
4. PC3 ↔ PC4 successful (inter-VLAN)

All hosts were able to communicate successfully.
