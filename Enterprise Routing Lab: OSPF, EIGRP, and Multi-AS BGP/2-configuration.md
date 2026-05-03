## Configuration

---

### 1. CORE Router (OSPF + EIGRP + Redistribution)

#### OSPF

```
router ospf 1
 router-id 1.1.1.1
 network 10.0.0.0 0.255.255.255 area 0
 passive-interface default
 no passive-interface g0/1
 no passive-interface g0/2
```

#### EIGRP

```
router eigrp 100
 no auto-summary
 network 172.16.200.0 0.0.0.255
```

#### Redistribution

```
router ospf 1
 redistribute eigrp 100 subnets

router eigrp 100
 redistribute ospf 1 metric 10000 100 255 1 1500
```
#### Redistribution with Route Tagging (Loop Prevention)

```
route-map EIGRP-TO-OSPF permit 10
 set tag 100

router ospf 1
 redistribute eigrp 100 subnets route-map EIGRP-TO-OSPF

route-map OSPF-TO-EIGRP deny 10
 match tag 100
route-map OSPF-TO-EIGRP permit 20

router eigrp 100
 redistribute ospf 1 metric 10000 100 255 1 1500 route-map OSPF-TO-EIGRP
```
---

### 2. EDGE Router (eBGP)

```
router bgp 65000
 bgp log-neighbor-changes

 neighbor 209.165.200.2 remote-as 65001
 neighbor 209.165.201.2 remote-as 65002

 network 10.10.10.0 mask 255.255.255.0
 network 10.20.20.0 mask 255.255.255.0
 network 172.16.200.0 mask 255.255.255.0
```

---

### 3. ISP1 / ISP2 (eBGP + Default Route)

```
router bgp 65001
 neighbor 209.165.200.2 remote-as 65000
```

#### Default Route

```
ip route 0.0.0.0 0.0.0.0 209.165.202.2
```

---

### 4. ISP3-CORE (iBGP + Loopback)

#### Loopback

```
interface Loopback0
 ip address 1.1.1.1 255.255.255.255
```

#### iBGP

```
router bgp 65003
 neighbor 2.2.2.2 remote-as 65003
 neighbor 2.2.2.2 update-source Loopback0
 neighbor 2.2.2.2 next-hop-self

 neighbor 3.3.3.3 remote-as 65003
 neighbor 3.3.3.3 update-source Loopback0
 neighbor 3.3.3.3 next-hop-self
```

---

### 5. ISP3-PE1

#### Loopback

```
interface Loopback0
 ip address 2.2.2.2 255.255.255.255
```

#### iBGP

```
router bgp 65003
 neighbor 1.1.1.1 remote-as 65003
 neighbor 1.1.1.1 update-source Loopback0
```

#### Static Route (Loopback Reachability)

```
ip route 1.1.1.1 255.255.255.255 209.165.204.2
```

---

### 6. ISP3-PE2

#### Loopback

```
interface Loopback0
 ip address 3.3.3.3 255.255.255.255
```

#### iBGP

```
router bgp 65003
 neighbor 1.1.1.1 remote-as 65003
 neighbor 1.1.1.1 update-source Loopback0
```

#### Static Route

```
ip route 1.1.1.1 255.255.255.255 209.165.205.2
```

---

### 7. Route Filtering (EDGE)

#### Prefix List

```
ip prefix-list OUR-NETS seq 10 permit 10.10.10.0/24
ip prefix-list OUR-NETS seq 20 permit 10.20.20.0/24
ip prefix-list OUR-NETS seq 30 permit 172.16.200.0/24
```

#### Route Map

```
route-map OUT-FILTER permit 10
 match ip address prefix-list OUR-NETS
```

#### Apply to Neighbors

```
router bgp 65000
 neighbor 209.165.200.2 route-map OUT-FILTER out
 neighbor 209.165.201.2 route-map OUT-FILTER out
```

---

### 8. Soft Reconfiguration

```
router bgp 65000
 neighbor 209.165.200.2 soft-reconfiguration inbound
 neighbor 209.165.201.2 soft-reconfiguration inbound
```

