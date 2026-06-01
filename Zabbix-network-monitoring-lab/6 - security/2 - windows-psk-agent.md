# Windows 10 Agent PSK Configuration

## Overview

The Windows 10 endpoint was configured to use PSK encryption for secure communication with the Zabbix Server.

This ensures that all monitoring data exchanged between the Windows host and the Zabbix Server is encrypted and authenticated.

---

## Copying the PSK File

Copy the generated PSK file from the Zabbix Server to the Windows machine.

Destination Directory:

```text
C:\Program Files\Zabbix Agent 2\
```

File:

```text
zabbix_agentd.psk
```

---

## Modifying Agent Configuration

```text
C:\Program Files\Zabbix Agent 2\zabbix_agent2.conf
```

```ini
Server=192.168.122.11
Hostname=Saby-Windows

TLSConnect=psk
TLSAccept=psk

TLSPSKIdentity=Windows10-PSK
TLSPSKFile=C:\Program Files\Zabbix Agent 2\zabbix_agentd.psk
```

Parameter Description:

| Parameter      | Purpose                            |
| -------------- | ---------------------------------- |
| Server         | Zabbix Server IP Address           |
| Hostname       | Host name configured in Zabbix     |
| TLSConnect     | Use PSK for outbound communication |
| TLSAccept      | Accept only PSK connections        |
| TLSPSKIdentity | Unique PSK identifier              |
| TLSPSKFile     | Location of the PSK file           |

---

## Restarting the Agent

After saving the configuration, restart the Zabbix Agent service.

PowerShell:

```powershell
Restart-Service "Zabbix Agent 2"
```

Or using Services.msc:

1. Open Services
2. Locate Zabbix Agent 2
3. Restart the service

---

## Verification

Verified that:

* Zabbix Agent service is running
* Host appears Available in Zabbix
* Latest Data continues updating
* No TLS errors are present in the agent log

---

## Outcome

The Windows 10 Zabbix Agent was successfully configured to use encrypted PSK communication with the Zabbix Server.

