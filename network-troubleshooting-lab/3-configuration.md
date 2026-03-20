# Configuration Summary

## 🔹 RIP Configuration

```bash
router rip
version 2
network 192.168.1.0
network 1.2.3.0
no auto-summary
```

---

## 🔹 DHCP Configuration

```bash
ip dhcp pool 1pool
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 30.0.0.100
```

---

## 🔹 NAT Configuration

```bash
access-list 1 permit 192.168.1.0 0.0.0.255

interface g0/0
ip nat inside

interface g0/1
ip nat outside

ip nat inside source list 1 interface g0/1 overload
```

---

## 🔹 SSH Configuration

```bash
ip domain-name cisco.com
crypto key generate rsa
ip ssh version 2

line vty 0 4
transport input ssh
login local
```

