
# 🔄 OSPF Configuration - Branch Site (India)

---

# 📌 Objective

The Branch Office was configured using OSPF to dynamically exchange routes between Layer-3 switches and routers.

The routing design mirrors the Main Site, providing a consistent enterprise architecture across both locations.

---

# 🏗️ OSPF Topology

Devices participating in OSPF:

- 2 × Layer-3 Switches
- Router-Site2
- Redundant Router

---

# 🌐 Advertised Networks

| Network | Description |
|----------|-------------|
| 192.168.30.0/24 | VLAN 300 |
| 192.168.40.0/24 | VLAN 400 |
| 192.168.60.0/24 | Server VLAN |
| 30.0.0.0/30 | Router Interconnection |
| 40.0.0.0/30 | Router Interconnection |

---

# ⚙️ Configuration Summary

Completed tasks:

- Enabled OSPF
- Configured Router ID
- Advertised VLAN networks
- Advertised inter-router links
- Verified neighbor relationships
- Verified routing tables

---

# ✅ Verification

Commands used:

```text
show ip ospf neighbor

show ip route ospf

show ip protocols

show ip ospf interface brief
```

Successful verification confirmed:

- Neighbor adjacency established
- Dynamic route learning
- End-to-end connectivity
- Stable routing across the Branch Site

---

# 📷 Verification Screenshots

- Neighbor Table
  ![Screenshots](../Images/router-site2-neighbor.png)  ![Screenshots](../Images/l3-site2-neighbor.png)
  
- Routing Table
- Interface Status
- Successful Ping Tests

---

# 📖 Notes

After OSPF convergence, both enterprise sites were prepared for secure route exchange through the FortiGate IPSec VPN.
