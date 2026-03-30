# 🔍 Verification & Testing

This document contains all commands and tests used to verify the network functionality.

---

# 🟢 1. VLAN Verification

```bash
show vlan brief
```

✔ Ensures VLANs are created and ports assigned

---

# 🟢 2. Trunk Verification

```bash
show interfaces trunk
```

✔ Confirms trunk links and allowed VLANs

---

# 🟢 3. EtherChannel Verification

```bash
show etherchannel summary
```

✔ Confirms:

* Port-channel is up (SU or RU)
* Member interfaces active

---

# 🟢 4. STP Verification

```bash
show spanning-tree
```

✔ Identifies:

* Root bridge
* Blocking ports (orange links)

---

# 🟢 5. IP Interface Status

```bash
show ip interface brief
```

✔ Confirms all interfaces are up/up

---

# 🟢 6. OSPF Neighbor Check

```bash
show ip ospf neighbor
```

✔ Ensures adjacency between switches

---

# 🟢 7. Routing Table

```bash
show ip route
```

✔ Confirms:

* OSPF routes (O)
* ECMP (multiple next-hops)

---

# 🟢 8. Connectivity Tests

## 🔹 PC to Gateway

```bash
ping 10.x.x.1
```

---

## 🔹 Inter-VLAN

```bash
ping between VLANs
```

---

## 🔹 Core to ISP

```bash
ping 200.1.1.2
```

---

## 🔹 End-to-End

```bash
PC → ISP
```

✔ Full path verification

---

# 🟢 9. DHCP Verification

On PC:

```bash
ipconfig
```

✔ Checks:

* IP assigned
* Gateway
* DNS

---

# 🟢 10. DNS Verification

Browser test:

```text
http://www.hospital.local
```

✔ Should resolve successfully

---

# 🟢 11. Wireless Testing

* Connect laptop/phone to WiFi
* Verify DHCP IP
* Test internet access

---

# 🟢 12. Port Security Check

```bash
show port-security
```

✔ Confirms:

* Secure MACs
* Violation mode

---

# 🟢 13. WAN Verification

```bash
show ip route
```

✔ Default route present

---

# 🟢 14. Troubleshooting Commands

```bash
show cdp neighbors
show running-config
show ip protocols
```

---

# ✅ Final Validation Checklist

✔ All VLANs reachable
✔ OSPF neighbors up
✔ ECMP working
✔ Wireless clients connected
✔ Internet reachable
✔ DNS working

---

# 🏆 Conclusion

The network has been successfully verified for:

* Connectivity
* Redundancy
* Routing
* Services
* Security

---

