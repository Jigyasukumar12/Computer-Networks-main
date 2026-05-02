# UNIT 3: Network Layer

**Coverage:** Logical addressing, subnetting, routing, protocols (IP, ARP, ICMP), congestion control

---

## ⭐ TIER A TOPICS (High Priority - Appeared 3-4 Years)

---

## 1. IP Subnetting (Tier A - 4/4 Years)

**Frequency:** All 4 years (2021-22, 2022-23, 2023-24, 2024-25)  
**Expected Questions:** Divide network into subnets, CIDR notation, subnet mask calculation

### Definition

Subnetting divides a large IP address space into smaller, manageable networks. Each subnet can have independent routing and management.

### IP Address Classes

| Class | Range                       | Default Mask        | Host Bits | Subnet Bits | Use         |
| ----- | --------------------------- | ------------------- | --------- | ----------- | ----------- |
| **A** | 0.0.0.0 - 126.255.255.255   | 255.0.0.0 (/8)      | 24        | 8           | Large orgs  |
| **B** | 128.0.0.0 - 191.255.255.255 | 255.255.0.0 (/16)   | 16        | 16          | Medium orgs |
| **C** | 192.0.0.0 - 223.255.255.255 | 255.255.255.0 (/24) | 8         | 24          | Small orgs  |
| **D** | 224.0.0.0 - 239.255.255.255 | N/A                 | N/A       | N/A         | Multicast   |
| **E** | 240.0.0.0 - 255.255.255.255 | N/A                 | N/A       | N/A         | Research    |

### Subnet Mask (Netmask)

**Definition:** 32-bit number with 1s for network bits and 0s for host bits.

**Example:** 255.255.255.0 in binary = 11111111.11111111.11111111.00000000

- Means: First 24 bits are network, last 8 bits are host

### CIDR Notation (Classless Inter-Domain Routing)

**Format:** IP_address/prefix_length

**Example:** 192.168.1.0/24

- Means: 192.168.1.0 with 24 bits as network
- Subnet mask: 255.255.255.0
- Host bits: 32 - 24 = 8 bits
- Number of usable hosts: 2^8 - 2 = 254 (excluding network and broadcast)

### Solved PYQ Examples

**Example 1 (2021-22)**

_Q: Divide the network with IP address 200.1.2.0 into 5 subnets._

**Solution:**

**Given:** Network = 200.1.2.0, need 5 subnets

**Step 1:** Determine bits needed for 5 subnets

- 2^n ≥ 5 → n = 3 (need 3 bits)
- So subnet mask extends by 3 bits: /24 + 3 = /27

**Step 2:** Calculate subnet mask

- Original mask: /24 = 255.255.255.0
- New mask: /27 = 255.255.255.224 (224 = 11100000 in binary)

**Step 3:** Generate subnets

- Subnet bit patterns: 000, 001, 010, 011, 100, 101, 110, 111
- Increment = 256 / 8 = 32

| Subnet | Network Address | First Host  | Last Host   | Broadcast   |
| ------ | --------------- | ----------- | ----------- | ----------- |
| 1      | 200.1.2.0/27    | 200.1.2.1   | 200.1.2.30  | 200.1.2.31  |
| 2      | 200.1.2.32/27   | 200.1.2.33  | 200.1.2.62  | 200.1.2.63  |
| 3      | 200.1.2.64/27   | 200.1.2.65  | 200.1.2.94  | 200.1.2.95  |
| 4      | 200.1.2.96/27   | 200.1.2.97  | 200.1.2.126 | 200.1.2.127 |
| 5      | 200.1.2.128/27  | 200.1.2.129 | 200.1.2.158 | 200.1.2.159 |

(Remaining subnets 6, 7, 8 also available)

**Example 2 (2022-23)**

_Q: The IP network 200.198.160.0 is using subnet mask 255.255.255.224. Draw the subnets._

**Solution:**

**Given:** Network = 200.198.160.0, Mask = 255.255.255.224

**Step 1:** Find CIDR notation

- 255.255.255.224 in binary = 255.255.255.11100000
- Number of 1s = 24 + 3 = 27
- CIDR: /27

**Step 2:** Subnet bits = 3 (224 = 11100000, three 1s in last octet)

- Total subnets: 2^3 = 8
- Hosts per subnet: 2^(32-27) - 2 = 2^5 - 2 = 30

**Step 3:** Generate subnets (increment = 32)

