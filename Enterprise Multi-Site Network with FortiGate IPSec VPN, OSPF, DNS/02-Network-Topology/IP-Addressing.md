
# 🏗️ Network Topology & IP Addressing

---

# 🌐 Network Architecture

The lab simulates a real-world enterprise consisting of two geographically separated sites connected through a secure Route-Based IPSec VPN.

A dedicated monitoring site hosts the Zabbix Server, providing centralized SNMP monitoring of both FortiGate firewalls.

---


---

# 🏢 Site Overview

| Site | Purpose |
|------|---------|
| 🇸🇬 Singapore | Main Enterprise Site |
| 🇮🇳 India | Branch Office |
| 🇻🇳 Vietnam | Centralized Monitoring Site |

---

# 🖥 Main Site Components

- 2 × Layer-2 Access Switches
- 2 × Layer-3 Distribution Switches
- 2 × Cisco Routers
- 1 × FortiGate Firewall
- 1 × Ubuntu DNS/DHCP Server
- Windows Clients
- VPCS Clients

---

# 🖥 Branch Site Components

- 2 × Layer-2 Access Switches
- 2 × Layer-3 Distribution Switches
- 2 × Cisco Routers
- 1 × FortiGate Firewall
- 1 × Ubuntu DNS/DHCP Server
- Windows Clients
- VPCS Clients

---

# 📊 Monitoring Site Components

- Ubuntu Server
- Zabbix Server 7.0.5
- SNMP Monitoring
- VPN Tunnel Monitoring
- Performance Dashboards

---

# 🔐 Enterprise Services

- OSPF Dynamic Routing
- Route-Based IPSec VPN
- DHCP Services
- DNS Services (BIND9)
- Internet Connectivity
- SNMP Monitoring
- Zabbix Monitoring

---

# 📡 VLAN Design

## Main Site

| VLAN | Network | Purpose |
|------|---------|---------|
| 100 | 192.168.100.0/24 | User LAN |
| 111 | 192.168.50.0/24 | Server Network |
| 200 | 192.168.200.0/24 | User LAN |

---

## Branch Site

| VLAN | Network | Purpose |
|------|---------|---------|
| 300 | 192.168.30.0/24 | User LAN |
| 222 | 192.168.60.0/24 | Server Network |
| 400 | 192.168.40.0/24 | User LAN |

---

# 🔗 VPN Information

| Parameter | Value |
|-----------|-------|
| VPN Type | Route-Based IPSec |
| Tunnel Network | 90.90.90.0/30 |
| Phase 1 | IKEv1 |
| Authentication | Pre-Shared Key |
| Routing | Static + OSPF |

---

# 🌍 Internet Connectivity

The FortiGate firewalls provide Internet connectivity for internal users through Source NAT (PAT).

Both enterprise sites can:

- Access Internet resources
- Resolve public DNS records
- Communicate securely across the IPSec VPN

---

# 📈 Monitoring Architecture

The Zabbix Server monitors:

- FortiGate Site 1
- FortiGate Site 2
- IPSec VPN Tunnel Status
- CPU Utilization
- Memory Utilization
- Interface Traffic
- VPN Availability
- SNMP Health

---

# 🛠 Network Design Highlights

✔ Hierarchical Campus Design

✔ Layer-2 Access Layer

✔ Layer-3 Distribution Layer

✔ Dynamic Routing using OSPF

✔ Secure Site-to-Site VPN

✔ Redundant Internal Routing

✔ Centralized DHCP & DNS

✔ Internet Access

✔ Enterprise Monitoring
