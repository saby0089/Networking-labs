
# ⚙️ Configuration Guide

This document provides step-by-step configuration of key components used in the enterprise network.

---

## 🔁 HSRP Configuration (Gateway Redundancy)

### Example (VLAN 10)

#### Dist-SW1 (Primary)
```bash
interface vlan 10
ip address 192.168.100.1 255.255.255.192
standby 10 ip 192.168.100.3
standby 10 priority 110
standby 10 preempt
```
#### Dist-SW2 (Secondary)
```bash
interface vlan 10
ip address 192.168.100.2 255.255.255.192
standby 10 ip 192.168.100.3
standby 10 priority 100
standby 10 preempt
```

👉 Repeat for all VLANs

---

## 🔗 EtherChannel Configuration

### Office (LACP)
```bash
interface range g0/1 - 2
channel-group 1 mode active
switchport mode trunk
```
---

### Admin (PAgP)
```bash
interface range g0/1 - 2
channel-group 1 mode desirable
switchport mode trunk
```

---

## 🌐 OSPF Configuration
```bash
router ospf 1
network 192.168.0.0 0.0.255.255 area 0
network 172.16.1.0 0.0.0.3 area 0
```

---

## 🌍 GRE Tunnel Configuration

### Office Router
```bash
interface tunnel0
ip address 172.16.1.1 255.255.255.252
tunnel source s0/0/0
tunnel destination 10.0.1.2
```

### Admin Router
```bash
interface tunnel0
ip address 172.16.1.2 255.255.255.252
tunnel source s0/0/0
tunnel destination 10.0.1.1
```

---

## 🌐 NAT Configuration (PAT)
```bash
access-list 100 permit ip 192.168.0.0 0.0.255.255

interface g0/0
ip nat inside

interface s0/0/1
ip nat outside

ip nat inside source list 100 interface s0/0/1 overload
```

---

## 🖥️ DHCP Configuration (Server Side)

- DHCP Server IP: 192.168.102.66

Example Pool:
```bash
Network: 192.168.100.0
Gateway: 192.168.102.71 (HSRP VIP)
DNS: 192.168.102.67
```

---

## 🔁 DHCP Relay (on SVIs)
```bash
interface vlan 10
ip helper-address 192.168.102.66
```

---

## 🌐 DNS Configuration

- Domain: sabycompany.com

Records:
```bash
web.sabycompany.com → 192.168.102.69
mail.sabycompany.com → 192.168.102.68
```

---

## 📧 Email Server Configuration

- Domain: sabycompany.com

Users:
```bash
saby / 123
admin / 123
```

---

## 🌍 Web Server Configuration

- HTTP: ON

Example HTML:
Welcome to Saby Enterprise Network 🚀

---

## 📡 Wireless Configuration

- SSID: SabyWiFi
- Security: WPA2
- VLAN mapping via access ports

---
