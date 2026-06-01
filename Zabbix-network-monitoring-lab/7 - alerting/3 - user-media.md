
# User Media Configuration

## Objective

Associate email addresses with Zabbix users to receive alert notifications.

---

## Navigation

```text
Users → Users → Admin → Media
```

---

## Media Configuration

Media Type:

```text
Email
```

Send To:

```text
zabbix@lab.local
```

Severity:

```text
Information
Warning
Average
High
Disaster
```

Enabled:

```text
Yes
```

---

## Testing

A test alert was generated to verify delivery.

The message successfully appeared within the MailHog mailbox.

---

## Result

The Zabbix administrator account was configured to receive email notifications for monitoring events and trigger alerts.
