# Hands-on Lab 2.1: IPv4 Subnetting Exercise

---

## Lab Overview

| Property | Value |
|----------|-------|
| **Objective** | Calculate subnet masks, network addresses, and usable host ranges for various network scenarios |
| **Time Required** | 30-45 minutes |
| **Difficulty** | Intermediate (I) |
| **Related Section** | Chapter 2, Section 2.2 |

---

## Prerequisites

Before starting this lab, you should have:

- [x] Completed Section 2.2: IP Addressing and Subnetting
- [x] Understanding of binary-to-decimal conversion
- [x] Familiarity with IP address classes and CIDR notation

---

## Environment Setup

**Required Tools:**

| Component | Requirement | Notes |
|-----------|-------------|-------|
| Calculator | Any scientific calculator or Windows Calculator in Programmer mode | For binary calculations |
| Paper and Pen | For working through calculations | Recommended for exam practice |
| Subnet Calculator (optional) | Online or offline tool | For verification only |

**Alternative Environment:**
- Any device with a calculator application
- Packet Tracer or GNS3 for practical verification (optional)

---

## Lab Steps

### Part 1: Basic Subnetting

#### Step 1: Calculate Subnet Requirements

**Given Network**: 192.168.10.0/24

**Scenario**: An organization needs to divide this network into 4 equal subnets for different departments:
- Subnet 1: Human Resources
- Subnet 2: Finance
- Subnet 3: IT Operations
- Subnet 4: Guest Network

**Instruction**: Calculate the new subnet mask needed.

**Your Calculation**:
```
Original network: 192.168.10.0/24
Subnets needed: 4
Bits to borrow: 2^n ≥ 4, so n = 2
New prefix: 24 + 2 = /26
New subnet mask: 255.255.255.192
```

**Expected Result**: Subnet mask is /26 or 255.255.255.192

---

#### Step 2: Determine Subnet Ranges

**Instruction**: Calculate the network address, first host, last host, and broadcast for each subnet.

**Subnet Increment**: 256 - 192 = 64

**Your Calculation**:

| Subnet | Network Address | First Host | Last Host | Broadcast |
|--------|-----------------|------------|-----------|-----------|
| HR | 192.168.10.0 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 |
| Finance | 192.168.10.64 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| IT Ops | 192.168.10.128 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 |
| Guest | 192.168.10.192 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 |

**Expected Result**: Four complete subnet ranges with 62 usable hosts each

---

#### Step 3: Calculate Usable Hosts

**Instruction**: Determine the number of usable host addresses per subnet.

**Your Calculation**:
```
Host bits = 32 - 26 = 6
Total addresses = 2^6 = 64
Usable hosts = 64 - 2 = 62 per subnet
```

**Expected Result**: 62 usable host addresses per subnet

---

### Part 2: Variable Length Subnet Masking (VLSM)

#### Step 4: VLSM Scenario

**Given Network**: 172.16.0.0/16

**Requirements**:
- Network A: 2,000 hosts (Data Center)
- Network B: 500 hosts (Main Office)
- Network C: 100 hosts (Branch 1)
- Network D: 50 hosts (Branch 2)
- Network E: 2 hosts (Point-to-Point Link)

**Instruction**: Design a VLSM addressing scheme starting with the largest requirement.

**Your Calculation**:

**Network A (2,000 hosts)**:
```
2^n - 2 ≥ 2000
2^11 - 2 = 2046 ✓
Host bits needed: 11
Prefix: 32 - 11 = /21
Network: 172.16.0.0/21
Range: 172.16.0.1 - 172.16.7.254
Broadcast: 172.16.7.255
Next available: 172.16.8.0
```

**Network B (500 hosts)**:
```
2^9 - 2 = 510 ✓
Prefix: /23
Network: 172.16.8.0/23
Range: 172.16.8.1 - 172.16.9.254
Broadcast: 172.16.9.255
Next available: 172.16.10.0
```

**Network C (100 hosts)**:
```
2^7 - 2 = 126 ✓
Prefix: /25
Network: 172.16.10.0/25
Range: 172.16.10.1 - 172.16.10.126
Broadcast: 172.16.10.127
Next available: 172.16.10.128
```

