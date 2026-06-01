
# PSK Generation

## Overview

To secure communication between the Zabbix Server and the Windows 10 Zabbix Agent, Pre-Shared Key (PSK) encryption was implemented.

PSK encryption ensures that monitoring traffic exchanged between the server and agent is encrypted and authenticated, preventing unauthorized systems from communicating with monitored hosts.

---

## Generating the PSK

On the Zabbix Server, generate a 256-bit PSK using OpenSSL:

```bash
openssl rand -hex 32 > /etc/zabbix/zabbix_agentd.psk
```

Display the generated key:

```bash
cat /etc/zabbix/zabbix_agentd.psk
```

Example Output:

```text
7e1f8d1a6c8f3b7c9e5d2a1f4b6c8d7e9a1b2c3d4e5f67890123456789abcdef
```

---

## Securing the PSK File

Restrict access permissions to prevent unauthorized access.

```bash
chmod 600 /etc/zabbix/zabbix_agentd.psk
```

Verify permissions:

```bash
ls -l /etc/zabbix/zabbix_agentd.psk
```

Expected Result:

```text
-rw------- 1 root root
```

---

## Security Considerations

* Never expose the PSK in public repositories.
* Store the PSK securely.
* Use unique PSK identities for each monitored host.
* Limit file permissions to the Zabbix service account.

---

## Outcome

A secure PSK was generated and prepared for deployment between the Zabbix Server and the Windows 10 monitoring agent.
