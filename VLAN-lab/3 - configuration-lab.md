# VLAN Configuration Lab

## Objective
Configure VLANs on a switch and assign access ports to different VLANs to segment the network. 

## Topology
The topology consists of :
- 1 router
- 2 switches
- 4 PCs
- Each PC is connected to different switch ports

## Refer to the topology diagram below:
![Network Topology](2%20-%20topology.png)

## Devices Used
| Device | Role |
|------|------|
| R1 | Router for inter-VLAN routing |
| SW1 | Access switch |
| SW2 | Access switch |
| PC1 | Host in VLAN 13 |
| PC2 | Host in VLAN 24 |
| PC3 | Host in VLAN 13 |
| PC4 | Host in VLAN 24 |

## IP Addressing
| Device | IP Address | VLAN |
|------|------|------|
| PC1 | 10.0.0.11/24 | VLAN 13 |
| PC2 | 10.0.1.12/24 | VLAN 24 |
| PC3 | 10.0.0.13/24 | VLAN 13 |
| PC4 | 10.0.1.14/24 | VLAN 24 |

## Gateway:
VLAN13 → 10.0.0.1
VLAN24 → 10.0.1.1

---

# Configuration Steps
## 1 Configure Hostnames
R1(config)# hostname R1
SW1(config)# hostname SW1
SW2(config)# hostname SW2

## 2 Configure Enable Secret
enable secret SABY - Configured on all networking devices.

## 3 Create VLANs
On both switches:

SW(config)# vlan 13
SW(config-vlan)# name VLAN13

SW(config)# vlan 24
SW(config-vlan)# name VLAN24

## 4 Configure Access Ports
Example on SW1:

interface f0/2
switchport mode access
switchport access vlan 13

interface f0/3
switchport mode access
switchport access vlan 24

## 5 Configure Trunk Between SW1 and SW2
First identify interfaces using CDP:

show cdp neighbors

Then configure trunk:

interface f0/1
switchport mode trunk

## 6 Configure Port Security
interface f0/2
switchport mode access
switchport port-security
switchport port-security mac-address sticky
switchport port-security violation restrict

## 7 Configure Router-on-a-Stick
interface g0/0.13
encapsulation dot1Q 13
ip address 10.0.0.1 255.255.255.0

interface g0/0.24
encapsulation dot1Q 24
ip address 10.0.1.1 255.255.255.0

---

## 8 Verification

Check VLANs:
show vlan brief

Check trunk:
show interfaces trunk

Check port security:
show port-security interface f0/2

Test connectivity:
ping between PCs

All hosts successfully communicated across VLANs.
