# 🔧 DNS Troubleshooting

---

# 📌 Overview

During deployment, DNS resolution worked correctly at the Singapore site but failed for clients at the India site.

Although network connectivity between sites and Internet access were functioning correctly, client devices connected to the India site were unable to resolve external Fully Qualified Domain Names (FQDNs).

This section documents the troubleshooting process used to identify and resolve the issue.

---

# Issue 1 - Clients Unable to Resolve FQDNs

## Symptoms

The following behaviour was observed:

- Clients successfully received IP addresses from DHCP.
- Clients could reach their default gateway.
- Internet connectivity was available.
- DNS queries for public domains failed.
- `ping google.com` failed.
- `ping 8.8.8.8` succeeded.

---

## Investigation

The following components were verified:

- DHCP configuration
- DNS server assignment
- Default gateway
- Internet connectivity
- NAT configuration
- VPN connectivity

Because connectivity to public IP addresses was successful, the issue was isolated to DNS resolution rather than routing.

---

# Issue 2 - BIND9 Configuration Verification

## Investigation

The following configuration files were reviewed:

```text
/etc/bind/named.conf.options
```

The following parameters were verified:

- Forwarders
- Recursion
- allow-query
- DNS listening interfaces

Both DNS servers were compared to ensure they used identical configurations.

---

# Issue 3 - Service Verification

## Investigation

The following commands were used during troubleshooting:

```text
sudo systemctl status named

sudo named-checkconf

journalctl -u named
```

Configuration validation confirmed that BIND9 contained no syntax errors.

---

# Root Cause

The DNS configuration itself was correct.

However, the BIND9 (`named`) service on the India DNS server was not actively serving the updated configuration.

As a result, DNS queries from client devices could not be resolved successfully.

---

# Resolution

The DNS service was restarted:

```text
sudo systemctl restart named
```

Immediately after restarting the service:

- External FQDN resolution succeeded.
- Client devices resolved Internet hostnames.
- DNS forwarding resumed normal operation.

---

# Verification

The following commands were used to verify successful operation:

```text
nslookup google.com

dig google.com

ping google.com
```

Successful verification confirmed:

- DNS forwarding operational.
- Recursive queries functioning correctly.
- Public domain resolution restored.
- Enterprise clients successfully resolved Internet hostnames.

---

# Lessons Learned

- Successful network connectivity does not necessarily indicate correct DNS functionality.
- Always verify network connectivity before investigating application-layer services.
- Compare working and non-working server configurations to isolate differences.
- Validate BIND configuration using `named-checkconf` before restarting services.
- Restarting a service after configuration changes is an essential final verification step.