| #   | Network            | Range               | Broadcast       |
| --- | ------------------ | ------------------- | --------------- |
| 0   | 200.198.160.0/27   | 200.198.160.1-30    | 200.198.160.31  |
| 1   | 200.198.160.32/27  | 200.198.160.33-62   | 200.198.160.63  |
| 2   | 200.198.160.64/27  | 200.198.160.65-94   | 200.198.160.95  |
| 3   | 200.198.160.96/27  | 200.198.160.97-126  | 200.198.160.127 |
| 4   | 200.198.160.128/27 | 200.198.160.129-158 | 200.198.160.159 |
| 5   | 200.198.160.160/27 | 200.198.160.161-190 | 200.198.160.191 |
| 6   | 200.198.160.192/27 | 200.198.160.193-222 | 200.198.160.223 |
| 7   | 200.198.160.224/27 | 200.198.160.225-254 | 200.198.160.255 |

**Example 3 (2024-25)**

_Q: A company is assigned the address block 192.168.10.0/24. Divide it into 4 subnets and specify subnet ranges._

**Solution:**

**Given:** 192.168.10.0/24, need 4 subnets

**Step 1:** Bits for 4 subnets

- 2^n ≥ 4 → n = 2
- New CIDR: /24 + 2 = /26

**Step 2:** Subnet mask = 255.255.255.192 (192 = 11000000)

**Step 3:** Increment = 256/4 = 64

| Subnet | Network           | Hosts              | Broadcast      |
| ------ | ----------------- | ------------------ | -------------- |
| 1      | 192.168.10.0/26   | 192.168.10.1-62    | 192.168.10.63  |
| 2      | 192.168.10.64/26  | 192.168.10.65-126  | 192.168.10.127 |
| 3      | 192.168.10.128/26 | 192.168.10.129-190 | 192.168.10.191 |
| 4      | 192.168.10.192/26 | 192.168.10.193-254 | 192.168.10.255 |

---

## 📘 TIER B TOPICS (Medium Priority)

---

## 2. Routing and Routing Algorithms (Tier B - 3/4 Years)

**Frequency:** 2021-22, 2023-24, 2024-25  
**Expected Questions:** Distance Vector Routing, Link State, count-to-infinity problem

### Routing Concept

**Definition:** Process of selecting paths for data packets to reach destination.

**Components:**

1. **Routing Table:** List of destinations and next-hop routers
2. **Routing Algorithm:** Determines which path to choose
3. **Routing Protocol:** Exchanges information between routers

### Static vs Dynamic Routing

| Feature         | Static                          | Dynamic                       |
| --------------- | ------------------------------- | ----------------------------- |
| **Setup**       | Manual by admin                 | Automatic by protocol         |
| **Adaptation**  | No                              | Adapts to network changes     |
| **Overhead**    | None                            | Uses bandwidth for updates    |
| **Scalability** | Poor (manual setup)             | Good (automatic)              |
| **Use**         | Small networks, specific routes | Large networks, ISP backbones |

---

## 3. Distance Vector Routing (DVR) (Tier B - 2/4 Years)

**Frequency:** 2021-22, 2024-25

### Concept

Each router maintains distance to every other router in vector format. Routers share vectors with neighbors; each updates based on neighbors' info.

**Algorithm:**

1. Initially, distance to self = 0, others = ∞
2. Periodically (or when link changes), send distance vector to neighbors
3. Neighbor receives vector, updates its own distances: D(i→j) = min(D(i→j), D(i→neighbor) + D(neighbor→j))
4. Update routing table with best path

**Solved PYQ Example (2024-25)**

_Q: For the following subnet, distance vector routing is used. Given vectors from B, D, E to router C: From B: (5,0,8,12,6,2); From D: (16,12,6,0,9,10); From E: (7,6,3,9,0,4). Measured delays to B, D, E are 6, 3, 5 respectively. Calculate C's new routing table._

**Solution:**

**Given:**

- C's distance to B = 6, to D = 3, to E = 5
- B's vector (to A,B,C,D,E,F): (5,0,8,12,6,2)
- D's vector: (16,12,6,0,9,10)
- E's vector: (7,6,3,9,0,4)

**Bellman-Ford equation:** D(C→X) = min over all neighbors Y of [D(C→Y) + D(Y→X)]

**Calculation for each destination:**

| Destination | Via B: 6+D_B | Via D: 3+D_D | Via E: 5+D_E | Min | Next-hop |
| ----------- | ------------ | ------------ | ------------ | --- | -------- |
| A           | 6+5=11       | 3+16=19      | 5+7=12       | 11  | B        |
| C           | 6+8=14       | 3+6=9        | 5+3=8        | 8   | E        |
| D           | 6+12=18      | 3+0=3        | 5+9=14       | 3   | D        |
| E           | 6+6=12       | 3+9=12       | 5+0=5        | 5   | E        |
| F           | 6+2=8        | 3+10=13      | 5+4=9        | 8   | B        |

