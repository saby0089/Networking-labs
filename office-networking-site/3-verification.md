# 🧪 Verification & Testing

This document validates network functionality, redundancy, and service availability.

---

## 🔁 HSRP Verification
```bash
show standby brief
```

✔ One Active, one Standby per VLAN  
✔ Virtual IP used as gateway  

---

## 🔗 EtherChannel Verification
```bash
show etherchannel summary
```

✔ Status: SU (Layer2 + in use)

---

## 🌐 Routing Verification
```bash
show ip route
show ip ospf neighbor
```

✔ OSPF neighbors established  
✔ Routes learned via tunnel  

---

## 🌍 GRE Tunnel Verification
```bash
show ip interface brief
```

✔ Tunnel0 → up/up  
```bash
ping 172.16.1.2
```

✔ Successful  

---

## 🔐 NAT Verification
```bash
show ip nat translations
```

✔ Private → Public translation visible  

---

## 🖥️ DHCP Verification

On PC:
```bash
ipconfig
```

✔ IP assigned  
✔ Gateway = HSRP VIP  
✔ DNS correct  

---

## 🌐 DNS Verification
```bash
ping web.sabycompany.com
```

✔ Name resolution successful  

---

## 🌍 Web Server Test

Browser:
```bash
http://web.sabycompany.com
```

✔ Page loads successfully  

---

## 📧 Email Verification

- Send email: saby → admin  
- Receive email: admin inbox  

✔ Successful delivery  

---

## 🔁 Redundancy Testing (CRITICAL)

### 🔻 Test 1: HSRP Failover
Shutdown primary switch

✔ Traffic continues  

---

### 🔻 Test 2: ISP Failover
Shutdown primary WAN link

✔ Backup route takes over  

---

### 🔻 Test 3: Link Failure
Disable one EtherChannel link

✔ No impact  

---

## 🧠 Conclusion

All redundancy mechanisms (HSRP, EtherChannel, ISP failover, GRE) and services (DHCP, DNS, Email, Web) are functioning correctly and validated end-to-end.
