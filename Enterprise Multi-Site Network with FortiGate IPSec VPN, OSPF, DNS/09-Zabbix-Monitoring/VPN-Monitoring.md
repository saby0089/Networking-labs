
# 🔐 IPSec VPN Monitoring

---

# 📌 Objective

The objective of this phase was to continuously monitor the operational status of the IPSec Site-to-Site VPN using Zabbix.

Monitoring the VPN ensures that administrators can quickly identify tunnel failures and verify that secure communication between enterprise sites remains available.

---

# 🌐 Monitoring Design

The Zabbix server monitors:

- Active VPN Tunnel Count
- Tunnel Availability
- Tunnel Health
- Historical Tunnel Status

Monitoring is performed through SNMP polling of both FortiGate firewalls.

---

# 📈 Verification

VPN monitoring was validated by:

- Tunnel status showing Active
- Historical graphs updating
- Continuous SNMP polling
- Stable tunnel availability

---

# 📷 Screenshots

- Active IPSec Tunnel Graph
  ![Screenshot](../Images/zabbix-vpn-graph.png)

---

# 📖 Notes

Continuous monitoring allows administrators to detect VPN outages immediately and provides historical visibility into tunnel stability.

This improves operational awareness and simplifies enterprise network management.