**C's Routing Table:**

| Destination | Distance | Next-hop |
| ----------- | -------- | -------- |
| A           | 11       | B        |
| B           | 6        | B        |
| C           | 0        | -        |
| D           | 3        | D        |
| E           | 5        | E        |
| F           | 8        | B        |

---

## 4. Count-to-Infinity Problem (Tier B - 2/4 Years)

**Frequency:** 2022-23, 2024-25

### Problem Description

When a link fails in DVR, incorrect distance information propagates through network. Routers keep incrementing distance indefinitely (→ ∞).

**Example:**

Network: A---B---C (linear)

- Initial: C→A: A knows C is 2 hops away
- Link A-B fails
- **Problem:** C doesn't know link failed
- C→B→A : B doesn't have info
- C→B→C: B receives, says A is 3 hops (from C's vector 2 + B's guess 1)
- **Next iteration:** C thinks A is 4 hops (from B's vector 3 + C's distance to B 1)
- **Continues forever:** 4, 5, 6...∞

### Solutions

1. **Maximum Hop Count (Infinity = 16):**
   - Set max distance = 16 hops
   - After 16, declare destination unreachable
   - Limits worst-case to 16 iterations

2. **Split Horizon:**
   - Don't send route back to source
   - If B learned A from C, B doesn't tell C about A
   - Prevents immediate loops

3. **Poison Reverse:**
   - If B learned A from C, B tells C: "distance to A = ∞"
   - Forces C to stop using B for A
   - Solves 2-node loops immediately

**Solved PYQ Example (2024-25)**

_Q: Discuss how the count-to-infinity problem occurs in Distance Vector Routing. Suggest any one method to mitigate it._

**Answer Structure:**

1. **Problem explanation (3-4 lines):** When a link fails, routers keep updating with increasing distances indefinitely

2. **Example (2-3 lines):** Simple linear network, describe the problem

3. **Solution (2-3 lines):** Describe one method (max hop count, split horizon, poison reverse)

---

## 5. IPv4 Header Format (Tier B - 1/4 Years)

**Frequency:** 2023-24

### IPv4 Header Structure (20-60 bytes)

| Field                   | Size       | Purpose                                            |
| ----------------------- | ---------- | -------------------------------------------------- |
| **Version**             | 4 bits     | IPv4 = 4                                           |
| **IHL (Header Length)** | 4 bits     | In 32-bit words (5 = 20 bytes minimum)             |
| **DSCP/ToS**            | 8 bits     | Quality of service, priority                       |
| **Total Length**        | 16 bits    | Entire packet size (header + data)                 |
| **ID**                  | 16 bits    | Identifies fragments of same packet                |
| **Flags**               | 3 bits     | Reserved, Don't Fragment (DF), More Fragments (MF) |
| **Fragment Offset**     | 13 bits    | Position of fragment in original packet            |
| **TTL**                 | 8 bits     | Decremented by each router; packet dropped at 0    |
| **Protocol**            | 8 bits     | 6=TCP, 17=UDP, 1=ICMP, etc.                        |
| **Checksum**            | 16 bits    | Header error checking (recalculated at each hop)   |
| **Source IP**           | 32 bits    | Sender IP address                                  |
| **Destination IP**      | 32 bits    | Recipient IP address                               |
| **Options** (optional)  | 0-320 bits | Routing, timestamps, security                      |

---

## 6. IPv4 vs IPv6 (Tier B - 2/4 Years)

**Frequency:** 2022-23, 2024-25

### Comparison Table

| Feature           | IPv4                         | IPv6                                          |
| ----------------- | ---------------------------- | --------------------------------------------- |
| **Address Size**  | 32 bits                      | 128 bits                                      |
| **Notation**      | Dotted decimal (192.168.1.1) | Hex (2001:0db8:85a3:0000:0000:8a2e:0370:7334) |
| **Address Space** | 2^32 ≈ 4.3 billion           | 2^128 ≈ 3.4 × 10^38                           |
| **Header Size**   | 20-60 bytes (variable)       | 40 bytes (fixed)                              |
| **Fragmentation** | At routers                   | At source only                                |
| **Checksum**      | Present                      | Absent (relies on TCP/UDP)                    |
| **Options**       | In header                    | Extension headers                             |
| **Multicast**     | Optional                     | Built-in                                      |
| **Security**      | IPSec optional               | IPSec mandatory                               |
| **NAT**           | Widespread (workaround)      | Not needed                                    |
| **Deployment**    | 99% of internet              | ~5-10% adoption                               |

