# Email Alert Configuration using MailHog

## Objective

Configure Zabbix email notifications using MailHog as the SMTP server for testing alert delivery in a lab environment.

---

## Environment

| Component         | Value          |
| ----------------- | -------------- |
| Monitoring Server | Zabbix Server  |
| SMTP Server       | MailHog        |
| Mail Client       | MailHog Web UI |
| Operating System  | Ubuntu Linux   |
| Notification Type | Email          |

---

## MailHog Installation

MailHog was installed on the Ubuntu Linux host used in the monitoring environment.

Verification:

```bash
systemctl status mailhog
```

MailHog web interface:

```text
http://192.168.122.191:8025
```

---

## Zabbix Media Type Configuration

Navigation:

```text
Alerts → Media Types → Email
```

Configuration:

```text
SMTP Server: Ubuntu MailHog Server
SMTP Port: 1025
Connection Security: None
Authentication: None
```

---

## Verification

A test email was generated from Zabbix and successfully received within the MailHog web interface.

This confirmed successful integration between Zabbix and the SMTP service.

---

## Result

Zabbix was successfully configured to deliver email notifications through MailHog, enabling alert testing without relying on an external mail provider.

