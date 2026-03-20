# 🔧 Troubleshooting Details

## 🔹 Issue 1: RIP route not received on R2 and R3

**Problem:**
R2 and R3 were not receiving the route for 192.168.1.0/24.

**Root Cause:**
Interface G0/1 on R1 was configured as a passive interface in RIP.

**Fix:**

```bash
router rip
no passive-interface g0/1
```

---

## 🔹 Issue 2: DHCP not working (192.168.2.0/24)

**Problem:**
Hosts were not receiving IP addresses.

**Root Cause:**
Missing DHCP relay configuration on R2.

**Fix:**

```bash
interface g0/0
ip helper-address 1.2.3.1
```

---

## 🔹 Issue 3: PAT not functioning

**Problem:**
Internal hosts could not access external network.

**Root Cause:**
Incorrect ACL used in NAT configuration.

**Fix:**

```bash
ip nat inside source list 1 interface g0/1 overload
```

---

## 🔹 Issue 4: DNS not received via DHCP

**Problem:**
Clients did not receive DNS server information.

**Root Cause:**
DNS server option missing in DHCP pool.

**Fix:**

```bash
ip dhcp pool 1pool
dns-server 30.0.0.100
```

---

## 🔹 Issue 5: SSH access not working

**Problem:**
Unable to connect via SSH.

**Root Cause:**
VTY lines allowed only Telnet.

**Fix:**

```bash
line vty 0 4
transport input ssh
```

---

## 🧠 Key Learning

* Importance of correct routing advertisements
* Role of DHCP relay in multi-network environments
* NAT ACL accuracy is critical
* DHCP options affect client usability
* SSH requires proper VTY configuration

