# Zabbix Network Monitoring Lab

![Topology](2%20-%20topology/topology.png)

---

# 📌 Project Overview

This project demonstrates the deployment and operation of a centralized enterprise monitoring platform using **Zabbix 7.0.26**.

The objective was to build a monitoring environment capable of monitoring servers, workstations, network devices, services, and applications while implementing security, alerting, and administrative automation features commonly found in production environments.

The entire lab was built in **GNS3** using virtualized infrastructure components to simulate a real-world enterprise monitoring deployment.

---

# 🏗️ Lab Architecture

## Monitoring Infrastructure

| Component             | Purpose                         |
| --------------------- | ------------------------------- |
| Zabbix Server         | Centralized monitoring platform |
| Ubuntu Linux          | Active Agent Monitoring         |
| Windows 10            | Passive Agent Monitoring        |
| MikroTik RouterOS CHR | SNMP Monitoring                 |
| Cisco Switch          | SNMP Monitoring                 |
| Nginx Web Server      | Service Monitoring              |
| MailHog               | Email Alert Testing             |

---

# ⚙️ Technologies Implemented

## Zabbix Monitoring

* Host Discovery
* Agent-Based Monitoring
* Active Agents
* Passive Agents
* Custom Monitoring Items
* Trigger Creation
* Event Management
* Network Maps
* Dashboard Customization

---

## SNMP Monitoring

Implemented monitoring of network devices using SNMP.

### Monitored Devices

* MikroTik RouterOS CHR
* Cisco Switch

### Features

* Interface Monitoring
* Availability Monitoring
* Device Statistics Collection
* Template-Based Monitoring

---

## Security

Implemented encrypted communication between monitored hosts and the monitoring server.

### Features

* PSK (Pre-Shared Key) Encryption
* Encrypted Agent Communication
* Secure Host Authentication

---

## Alerting & Notifications

Implemented automated event notification workflows.

### Features

* Email Alerting
* Trigger-Based Actions
* User Media Configuration
* Recovery Notifications
* MailHog SMTP Integration

---

## Administrative Automation

Created custom scripts accessible directly from the Zabbix interface.

### Custom Scripts

* Ping Test
* Traceroute
* Operating System Detection
* Disk Space Verification

---

## Web Service Monitoring

Implemented monitoring of web services hosted within the lab.

### Monitored Service

* Nginx Web Server

---

# 🖥️ Software Versions

| Component             | Version       |
| --------------------- | ------------- |
| Zabbix Server         | 7.0.26        |
| Zabbix Agent          | 7.0.26        |
| Ubuntu Linux          | 24.04 LTS     |
| Windows               | Windows 10    |
| MikroTik RouterOS CHR | 7.5           |
| Nginx                 | Latest Stable |
| MailHog               | Latest Stable |

---

# 📸 Project Screenshots

## Zabbix Dashboard

![Dashboard](3%20-%20screenshots/1-%20zabbix-dashboard.png)

## MikroTik SNMP Monitoring

![MikroTik](3%20-%20screenshots/2-%20mikrotik-snmp-monitoring.png)

## Cisco SNMP Monitoring

![Cisco](3%20-%20screenshots/3-%20cisco-snmp-monitoring.png)

## Custom Administrative Scripts

![Scripts](3%20-%20screenshots/4-%20custom-scripts.png)

## Network Map Actions

![Network Map](3%20-%20screenshots/5-%20network-map-actions.png)

## Email Alerting

![Email Alerts](3%20-%20screenshots/6-%20email-alerts.png)

## PSK Encryption

![PSK](3%20-%20screenshots/7-%20psk-encryption.png)

## Active Agent Monitoring

![Active Agent](3%20-%20screenshots/8-%20active-agent.png)

## Passive Agent Monitoring

![Passive Agent](3%20-%20screenshots/9-%20passive-agent.png)

---

# 🔍 Validation Performed

The following tests were successfully completed:

* Agent Connectivity Verification
* SNMP Polling Validation
* PSK Encryption Validation
* Trigger Generation Testing
* Email Alert Testing
* Recovery Notification Testing
* Custom Script Execution
* Network Map Actions
* Web Service Monitoring

---

# 📚 Key Skills Demonstrated

* Network Monitoring
* Zabbix Administration
* Linux Administration
* SNMP Monitoring
* Alert Management
* Infrastructure Security
* Troubleshooting
* Service Monitoring
* Network Visibility
* Monitoring Automation

---

# 🎯 Outcome

This lab demonstrates the deployment of a secure enterprise monitoring solution capable of monitoring servers, endpoints, network devices, and services while providing centralized visibility, automated alerting, encrypted communications, and operational troubleshooting tools.

# 🎯 Future Improvements

* SNMPv3 Monitoring
* Custom Templates
* Low-Level Discovery
* Zabbix Proxy
* Grafana Integration
* Advanced Trigger Logic
  
# 👨‍💻 Author

### Sabyasachi Dasgupta
