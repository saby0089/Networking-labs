
# 📌 Project Overview

---

# 🌍 Enterprise Multi-Site Network using FortiGate IPSec VPN, OSPF & Zabbix

This project demonstrates the design, deployment, and troubleshooting of a secure **multi-site enterprise network** connecting a **Main Site (Singapore)** and a **Branch Site (India)** through a **FortiGate Route-Based IPSec Site-to-Site VPN**.

A separate **Monitoring Site (Vietnam)** hosts a centralized **Zabbix Server**, providing continuous SNMP monitoring of both FortiGate firewalls and VPN tunnel health.

The entire environment was designed and implemented in **GNS3** to closely simulate a real enterprise network, integrating routing, switching, firewall security, Linux services, Internet connectivity, and infrastructure monitoring.

---

# 🎯 Project Objectives

The primary objectives of this project were to:

- Design a hierarchical enterprise campus network
- Deploy Layer-2 and Layer-3 switching
- Implement VLAN segmentation
- Configure Inter-VLAN Routing
- Configure OSPF dynamic routing
- Build redundant routing paths within each site
- Deploy Route-Based IPSec VPN using FortiGate firewalls
- Exchange enterprise routes securely across the VPN
- Configure Ubuntu DHCP servers
- Deploy BIND9 DNS servers
- Provide Internet access through the FortiGate firewall
- Monitor enterprise infrastructure using Zabbix
- Monitor VPN tunnel availability through SNMP
- Perform end-to-end verification and troubleshooting

---

# 🏢 Enterprise Architecture

The lab consists of three logical locations.

## 🇸🇬 Main Site (Singapore)

The primary enterprise site contains:

- Layer-2 Access Switches
- Layer-3 Distribution Switches
- Cisco Routers
- Redundant Router
- FortiGate Firewall
- Ubuntu DHCP/DNS Server
- Multiple Windows and Linux clients

---

## 🇮🇳 Branch Site (India)

The branch office mirrors the primary site and contains:

- Layer-2 Access Switches
- Layer-3 Distribution Switches
- Cisco Routers
- Redundant Router
- FortiGate Firewall
- Ubuntu DHCP/DNS Server
- Multiple Windows and Linux clients

---

## 🇻🇳 Monitoring Site (Vietnam)

A dedicated monitoring network hosts:

- Zabbix Server
- SNMP Monitoring
- VPN Tunnel Monitoring
- Performance Dashboards
- Alerting Infrastructure

---

# 🖥️ Technologies Used

| Technology | Purpose |
|------------|---------|
| FortiGate Firewall | IPSec VPN, Firewall Policies, NAT |
| Cisco Routers | OSPF Dynamic Routing |
| Cisco Layer-3 Switches | Inter-VLAN Routing |
| Cisco Layer-2 Switches | Access Layer Switching |
| Ubuntu Server | DHCP & DNS (BIND9) |
| Zabbix 7.x | Infrastructure Monitoring |
| SNMP | Network Monitoring |
| GNS3 | Enterprise Lab Simulation |
| Linux | Server Administration |

---

# 🌐 Major Features

✅ Hierarchical Campus Network

✅ Layer-2 Switching

✅ Layer-3 Switching

✅ VLAN Segmentation

✅ Inter-VLAN Routing

✅ OSPF Dynamic Routing

✅ Redundant Internal Routing

✅ Route-Based IPSec VPN

✅ Secure Firewall Policies

✅ Ubuntu DHCP Server

✅ BIND9 DNS Server

✅ Internet Access via FortiGate NAT

✅ Centralized Zabbix Monitoring

✅ SNMP Monitoring

✅ VPN Tunnel Monitoring

✅ Enterprise Troubleshooting Documentation

---

# 🛠 Skills Demonstrated

This project demonstrates hands-on experience with:

- Enterprise Network Design
- Campus LAN Architecture
- Layer-2 Switching
- Layer-3 Switching
- VLAN Design
- Inter-VLAN Routing
- OSPF Configuration & Troubleshooting
- Route Redistribution
- FortiGate Firewall Administration
- IPSec VPN Deployment
- Firewall Policy Configuration
- NAT Configuration
- Linux Server Administration
- DHCP Configuration
- BIND9 DNS Administration
- SNMP Monitoring
- Zabbix Monitoring
- VPN Monitoring
- Enterprise Troubleshooting
- Technical Documentation

---

# 📷 Project Components

The repository documents every stage of the deployment, including:

- Network Topology
- IP Addressing Plan
- OSPF Configuration
- FortiGate IPSec VPN Configuration
- Firewall Policies
- Static Routes
- Route Redistribution
- DHCP Configuration
- DNS Configuration
- Internet Connectivity
- Zabbix Monitoring
- End-to-End Verification
- Real Troubleshooting Scenarios
