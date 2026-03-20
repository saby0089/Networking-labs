
# Verification

## ✅ Routing Verification

```bash
show ip route
```

✔ R2 and R3 received 192.168.1.0/24

---

## ✅ DHCP Verification

```bash
ipconfig /all
```

✔ IP assigned
✔ Default gateway present
✔ DNS received

---

## ✅ NAT Verification

```bash
show ip nat translations
```

✔ Internal IP translated to public IP

---

## ✅ SSH Verification

```bash
ssh -l cisco 1.2.3.1
```

✔ Successful login

---

## ✅ Connectivity Tests

```bash
ping
traceroute
```

✔ End-to-end connectivity confirmed
