# Configuration Details

## R1 (HQ Router)

### WAN Interface

* IP: 10.10.10.1/30

### VLAN Interfaces

* VLAN 10: 192.168.10.1
* VLAN 20: 192.168.20.1
* VLAN 30: 192.168.30.1

### NAT Configuration

* Inside: VLAN interfaces + Serial interface
* Outside: Internet-facing interface

### Routing

* OSPF configured for HQ and Branch networks
* Default route to ISP

---

## R2 (Branch Router)

### WAN Interface

* IP: 10.10.10.2/30

### LAN Interface

* Network: 192.168.40.0/24

### Routing

* OSPF for internal routing
* Default route towards R1

---

## Switch Configuration

### SW1 (HQ)

* VLANs: 10, 20, 30
* Trunk to R1
* Access ports assigned to respective VLANs

### SW2 (Branch)

* Single VLAN for branch users

