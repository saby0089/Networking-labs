# ⚙️ Configuration Guide

This document contains all major configurations used in the Enterprise Hospital Network project.

---

# 🟢 1. VLAN Configuration (All Switches)

```bash
vlan 10
 name RECEPTION
vlan 20
 name DOCTOR
vlan 30
 name NURSE
vlan 40
 name ADMIN
vlan 50
 name BILLING
vlan 60
 name STAFF_WIFI
vlan 70
 name GUEST_WIFI
```

---

# 🟢 2. Access Port Configuration

```bash
interface range fa0/1-5
switchport mode access
switchport access vlan 10

interface range fa0/1-4
switchport mode access
switchport access vlan 20

interface range fa0/1-5
switchport mode access
switchport access vlan 30

interface range fa0/1-5
switchport mode access
switchport access vlan 40

interface range fa0/4-6
switchport mode access
switchport access vlan 50
```

---

# 🟢 3. Trunk Configuration

```bash
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50,60,70
```

---

# 🟢 4. EtherChannel Configuration

## 🔹 L2 EtherChannel (Access ↔ Distribution)

```bash
interface range g0/1-2
channel-group 1 mode active

interface port-channel 1
switchport mode trunk
```

---

## 🔹 L3 EtherChannel (Distribution ↔ Core)

```bash
interface range g1/0/1-2
no switchport
channel-group 110 mode active

interface port-channel110
no switchport
ip address 192.168.1.2 255.255.255.0
```

---

# 🟢 5. Inter-VLAN Routing (SVI)

```bash
interface vlan 10
ip address 10.10.10.1 255.255.255.0
no shutdown

interface vlan 20
ip address 10.20.20.1 255.255.255.0
no shutdown

interface vlan 30
ip address 10.30.30.1 255.255.255.0
no shutdown

interface vlan 40
ip address 10.40.40.1 255.255.255.0
no shutdown

interface vlan 50
ip address 10.50.50.1 255.255.255.0
no shutdown

interface vlan 60
ip address 10.60.60.1 255.255.255.0
no shutdown

interface vlan 70
ip address 10.70.70.1 255.255.255.0
no shutdown
```

---

# 🟢 6. Enable Routing

```bash
ip routing
```

---

# 🟢 7. OSPF Configuration

```bash
router ospf 1
network 10.0.0.0 0.255.255.255 area 0
```

---

# 🟢 8. Edge Router Configuration

## 🔹 LAN Interface

```bash
interface g0/0/0
ip address 192.168.100.1 255.255.255.0
no shutdown
```

---

## 🔹 Serial WAN Link

```bash
interface s0/1/0
ip address 200.1.1.1 255.255.255.252
clock rate 64000
no shutdown
```

---

## 🔹 Default Route

```bash
ip route 0.0.0.0 0.0.0.0 200.1.1.2
```

---

# 🟢 9. ISP Configuration

```bash
interface s0/3/0
ip address 200.1.1.2 255.255.255.252
no shutdown

ip route 10.0.0.0 255.0.0.0 200.1.1.1
```

---

# 🟢 10. Port Security

```bash
interface range fa0/1-24
switchport mode access
switchport port-security
switchport port-security maximum 2
switchport port-security violation restrict
```

---

# 🟢 11. Wireless Configuration (AP)

* SSID: Staff WiFi / Guest WiFi
* Security: WPA2-PSK
* Connected to Access VLAN

---

# 🟢 12. DHCP Server

* Multiple pools configured per VLAN
* Default gateway = 10.60.60.1
* DNS server configured

---

# 🟢 13. DNS Server

* Domain:

```
www.hospital.local
```

* Points to Web Server IP

---

# 🟢 14. Web Server

* HTTP service enabled
* Tested via browser

---

# ✅ Summary

This configuration enables:

* VLAN segmentation
* Routing
* Redundancy
* Wireless connectivity
* WAN access

---

