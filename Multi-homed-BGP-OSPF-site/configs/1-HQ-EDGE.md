############################################################

# DEVICE DOCUMENTATION: HQ-EDGE

############################################################

## 1. DEVICE OVERVIEW

---

Hostname        : HQ-EDGE
Role            : Enterprise Edge Router (HQ Site)
Autonomous System: 65001
Function        :

* Connects HQ to multiple ISPs
* Runs OSPF (IGP) internally
* Runs BGP (EGP) externally
* Performs route redistribution (BGP ↔ OSPF)
* Implements traffic engineering policies

---

## 2. INTERFACE CONFIGURATION

---

### 2.1 Internal Link (HQ-CORE)
```bash
interface g0/0
description Link to HQ-CORE
ip address 10.1.1.1 255.255.255.252
no shutdown
```
### 2.2 External Links (ISPs)
```bash
interface g0/1
description Link to ISP-1 (Primary)
ip address 100.1.1.1 255.255.255.252
no shutdown

interface g0/2
description Link to ISP-2 (Secondary)
ip address 100.1.2.1 255.255.255.252
no shutdown

interface g0/3
description Link to ISP-3 (Backup)
ip address 100.1.3.1 255.255.255.252
no shutdown
```
---

## 3. IGP CONFIGURATION (OSPF)

---
```bash
router ospf 1
router-id 1.1.1.2
```
# Internal network advertisement
```bash
network 10.1.1.0 0.0.0.3 area 0
```
# Inject external routes into OSPF
```bash
redistribute bgp 65001 subnets
```
# Inject default route into internal network
```bash
default-information originate
```
---

## 4. EGP CONFIGURATION (BGP)

---
```bash
router bgp 65001
bgp log-neighbor-changes
```
### 4.1 eBGP Neighbors
```bash
neighbor 100.1.1.2 remote-as 65000   # ISP-1
neighbor 100.1.2.2 remote-as 65000   # ISP-2
neighbor 100.1.3.2 remote-as 65003   # ISP-3
```
### 4.2 Network Advertisement
```bash
network 192.168.10.0 mask 255.255.255.0
```
---

## 5. TRAFFIC ENGINEERING POLICIES

---

### 5.1 Outbound Traffic Control (Local Preference)

# Prefer ISP-1
```bash
route-map PREF-ISP1 permit 10
set local-preference 200

router bgp 65001
neighbor 100.1.1.2 route-map PREF-ISP1 in
```
# Lower priority for ISP-3 (Backup)
```bash
route-map LOW-PREF permit 10
set local-preference 50

router bgp 65001
neighbor 100.1.3.2 route-map LOW-PREF in
```
---

## 6. INBOUND TRAFFIC CONTROL (AS PATH PREPENDING)

---

# De-prioritize ISP-2 path
```bash
route-map PREPEND-ISP2 permit 10
set as-path prepend 65001 65001 65001

router bgp 65001
neighbor 100.1.2.2 route-map PREPEND-ISP2 out
```
---

## 7. ROUTE FILTERING POLICIES

---

### 7.1 Outbound Filtering

# Advertise only HQ LAN network
```bash
ip prefix-list LAN_ONLY seq 5 permit 192.168.10.0/24

route-map FILTER-OUT permit 10
match ip address prefix-list LAN_ONLY

router bgp 65001
neighbor 100.1.1.2 route-map FILTER-OUT out
neighbor 100.1.2.2 route-map FILTER-OUT out
neighbor 100.1.3.2 route-map FILTER-OUT out
```
---

### 7.2 Inbound Filtering

# Accept only DR LAN network
```bash
ip prefix-list REMOTE-LAN seq 5 permit 192.168.20.0/24

route-map FILTER-IN permit 10
match ip address prefix-list REMOTE-LAN

router bgp 65001
neighbor 100.1.1.2 route-map FILTER-IN in
neighbor 100.1.2.2 route-map FILTER-IN in
neighbor 100.1.3.2 route-map FILTER-IN in
```
---

## 8. VERIFICATION COMMANDS

---
```bash
show ip bgp summary
show ip bgp
show ip route
show ip ospf neighbor
show ip bgp neighbors
```
---

## 9. DESIGN NOTES

---

* OSPF is used for internal routing within HQ
* BGP is used for external connectivity with ISPs
* Redistribution ensures route visibility across domains
* Local Preference influences outbound traffic selection
* AS Path Prepending influences inbound traffic selection
* Route filtering ensures controlled route advertisement

---

## 10. KEY TAKEAWAYS

---

* Demonstrates multi-homing with three ISPs
* Implements redundancy and failover
* Uses BGP attributes for traffic engineering
* Applies best practices for route control and filtering

############################################################
