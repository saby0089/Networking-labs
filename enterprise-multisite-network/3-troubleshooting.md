# Troubleshooting Scenarios

## Issue 1: Branch PCs unable to access internet

### Problem

Branch network traffic was reaching ISP, but no reply was received.

### Root Cause

NAT was incorrectly configured on R2 instead of R1.

### Resolution

* Removed NAT configuration from R2
* Configured NAT only on R1 (edge router)
* Marked serial interface on R1 as `ip nat inside`

---

## Issue 2: NAT not working for Branch traffic

### Problem

Branch traffic was not being translated.

### Root Cause

Serial interface on R1 was not configured as `ip nat inside`.

### Resolution

Configured:
interface s0/2/0
ip nat inside

---

## Issue 3: Missing return path

### Problem

ICMP request reached ISP but reply failed.

### Root Cause

Traffic was not NATed, so ISP could not route back to private IP.

### Resolution

Updated NAT ACL to include all internal networks.

