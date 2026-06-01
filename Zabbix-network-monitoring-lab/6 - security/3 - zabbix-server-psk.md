
# Zabbix Server PSK Configuration

## Overview

After configuring PSK encryption on the Windows 10 Zabbix Agent, the Zabbix Server was configured to authenticate using the same PSK Identity and Pre-Shared Key.

This enables encrypted communication between the monitoring server and monitored endpoint.

---

## Host Configuration

Navigate to:

```text
Data Collection → Hosts → Saby-Windows
```

Open the host configuration and select the **Encryption** tab.

---

## Encryption Settings

Configure the following parameters:

| Setting               | Value             |
| --------------------- | ----------------- |
| Connections to host   | PSK               |
| Connections from host | PSK               |
| PSK Identity          | Windows10-PSK     |
| PSK                   | Generated PSK Key |

Example:

```text
PSK Identity:
Windows10-PSK

PSK:
<REDACTED FOR SECURITY>
```

---

## Applying Changes

After entering the PSK details:

1. Click **Update**
2. Wait for the host to reconnect
3. Monitor the host availability indicator

Expected Result:

```text
Availability: ZBX (Green)
```

---

## Security Benefits

Using PSK encryption provides:

* Encrypted agent-server communication
* Agent authentication
* Protection against unauthorized monitoring requests
* Protection against packet interception

---

## Troubleshooting

If the host becomes unavailable after enabling PSK:

### Verify PSK Identity

The identity configured on:

* Windows Agent
* Zabbix Server

must match exactly.

### Verify PSK Value

Both systems must use the identical PSK string.

### Check Agent Logs

Windows Agent Log Location:

```text
C:\Program Files\Zabbix Agent 2\zabbix_agent2.log
```

Common Error:

```text
TLS handshake failed
```

This usually indicates a PSK mismatch.

---

## Outcome

The Zabbix Server was successfully configured to communicate securely with the Windows 10 agent using PSK encryption.
