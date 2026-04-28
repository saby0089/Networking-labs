
############################################################

# DEVICE DOCUMENTATION: ISP NETWORK (ISP-1 / ISP-2 / ISP-3)

############################################################

## 1. NETWORK OVERVIEW

---

Role             : Service Provider (Transit Network)
Primary Function :

* Provide connectivity between HQ (AS 65001) and DR (AS 65002)
* Act as transit network for inter-site communication
* Maintain BGP routing across ISP cloud

Autonomous Systems:

* ISP-1 / ISP-2 : AS 65000
* ISP-3         : AS 65003

---

## 2. ISP TOPOLOGY DESIGN

---

* ISP-1 and ISP-2 form core ISP backbone (AS 65000)
* ISP-3 operates as external ISP (AS 65003)
* Full connectivity maintained between ISPs

Interconnections:

* ISP-1 ↔ ISP-2
* ISP-1 ↔ ISP-3
* ISP-2 ↔ ISP-3

---

## 3. INTERFACE CONFIGURATION

---

### 3.1 ISP-1 Interfaces
```bash
interface g0/0
description Link to HQ-EDGE
ip address 100.1.1.2 255.255.255.252
no shutdown

interface g0/1
description Link to DR-EDGE
ip address 100.2.1.2 255.255.255.252
no shutdown

interface g0/2
description Link to ISP-2
ip address 200.1.1.1 255.255.255.252
no shutdown

interface g0/3
description Link to ISP-3
ip address 200.1.2.2 255.255.255.252
no shutdown
```
---

### 3.2 ISP-2 Interfaces
```bash
interface g0/0
description Link to HQ-EDGE
ip address 100.1.2.2 255.255.255.252
no shutdown

interface g0/1
description Link to DR-EDGE
ip address 100.2.2.2 255.255.255.252
no shutdown

interface g0/2
description Link to ISP-1
ip address 200.1.1.2 255.255.255.252
no shutdown

interface g0/3
description Link to ISP-3
ip address 200.1.3.2 255.255.255.252
no shutdown
```
---

### 3.3 ISP-3 Interfaces
```bash
interface g0/0
description Link to HQ-EDGE
ip address 100.1.3.2 255.255.255.252
no shutdown

interface g0/1
description Link to DR-EDGE
ip address 100.2.3.2 255.255.255.252
no shutdown

interface g0/2
description Link to ISP-1
ip address 200.1.2.1 255.255.255.252
no shutdown

interface g0/3
description Link to ISP-2
ip address 200.1.3.1 255.255.255.252
no shutdown
```
---

## 4. BGP CONFIGURATION

---

### 4.1 ISP-1 (AS 65000)
```bash
router bgp 65000
bgp log-neighbor-changes
```
# Enterprise neighbors
```bash
neighbor 100.1.1.1 remote-as 65001   # HQ
neighbor 100.2.1.1 remote-as 65002   # DR
```
# Internal ISP peer
```bash
neighbor 200.1.1.2 remote-as 65000   # ISP-2
```
# External ISP peer
```bash
neighbor 200.1.2.1 remote-as 65003   # ISP-3
```
---

### 4.2 ISP-2 (AS 65000)
```bash
router bgp 65000
bgp log-neighbor-changes
```
# Enterprise neighbors
```bash
neighbor 100.1.2.1 remote-as 65001   # HQ
neighbor 100.2.2.1 remote-as 65002   # DR
```
# Internal ISP peer
```bash
neighbor 200.1.1.1 remote-as 65000   # ISP-1
```
# External ISP peer
```bash
neighbor 200.1.3.1 remote-as 65003   # ISP-3
```
---

### 4.3 ISP-3 (AS 65003)
```bash
router bgp 65003
bgp log-neighbor-changes
```
# Enterprise neighbors
```bash
neighbor 100.1.3.1 remote-as 65001   # HQ
neighbor 100.2.3.1 remote-as 65002   # DR
```
# Upstream ISPs
```bash
neighbor 200.1.2.2 remote-as 65000   # ISP-1
neighbor 200.1.3.2 remote-as 65000   # ISP-2
```
---

## 5. ROUTING BEHAVIOR

---

* ISPs exchange routes using BGP
* Enterprise prefixes learned from HQ and DR
* Routes propagated across ISP network
* Enables inter-site communication via transit paths

---

## 6. DESIGN CHARACTERISTICS

---

* Multi-homed enterprise connectivity
* Redundant ISP paths
* Full mesh ISP interconnectivity
* Separation of enterprise and provider AS

---

## 7. VERIFICATION COMMANDS

---
```bash
show ip bgp summary
show ip bgp
show ip route
show ip bgp neighbors
```
---

## 8. KEY TAKEAWAYS

---

* Demonstrates ISP transit routing
* Shows eBGP and iBGP relationships
* Enables multi-path routing between enterprise sites
* Supports failover and redundancy scenarios

############################################################