### Why IPv6?

1. **Address exhaustion:** IPv4 running out (allocated 99%+)
2. **Built-in security:** IPSec standard
3. **Better routing:** Simpler headers, faster processing
4. **Mobile support:** Better for mobile devices
5. **QoS:** Differentiated services simpler

---

## 7. ICMP (Internet Control Message Protocol) (Tier B - 2/4 Years)

**Frequency:** 2021-22, 2022-23

### Definition

ICMP allows routers and hosts to report network errors and perform diagnostics.

### ICMP Message Types

| Type | Name                    | Purpose                       |
| ---- | ----------------------- | ----------------------------- |
| 0    | Echo Reply              | Response to ping              |
| 3    | Destination Unreachable | Network/host/port unreachable |
| 5    | Redirect                | Inform better route available |
| 8    | Echo Request            | Ping request                  |
| 11   | Time Exceeded           | TTL expired (tracert)         |
| 12   | Parameter Problem       | Invalid header                |

### Common Uses

1. **Ping:** Send Echo Request (type 8), receive Echo Reply (type 0)
2. **Tracert:** Send packets with increasing TTL, receive Time Exceeded (type 11)
3. **Path MTU Discovery:** Determine max packet size without fragmentation

---

## 8. ARP / RARP / DHCP (Tier B - 1-2 Years)

**Frequency:** ARP: 2022-23; RARP/DHCP: 2024-25

### ARP (Address Resolution Protocol)

**Purpose:** Convert IP address → MAC address

**How it works:**

1. Sender broadcasts "Who has IP 192.168.1.5?"
2. Host with that IP responds "My MAC is 00:11:22:33:44:55"
3. Sender caches mapping in ARP table
4. Subsequent packets use MAC directly

### RARP (Reverse ARP)

**Purpose:** Convert MAC address → IP address (diskless machines)

**Use:** Diskless workstations request IP on boot

### DHCP (Dynamic Host Configuration Protocol)

**Purpose:** Automatically assign IP addresses

**Process:**

1. **Discover:** New host broadcasts "I need IP"
2. **Offer:** DHCP server offers IP address
3. **Request:** Host requests offered address
4. **Acknowledge:** Server confirms assignment

**Lease:** IP assignment temporary (24 hours to days), renewed automatically

---

## 9. Logical Addressing (Tier B - 1/4 Years)

**Frequency:** 2021-22

### Definition

IP addresses uniquely identify devices on a network. Different from physical (MAC) addresses.

**IP Address Structure:**

- 32-bit address divided into 4 octets
- Network portion + Host portion
- Network determined by subnet mask

---

## 10. Congestion Control Algorithms (Tier B - Implicit)

### Concept

When more packets arrive than router can process, packets queue and delay increases. Congestion control prevents and handles this.

### Algorithms

1. **Backpressure:** Receiver signals sender to slow down
2. **Choke Packet:** Router sends special packet signaling congestion
3. **Implicit Signaling:** Sender detects congestion from timeouts, packet loss
4. **Explicit Signaling:** Router marks packets (ECN: Explicit Congestion Notification)

---

## Exam Answer Tips (Unit 3)

### For Section A (2 marks):

- Define IP subnetting + 1 example
- List routing types or protocols
- Compare IPv4 vs IPv6 (2-3 points)
- **Time:** 2-3 min

### For Section B/C (10 marks):

- **Subnetting:** Provide 5-8 subnets with full address ranges
- **Routing:** Work through Bellman-Ford calculation with table
- **Count-to-infinity:** Explain problem + show example + solution
- **Protocol comparison:** IPv4 vs IPv6 table or DVR vs LSR
- **Time:** 10-12 min

### Common Section C Patterns:

1. **Subnetting with masks:** Calculate subnets, fill network address table
2. **Distance vector routing:** Calculate C's new routing table (like 2024-25 example)
3. **Count-to-infinity:** Explain problem, show iteration, name mitigation

### High-Scoring Tips:

- Always show calculation steps for subnetting
- Use table format for routing table (cleaner)
- Include CIDR notation in subnet answers
- Name specific solutions (split horizon, poison reverse)
- Binary representation for subnet masks in complex problems

---

**Study Checklist:**

- [ ] Subnet Class A, B, C network (1 example each)
- [ ] Calculate CIDR from subnet mask (10 examples)
- [ ] Distance vector routing calculation (5 examples)
- [ ] Count-to-infinity problem with solution (diagram)
- [ ] Explain ARP, RARP, DHCP in sequence
- [ ] IPv4 vs IPv6 comparison table
- [ ] ICMP message types and uses
- [ ] Routing table interpretation
