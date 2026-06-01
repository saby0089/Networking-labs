# PSK Encryption Verification

## Overview

After configuring PSK encryption on both the Zabbix Server and Windows 10 Agent, verification was performed to confirm successful encrypted communication.

---

## Host Availability Check

Navigate to:

```text
Monitoring → Hosts
```

Verify that the monitored Windows host displays:

```text
ZBX Available (Green)
```

A green status indicates successful communication between the server and agent.

---

## Latest Data Verification

Navigate to:

```text
Monitoring → Latest Data
```

Select the Windows host and verify that metrics are being collected.

Examples:

* CPU Utilization
* Memory Usage
* Disk Space
* Network Traffic
* System Uptime

Expected Result:

```text
Recent timestamps continue updating
```

---

## Agent Log Verification

Open the Windows Agent log:

```text
C:\Program Files\Zabbix Agent 2\zabbix_agent2.log
```

Confirm that no TLS-related errors are present.

Expected Result:

```text
No TLS handshake failures
No authentication errors
```

---

## Server-Side Verification

On the Zabbix Server:

```bash
tail -f /var/log/zabbix/zabbix_server.log
```

Monitor the log while the host communicates with the server.

Expected Result:

```text
No PSK mismatch errors
No TLS negotiation failures
```

---

## Functional Test

Restart the Windows Agent service:

```powershell
Restart-Service "Zabbix Agent 2"
```

Verify that:

* Host reconnects automatically
* Monitoring data continues updating
* Availability remains green

---

## Security Validation

The following conditions confirm PSK encryption is operational:

| Validation Item         | Status |
| ----------------------- | ------ |
| Host Available          | ✓      |
| Metrics Updating        | ✓      |
| Agent Logs Clean        | ✓      |
| Server Logs Clean       | ✓      |
| PSK Identity Match      | ✓      |
| Encrypted Communication | ✓      |

---

## Lessons Learned

This exercise demonstrated how Zabbix supports secure agent communication using Pre-Shared Key (PSK) encryption.

Key takeaways:

* PSK is simpler to deploy than certificate-based TLS.
* Both PSK Identity and PSK value must match exactly.
* Encryption can be enabled without requiring a PKI infrastructure.
* Host availability is the quickest method to validate successful deployment.

---

## Outcome

Encrypted communication between the Windows 10 Zabbix Agent and the Zabbix Server was successfully verified and validated.

