# Configuration Details

## R1 (HQ Router)

### WAN Interface

* IP: 10.10.10.1/30

### VLAN Interfaces

* VLAN 10: 192.168.10.1
* VLAN 20: 192.168.20.1
* VLAN 30: 192.168.30.1

### 🔸 Interface Configuration
```bash
interface g0/0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```

### NAT Configuration

* Inside: VLAN interfaces + Serial interface
* Outside: Internet-facing interface
  
```bash
access-list 1 permit 192.168.0.0 0.0.255.255

interface g0/1/0
ip nat outside

interface s0/2/0
ip nat inside

ip nat inside source list 1 interface g0/0/1 overload
```

### Routing

* OSPF configured for HQ and Branch networks
* Default route to ISP

```bash
router ospf 1
network 192.168.0.0 0.0.255.255 area 0
network 10.10.10.0 0.0.0.3 area 0
```
---

## R2 (Branch Router)

### WAN Interface

* IP: 10.10.10.2/30

### LAN Interface

* Network: 192.168.40.0/24

### 🔸 Interface Configuration

```bash
interface g0/0/0
ip address 192.168.40.1 255.255.255.0
```

### Routing

* OSPF for internal routing
* Default route towards R1
  
```bash
ip route 0.0.0.0 0.0.0.0 10.10.10.1
```
---

## Switch Configuration

### SW1 (HQ)

* VLANs: 10, 20, 30
* Trunk to R1
* Access ports assigned to respective VLANs

### 🔸 VLAN Setup

Configuring VLANs on the switch to segment HR and IT networks.

```bash
vlan 10
name HR

vlan 20
name IT

interface fa0/1
switchport mode access
switchport access vlan 10

interface g0/1
switchport mode trunk
```

### SW2 (Branch)

* Single VLAN for branch users

