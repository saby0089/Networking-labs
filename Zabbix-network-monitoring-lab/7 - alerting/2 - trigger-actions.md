
# Trigger and Action Configuration

## Objective

Create automated actions that generate email notifications when monitored hosts experience failures.

---

## Trigger Creation

Example trigger:

```text
Host unavailable
```

Expression:

```text
agent.ping.nodata(3m)=1
```

Severity:

```text
High
```

---

## Action Configuration

Navigation:

```text
Alerts → Actions → Trigger Actions
```

Action Name:

```text
Host Failure Alert
```

Conditions:

```text
Trigger Severity >= High
```

Operations:

```text
Send message to user
```

Media:

```text
Email
```

---

## Recovery Actions

Configured recovery notifications to automatically inform administrators when the host becomes available again.

Example:

```text
Problem:
Host is Down

Recovery:
Host is Back Online
```

---

## Result

Automatic notifications were successfully generated whenever monitored hosts entered or exited a fault condition.
