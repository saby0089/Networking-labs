
# 🔐 IPSec VPN Phase 1 Configuration

---

# 📌 Objective

The objective of Phase 1 was to establish a secure IKE (Internet Key Exchange) relationship between the FortiGate firewalls deployed at the Singapore and India sites.

Phase 1 is responsible for:

- Peer authentication
- Negotiating encryption algorithms
- Creating the IKE Security Association (IKE SA)
- Authenticating both VPN gateways using a Pre-Shared Key (PSK)

Only after a successful Phase 1 negotiation can the IPSec tunnel proceed to Phase 2.

---

# 🌐 VPN Design

| Parameter | Value |
|-----------|-------|
| VPN Type | Route-Based IPSec VPN |
| IKE Version | IKEv1 |
| Authentication | Pre-Shared Key |
| Encryption | DES |
| Authentication Algorithm | SHA1 |
| Diffie-Hellman Group | 5 |
| NAT Traversal | Disabled |
| Dead Peer Detection | Enabled |

> **Note:** The FortiGate VM trial image used in this project supported DES/SHA1 with DH Group 5, so those parameters were selected to ensure successful tunnel negotiation.

---

# 🏗️ VPN Topology

Singapore FortiGate

↓

WAN Interface (90.90.90.1)

↓

IPSec Tunnel

↓

WAN Interface (90.90.90.2)

↓

India FortiGate

---

# ⚙️ Configuration Summary

The following tasks were completed:

- Configured WAN interfaces
- Configured Remote Gateway
- Configured Pre-Shared Key
- Configured IKE Proposal
- Configured Dead Peer Detection
- Disabled NAT Traversal
- Verified Phase 1 Negotiation

---

# 📷 Configuration Screenshots

Insert screenshots:

- Singapore FortiGate Phase 1
- India FortiGate Phase 1

---

# ✅ Verification

Phase 1 negotiation was verified using:

```text
diagnose vpn ike gateway list

diagnose vpn tunnel list
```

Successful verification confirmed:

- IKE Security Association established
- VPN Gateway reachable
- Phase 1 negotiation successful

---

# 📷 Verification Screenshots

Insert:

- diagnose vpn ike gateway list

- diagnose vpn tunnel list

---

# 📖 Notes

A successful Phase 1 negotiation established the encrypted control channel between both FortiGate firewalls.

Once Phase 1 completed successfully, the deployment proceeded to configuring Phase 2 selectors and IPSec Security Associations.
