
## Verification

---

### 1. OSPF Adjacency (Core ↔ Edge)

```bash id="ybm2n7"
show ip ospf neighbor
```

**Expected**

* FULL adjacency with Edge router
* No neighbors stuck in EXSTART / DOWN

---

### 2. EIGRP Adjacency (Core ↔ Branch)

```bash id="s1v3gr"
show ip eigrp neighbors
```

**Expected**

* Neighbor entry for Branch router
* Stable uptime (no frequent resets)

---

### 3. Redistribution Check (OSPF ↔ EIGRP)

```bash id="7mns4o"
show ip route
```

**Expected**

* OSPF routes visible in EIGRP domain (D EX)
* EIGRP routes visible in OSPF domain (O E2)

---

### 4. BGP Neighbor Status

```bash id="9n3qz9"
show ip bgp summary
```

**Expected**

* All neighbors in **Established**
* Non-zero prefixes received

---

### 5. BGP Route Table

```bash id="u1axv3"
show ip bgp
```

**Expected**

* Multiple paths for external prefixes
* Valid next-hop entries
* Best path marked with `*>`

---

### 6. Routing Table Validation

```bash id="qz9t8l"
show ip route
```

**Expected**

* BGP routes (B)
* OSPF routes (O)
* EIGRP routes (D)
* Default route

---

### 7. Next-Hop Reachability

```bash id="c6lq9y"
show ip route <next-hop-ip>
```

**Expected**

* Next-hop IP must be reachable
* Route installed in RIB

---

### 8. Advertised Routes (BGP)

```bash id="2j9k0h"
show ip bgp neighbors <neighbor-ip> advertised-routes
```

**Expected**

* Only intended prefixes advertised
* No unwanted internal networks leaked

---

### 9. Received Routes (BGP)

```bash id="d8f4m1"
show ip bgp neighbors <neighbor-ip> received-routes
```

**Expected**

* Routes received from ISP / transit network
* No missing prefixes

---

### 10. End-to-End Connectivity

```bash id="v3n2k7"
ping 209.165.204.2
```

**Expected**

* Successful replies from:

  * Branch → HQ
  * HQ → ISP networks

---

### 11. Path Verification

```bash id="g5p1x9"
traceroute 209.165.205.2
```

**Expected**

* Traffic path:

  * Enterprise → ISP → Transit
* No unexpected drops

---

### 12. Data Plane Validation

```bash id="y7w4q2"
show ip cef 209.165.201.1
```

**Expected**

* Correct next-hop resolution
* Multiple paths if ECMP enabled

---
