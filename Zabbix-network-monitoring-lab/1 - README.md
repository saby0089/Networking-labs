# Zabbix Network Monitoring Lab

![Topology](2%20-%20topology/topology.png)

---

# 📌 Project Overview

This project demonstrates the deployment and operation of a centralized monitoring solution using **Zabbix 7.x**.

The objective was to build a monitoring platform capable of monitoring Linux servers, Windows endpoints, Cisco devices, and MikroTik routers using a combination of:

* Zabbix Agents
* SNMP Monitoring
* PSK Encryption
* Email Alerting
* Network Maps
* Custom Administrative Scripts

The lab was built entirely in GNS3 using virtualized infrastructure components to simulate a real-world enterprise monitoring environment.

---

# 🏗️ Lab Architecture

## Monitoring Server

| Component           | Technology    |
| ------------------- | ------------- |
| Monitoring Platform | Zabbix 7.x    |
| Operating System    | Ubuntu Server |
| Database            | MariaDB       |
| Web Server          | Nginx         |

---

## Monitored Devices

| Device            | Monitoring Method     |
| ----------------- | --------------------- |
| Ubuntu Server     | Zabbix Agent (Active) |
| Windows 10        | Zabbix Agent          |
| Cisco Switch      | SNMPv2                |
| MikroTik RouterOS | SNMPv2                |

---

# 🚀 Features Implemented

## Agent Monitoring

✔ Linux Passive Agent

✔ Linux Active Agent

✔ Windows Agent Monitoring

✔ Agent Availability Monitoring

✔ CPU Monitoring

✔ Memory Monitoring

✔ Disk Monitoring

✔ Network Interface Monitoring

---

## Secure Monitoring

✔ PSK Encryption

✔ Secure Agent Authentication

✔ Encrypted Agent Communication

✔ TLS Identity Configuration

---

## SNMP Monitoring

✔ Cisco Device Monitoring

✔ MikroTik Router Monitoring

✔ Interface Discovery

✔ Performance Monitoring

✔ SNMP Validation using snmpwalk

---

## Alerting

✔ Trigger Configuration

✔ User Media Configuration

✔ MailHog Email Integration

✔ Alert Testing

✔ Problem Notifications

✔ Recovery Notifications

---

## Automation and Administrative Scripts

✔ Ping Script

✔ Traceroute Script

✔ Operating System Detection (Nmap)

✔ Memory Utilization Script

✔ Network Map Actions

---

## Visualization

✔ Custom Dashboards

✔ Network Maps

✔ Host Status Visualization

✔ Interactive Actions

---

# ⚙️ Configuration Sections

Detailed implementation steps are documented in:

| Section           | Description                            |
| ----------------- | -------------------------------------- |
| 5 - zabbix-agents | Active and Passive Agent Configuration |
| 6 - security      | PSK Encryption Implementation          |
| 7 - alerting      | MailHog Alerting Configuration         |
| 4 - configs       | Configuration Backups                  |
| 3 - screenshots   | Validation Screenshots                 |

---

# 🔍 Verification Performed

The following validation tests were successfully completed:

### Agent Monitoring

* Verified Linux Agent connectivity
* Verified Windows Agent connectivity
* Confirmed Active Agent operation
* Confirmed Passive Agent operation

### SNMP Monitoring

* SNMP Walk Verification
* Cisco Monitoring Validation
* MikroTik Monitoring Validation

### Alerting

* Trigger Generation
* Email Notification Delivery
* Recovery Notification Testing

### Administrative Scripts

* Ping Execution
* Traceroute Execution
* Nmap OS Detection
* Memory Usage Verification

---

# 🛠️ Challenges Encountered

During implementation several issues were identified and resolved:

* Zabbix Agent communication failures
* PSK authentication mismatches
* SNMP monitoring issues
* Missing Nmap dependency
* Missing Traceroute dependency
* Script execution permission errors
* Host onboarding issues
* Manual action execution failures

---

# 📚 Key Skills Demonstrated

### Monitoring

* Zabbix Administration
* Agent Deployment
* Active Monitoring
* Passive Monitoring

### Networking

* SNMP
* ICMP
* TCP/IP
* Network Device Monitoring

### Security

* PSK Encryption
* TLS Authentication
* Secure Monitoring

### Linux Administration

* Ubuntu Server
* Service Management
* Package Management
* Troubleshooting

---

# 🎯 Future Improvements

* SNMPv3 Monitoring
* Custom Templates
* Low-Level Discovery
* Zabbix Proxy
* Grafana Integration
* Advanced Trigger Logic

---

# 👨‍💻 Author

**Sabyasachi Dasgupta**

CCNA Certified | Network Monitoring | Zabbix | SNMP | Linux | Infrastructure Monitoring

