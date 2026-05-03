## Troubleshooting

---

### 1. BGP Neighbor Stuck in Active State

**Command**

```bash
show ip bgp summary
```

**Observation**

* Neighbor state remains in Active
* No prefixes received

**Cause**

* Loopback-based iBGP peering without reachability

**Fix**

```bash
ip route 2.2.2.2 255.255.255.255 209.165.204.1
ip route 3.3.3.3 255.255.255.255 209.165.205.1
```

---

### 2. Ping Works Normally but Fails with Source Loopback

**Command**

```bash
ping 2.2.2.2 source 1.1.1.1
```

**Observation**

* Standard ping works
* Source-based ping fails

**Cause**

* Missing return path for loopback traffic

**Fix**

```bash
ip route 1.1.1.1 255.255.255.255 209.165.204.2
ip route 1.1.1.1 255.255.255.255 209.165.205.2
```

---

### 3. Route Present in BGP Table but Not in Routing Table

**Commands**

```bash
show ip bgp
show ip route
```

**Observation**

* Route visible in BGP table
* Route missing from routing table

**Cause**

* Next-hop not reachable

**Fix**

```bash
router bgp 65003
 neighbor 2.2.2.2 next-hop-self
 neighbor 3.3.3.3 next-hop-self
```

---

### 4. Traffic Dropped at ISP Edge

**Command**

```bash
traceroute 209.165.204.2
```

**Observation**

* Traffic stops at ISP router

**Cause**

* Missing default route toward transit network

**Fix**

```bash
ip route 0.0.0.0 0.0.0.0 209.165.203.2
```

---

### 5. Partial Connectivity Across Network

**Command**

```bash
show ip bgp
```

**Observation**

* Some networks reachable, others not

**Cause**

* Missing BGP network advertisement

**Fix**

```bash
router bgp 65000
 network 10.10.10.0 mask 255.255.255.0
 network 172.16.200.0 mask 255.255.255.0
```

---

### 6. iBGP Session Established but No Route Exchange

**Command**

```bash
show ip bgp neighbors
```

**Observation**

* Session is Established
* No prefixes received

**Cause**

* No networks configured for advertisement

**Fix**

* Add `network` statements or redistribution in BGP

---

### 7. Routes Filtered Incorrectly

**Command**

```bash
show ip bgp neighbors 209.165.201.2 received-routes
```

**Observation**

* Expected routes missing

**Cause**

* Incorrect prefix-list or route-map

**Fix**

```bash
ip prefix-list OUR-NETS permit 10
```

---

### 8. End-to-End Connectivity Failure

**Commands**

```bash
ping 209.165.204.2
traceroute 209.165.204.2
```

**Observation**

* Packet loss or incomplete path

**Cause**

* Routing inconsistency (next-hop / default route / filtering)

**Fix**

* Verify:

  * Next-hop reachability
  * Default route presence
  * Route installation in RIB

```
```

