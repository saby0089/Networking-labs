# 🔧 IPSec VPN Troubleshooting

---

# 📌 Overview

Deploying the FortiGate Route-Based IPSec VPN required several rounds of troubleshooting before stable communication was achieved between both enterprise sites.

Although the VPN tunnel was successfully negotiated, traffic initially failed to traverse the tunnel. Multiple networking components were investigated before identifying the root causes.

---

# Issue 1 - Phase 1 Negotiation Failed

## Symptoms

- VPN tunnel remained down.
- Phase 1 Security Association was not established.

## Investigation

The following items were verified:

- Peer IP addresses
- WAN connectivity
- Pre-Shared Key
- Encryption proposal
- Authentication proposal
- Diffie-Hellman Group

## Root Cause

The FortiGate VM trial image supported only:

- DES
- SHA1
- DH Group 5

Using unsupported proposals prevented successful Phase 1 negotiation.

## Resolution

Both FortiGate firewalls were configured with identical supported proposals:

- DES
- SHA1
- DH Group 5

Phase 1 was successfully established.

---

# Issue 2 - Tunnel Established but No Traffic Passed

## Symptoms

- Phase 1: UP
- Phase 2: UP
- Remote networks unreachable

## Investigation

The following components were verified:

- Static routes
- Firewall policies
- Phase 2 selectors
- Routing tables

## Root Cause

Traffic was not being forwarded correctly into the IPSec tunnel due to incomplete routing configuration.

## Resolution

Static routes pointing to the IPSec tunnel interface were configured for all remote enterprise networks.

---

# Issue 3 - Remote Routes Not Learned

## Symptoms

- Tunnel operational
- Cisco routers unaware of remote networks

## Investigation

Routing tables on Cisco routers and FortiGate firewalls were compared.

## Root Cause

FortiGate static routes were not advertised into the OSPF routing domain.

## Resolution

Static route redistribution into OSPF was enabled.

Immediately afterwards, Cisco routers learned all remote enterprise networks dynamically.

---

# Issue 4 - Tunnel Up but Encryption Counters Not Increasing

## Symptoms

- Tunnel operational
- No encrypted traffic

## Investigation

The following command was used:

diagnose vpn tunnel list

## Root Cause

No user traffic matched the VPN routing and firewall policy.

## Resolution

Verified:

- Static routes
- Firewall policies
- Route redistribution

Generated ICMP traffic between both sites.

Encryption and decryption counters immediately increased.

---

# Verification

The VPN was considered fully operational after confirming:

- Tunnel Established
- Active ESP Security Associations
- Increasing Encryption Counters
- Successful End-to-End Communication

---

# Lessons Learned

- A tunnel showing **UP** does not guarantee traffic flow.
- Routing and firewall policies are just as important as VPN configuration.
- Route redistribution is essential when integrating static VPN routes into an OSPF environment.
- Verification should always include encrypted traffic counters, not only tunnel status.
