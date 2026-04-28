############################################################

# DEVICE DOCUMENTATION: DR-EDGE

############################################################

## 1. DEVICE OVERVIEW

---

Hostname         : DR-EDGE
Role             : Enterprise Edge Router (DR Site)
Autonomous System: 65002
Function         :

* Connects DR site to multiple ISPs
* Runs OSPF internally within DR
* Runs BGP externally with ISPs
* Performs route redistribution (BGP ↔ OSPF)
* Implements traffic engineering and failover policies

---

## 2. INTERFACE CONFIGURATION

---

### 2.1 Internal Link (DR-CORE)
```bash
interface g0/0
description Link to DR-CORE
ip address 10.2.2.1 255.255.255.252
no shutdown
```
### 2.2 External Links (ISPs)
```bash
interface g0/1
description Link to ISP-1 (Secondary Path)
ip address 100.2.1.1 255.255.255.252
no shutdown

interface g0/2
description Link to ISP-2 (Primary Path)
ip address 100.2.2.1 255.255.255.252
no shutdown

interface g0/3
description Link to ISP-3 (Backup Path)
ip address 100.2.3.1 255.255.255.252
no shutdown
```
---

## 3. IGP CONFIGURATION (OSPF)

---
```bash
router ospf 1
router-id 2.2.2.1
```
# Internal network advertisement
```bash
network 10.2.2.0 0.0.0.3 area 0
```
# Redistribute external routes into OSPF
```bash
redistribute bgp 65002 subnets
```
# Inject default route into DR internal network
```bash
default-information originate
```
---

## 4. EGP CONFIGURATION (BGP)

---
```bash
router bgp 65002
bgp log-neighbor-changes
```
### 4.1 eBGP Neighbors
```bash
neighbor 100.2.1.2 remote-as 65000   # ISP-1
neighbor 100.2.2.2 remote-as 65000   # ISP-2
neighbor 100.2.3.2 remote-as 65003   # ISP-3
```
### 4.2 Network Advertisement
```bash
network 192.168.20.0 mask 255.255.255.0
```
---

## 5. TRAFFIC ENGINEERING POLICIES

---

### 5.1 Outbound Traffic Control (Local Preference)

# Prefer ISP-2 (Primary Path for DR)
```bash
route-map PREF-ISP2 permit 10
set local-preference 200

router bgp 65002
neighbor 100.2.2.2 route-map PREF-ISP2 in
```
# Lower priority for ISP-3 (Backup)
```bash
route-map LOW-PREF permit 10
set local-preference 50

router bgp 65002
neighbor 100.2.3.2 route-map LOW-PREF in
```
---

## 6. INBOUND TRAFFIC CONTROL (AS PATH PREPENDING)

---

# De-prioritize ISP-1 path
```bash
route-map PREPEND-ISP1 permit 10
set as-path prepend 65002 65002 65002

router bgp 65002
neighbor 100.2.1.2 route-map PREPEND-ISP1 out
```
---

## 7. ROUTE FILTERING POLICIES

---

### 7.1 Outbound Filtering

# Advertise only DR LAN network
```bash
ip prefix-list LAN_ONLY seq 5 permit 192.168.20.0/24

route-map FILTER-OUT permit 10
match ip address prefix-list LAN_ONLY

router bgp 65002
neighbor 100.2.1.2 route-map FILTER-OUT out
neighbor 100.2.2.2 route-map FILTER-OUT out
neighbor 100.2.3.2 route-map FILTER-OUT out
```
---

### 7.2 Inbound Filtering

# Accept only HQ LAN network
```bash
ip prefix-list REMOTE-LAN seq 5 permit 192.168.10.0/24

route-map FILTER-IN permit 10
match ip address prefix-list REMOTE-LAN

router bgp 65002
neighbor 100.2.1.2 route-map FILTER-IN in
neighbor 100.2.2.2 route-map FILTER-IN in
neighbor 100.2.3.2 route-map FILTER-IN in
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

* OSPF provides internal routing within DR site
* BGP provides external connectivity to ISPs
* Redistribution ensures DR internal routers learn remote routes
* Local Preference determines outbound path selection
* AS Path Prepending influences inbound traffic behavior
* Route filtering controls route advertisement and acceptance

---

## 10. KEY TAKEAWAYS

---

* Demonstrates DR site redundancy design
* Implements multi-homing with three ISPs
* Ensures high availability and failover capability
* Uses BGP policies for traffic engineering
* Follows best practices for route control and filtering

############################################################