**Network D (50 hosts)**:
```
2^6 - 2 = 62 ✓
Prefix: /26
Network: 172.16.10.128/26
Range: 172.16.10.129 - 172.16.10.190
Broadcast: 172.16.10.191
Next available: 172.16.10.192
```

**Network E (2 hosts - point-to-point)**:
```
2^2 - 2 = 2 ✓
Prefix: /30
Network: 172.16.10.192/30
Range: 172.16.10.193 - 172.16.10.194
Broadcast: 172.16.10.195
```

**Expected Result**: Complete VLSM scheme with no overlapping addresses

---

### Part 3: Exam-Style Problems

#### Step 5: Quick Calculation Practice

Complete the following calculations:

**Problem 1**: How many hosts in a /27 network?
```
Host bits: 32 - 27 = 5
Usable hosts: 2^5 - 2 = 30
```

**Problem 2**: What subnet mask creates 8 subnets from a Class C network?
```
2^3 = 8 subnets
Bits borrowed: 3
New mask: /24 + 3 = /27
Subnet mask: 255.255.255.224
```

**Problem 3**: Host 10.45.67.89/22 - What is the network address?
```
/22 = 255.255.252.0
Network boundary at: 4 (256-252)
67 / 4 = 16.75 → Floor to 16 → 16 * 4 = 64
Network address: 10.45.64.0/22
```

**Problem 4**: Is 192.168.15.255/20 a valid host address?
```
/20 = 255.255.240.0
Network boundary at: 16 (256-240)
15 / 16 = 0.9375 → Floor to 0 → Network: 192.168.0.0
Broadcast: 192.168.15.255
Answer: No, this is the broadcast address
```

**Expected Result**: All four problems solved correctly

---

#### Step 6: Verification (Optional)

**Instruction**: If available, verify your calculations using:
- An online subnet calculator
- Packet Tracer network simulation
- Windows ipconfig /all on configured devices

---

## Validation Checklist

Verify your lab is complete by checking all boxes:

- [ ] Correctly calculated /26 subnet mask for 4-subnet requirement
- [ ] Identified all four subnet ranges with network, first/last host, and broadcast
- [ ] Calculated 62 usable hosts per /26 subnet
- [ ] Completed VLSM scheme without overlapping addresses
- [ ] Solved all four exam-style problems correctly

**Lab Complete**: All boxes should be checked before proceeding.

---

## Troubleshooting Guide

| Issue | Possible Cause | Solution |
|-------|----------------|----------|
| Wrong subnet count | Incorrect bit calculation | Remember: 2^n = number of subnets |
| Wrong host count | Forgot to subtract 2 | Always subtract 2 (network + broadcast) |
| Overlapping VLSM subnets | Started new subnet at wrong address | Use broadcast + 1 as next network |
| Wrong network address | Binary boundary error | Convert to binary and zero out host bits |
| Broadcast calculation error | Added hosts incorrectly | Broadcast = Network + (Total addresses - 1) |

---

## Lab Cleanup

After completing the lab, clean up your environment:

1. Review any incorrect calculations and understand errors
2. Practice similar problems until comfortable
3. Time yourself on exam-style problems (target: 2 min per problem)

---

## Key Learning Points

From this lab, you should understand:

1. **Subnetting is about borrowing bits**: The number of bits borrowed determines subnets; remaining bits determine hosts
2. **VLSM enables efficient address allocation**: Always start with largest requirement to minimize waste
3. **Network and broadcast addresses are reserved**: Total hosts = 2^n - 2

---

## Challenge Extension (Optional)

For additional practice, try:

- Given 10.0.0.0/8, design a scheme for: 100 sites with 500 hosts each, 200 sites with 50 hosts each, and 1000 point-to-point links
- Identify which IP addresses are in the same subnet: 172.30.128.57/21 and 172.30.135.201/21

---

**Lab Status**: Complete
**Last Updated**: 2026-02-01
**Tested On**: Pen and paper, verified with subnet calculator
