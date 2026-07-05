---

# 🌐 Enterprise Multi-Site Network Infrastructure using FortiGate, IPSec VPN, OSPF, Ubuntu Services & Zabbix Monitoring

---

# Topology
![Topology](topology.png)

---

# 📌 Project Overview

This project demonstrates the design, deployment, monitoring, and troubleshooting of a complete enterprise network consisting of two geographically separated branch offices connected through a **FortiGate Route-Based IPSec Site-to-Site VPN**.

Each site provides dynamic routing using **OSPF**, local infrastructure services through **Ubuntu DHCP** and **BIND9 DNS**, secure communication over an encrypted IPSec tunnel, Internet connectivity via NAT, and centralized monitoring using **Zabbix**.

Unlike traditional networking labs that stop after configuration, this project focuses on the complete engineering lifecycle—from deployment and validation to troubleshooting and performance monitoring.

The entire environment was designed and implemented inside **GNS3** using virtualized Cisco routers, FortiGate firewalls, Ubuntu Linux servers, and a dedicated Zabbix monitoring platform to simulate a real-world enterprise branch network.

---

# 🏗️ Lab Architecture

## Enterprise Infrastructure

| Component | Purpose |
|-----------|----------|
| Cisco Layer-3 Routers | Dynamic Routing (OSPF) |
| FortiGate Firewalls | IPSec VPN & Firewall Policies |
| Ubuntu Linux Server | DHCP Server |
| Ubuntu Linux Server | BIND9 DNS Server |
| Zabbix Server | Infrastructure Monitoring |
| Client PCs | End User Simulation |
| NAT Cloud | Internet Connectivity |

---

## 🌍 Site 1

| Component | Function |
|----------|----------|
| Cisco Router | OSPF Routing |
| FortiGate Firewall | VPN Gateway |
| Ubuntu DHCP/DNS Server | Infrastructure Services |
| PCs | Client Devices |

---

## 🌍 Site 2

| Component | Function |
|----------|----------|
| Cisco Router | OSPF Routing |
| FortiGate Firewall | VPN Gateway |
| Ubuntu DHCP/DNS Server | Infrastructure Services |
| PCs | Client Devices |

---

## 📊 Monitoring Infrastructure

The environment includes a dedicated **Zabbix Server** responsible for monitoring both FortiGate firewalls using SNMP.

Current monitoring includes:

- VPN Tunnel Status
- CPU Utilization
- Memory Usage
- Interface Statistics
- Firewall Health
- Availability Monitoring

---

# 🎯 Project Objectives

The primary objective of this project was to build a realistic enterprise branch-office network capable of demonstrating modern networking, security, infrastructure services, and monitoring technologies.

Key objectives include:

- Configure Dynamic Routing using OSPF
- Deploy Route-Based IPSec VPN
- Secure Inter-Site Communication
- Configure DHCP Services
- Configure BIND9 DNS
- Implement Internet Access using NAT
- Monitor Infrastructure using Zabbix
- Validate End-to-End Connectivity
- Perform Real-World Troubleshooting
- Document Complete Deployment Process

---

# 🚀 Technologies Used

| Technology | Purpose |
|------------|---------|
| FortiGate VM | Firewall & IPSec VPN |
| Cisco IOS | Enterprise Routing |
| OSPF | Dynamic Routing |
| IPSec | Secure Site-to-Site VPN |
| Ubuntu Linux | Infrastructure Services |
| BIND9 | DNS Server |
| ISC DHCP | DHCP Server |
| Zabbix 7 | Enterprise Monitoring |
| SNMP | Network Monitoring |
| NAT | Internet Access |
| GNS3 | Network Emulation |

---

# ⭐ Project Features

✅ Enterprise Dual-Site Network

✅ Dynamic Routing (OSPF)

✅ Route-Based IPSec VPN

✅ Route Redistribution

✅ Ubuntu DHCP Server

✅ Ubuntu BIND9 DNS Server

✅ Internet Connectivity

✅ NAT Configuration

✅ DNS Forwarding

✅ Secure Inter-Site Communication

✅ Zabbix SNMP Monitoring

✅ VPN Tunnel Monitoring

✅ Infrastructure Health Monitoring

✅ End-to-End Validation

✅ Enterprise Troubleshooting

---

# 💼 Skills Demonstrated

This project demonstrates practical experience in:

- Enterprise Routing
- OSPF Design
- IPSec VPN Deployment
- FortiGate Administration
- Firewall Policy Configuration
- Linux Administration
- DHCP Configuration
- DNS Configuration
- NAT
- SNMP
- Zabbix Monitoring
- Network Troubleshooting
- Root Cause Analysis
- Technical Documentation

---

# 📖 Why This Project?

Most networking labs focus only on successful configuration.

This repository intentionally documents the complete engineering journey, including configuration, validation, troubleshooting, and final optimization.

Throughout the implementation, multiple real-world networking issues involving routing, VPN connectivity, DNS resolution, Linux services, Internet access, and monitoring were investigated and resolved using structured troubleshooting techniques.

This makes the project representative of day-to-day enterprise network engineering rather than a simple configuration exercise.

---
