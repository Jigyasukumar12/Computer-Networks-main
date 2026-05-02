# UNIT 1: Introductory Concepts & Physical Layer

**Coverage:** Network fundamentals, OSI model, topology design, transmission media, and signal encoding

---

## ⭐ TIER A TOPICS (High Priority - Appeared 3-4 Years)

---

## 1. OSI Reference Model (Tier A - 4/4 Years)

**Frequency:** Appeared in all 4 years (2021-22, 2022-23, 2023-24, 2024-25)  
**Expected Questions:** Describe 7 layers, layer functions, data units at each layer, compare with TCP/IP

### Definition

The OSI (Open Systems Interconnection) reference model is a 7-layer framework standardized by ISO that defines how data is transmitted across networks. Each layer performs specific functions and communicates with adjacent layers.

### Detailed Explanation with All 7 Layers

| Layer | Name             | Function                                | Data Unit | Key Concepts                  |
| ----- | ---------------- | --------------------------------------- | --------- | ----------------------------- |
| **7** | **Application**  | User services, email, FTP, DNS, HTTP    | Message   | User interfaces, network apps |
| **6** | **Presentation** | Encryption, compression, formatting     | Data      | SSL/TLS, data conversion      |
| **5** | **Session**      | Dialogue control, connection management | Data      | SYN, ACK, session tokens      |
| **4** | **Transport**    | End-to-end delivery, TCP/UDP            | Segment   | Flow control, error handling  |
| **3** | **Network**      | Logical routing, IP addressing          | Packet    | Routing, forwarding, IP       |
| **2** | **Data Link**    | Physical addressing, MAC, framing       | Frame     | Switches, MAC address         |
| **1** | **Physical**     | Bits transmission, cables, signals      | Bit       | Cables, voltage levels, Hz    |

**Mnemonic:** "All People Seem To Need Data Processing" (Layer 7→1)

### Detailed Function Breakdown

**Layer 7 - Application Layer:**

- Provides network services directly to user applications
- Examples: Web browsers (HTTP), email (SMTP), file transfer (FTP), DNS, Telnet
- Services: Authentication, encryption support, data formatting
- Exam Focus: What protocols work here, how user requests convert to network requests

**Layer 6 - Presentation Layer:**

- Translates data formats between application and network
- Compression: Reduces data size (JPEG, MP3 compression)
- Encryption: Applies SSL/TLS security
- Character coding: Converts between ASCII, EBCDIC, Unicode
- Exam Focus: Encryption/decryption basics, data compression types

**Layer 5 - Session Layer:**

- Manages dialogs (conversations) between computers
- Establishes, maintains, terminates connections
- Synchronization: Sets sync points in data streams
- Example: Phone call setup/teardown, login sessions
- Exam Focus: Session establishment, keep-alive, graceful termination

**Layer 4 - Transport Layer:**

- Ensures end-to-end message delivery
- TCP: Reliable, connection-oriented, ordered delivery
- UDP: Fast, connectionless, no reliability guarantees
- Flow control: Prevents receiver from being overwhelmed
- Error handling: Detects and handles transmission errors
- Exam Focus: TCP vs UDP, port numbers, window size

**Layer 3 - Network Layer:**

- Routes data from source to destination across networks
- IP addressing: Assigns unique addresses (IPv4, IPv6)
- Routing protocols: Find optimal paths (RIP, OSPF, BGP)
- Forwarding: Moves packets from incoming to outgoing interface
- Switching techniques: Packet, circuit, message switching
- Exam Focus: Subnetting, routing algorithms, IP classes

**Layer 2 - Data Link Layer:**

- Frames data for transmission over physical medium
- MAC (Media Access Control): Manages access to shared media
- Physical addressing: Uses MAC addresses (48-bit)
- Error detection: CRC, parity bits
- Flow control: Manages frame-by-frame transfer
- Switching: Bridges and switches operate here
- Exam Focus: CRC calculation, MAC protocols, error detection

**Layer 1 - Physical Layer:**

- Transmits raw bits over physical medium
- Transmission media: Cables, fiber, wireless
- Encoding: Converts digital bits to signals (NRZ, Manchester)
- Modulation: Combines data with carrier signal
- Synchronization: Ensures sender and receiver clocks align
- Topology: Physical arrangement of network elements
- Exam Focus: Encoding types, transmission media, topology design

### Comparison: OSI vs TCP/IP Model

| Aspect          | OSI Model                                | TCP/IP Model                                      |
| --------------- | ---------------------------------------- | ------------------------------------------------- |
| **Layers**      | 7 layers                                 | 4 layers (Application, Transport, Internet, Link) |
| **Development** | ISO standard (1984)                      | DoD standard (1970s)                              |
| **Origin**      | Theory-driven                            | Practice-driven                                   |
| **Protocols**   | Generic (not tied to specific protocols) | Built around TCP/IP suite                         |
| **Adoption**    | Used in theory/teaching                  | Real-world internet standard                      |
| **Flexibility** | Less flexible, strict boundaries         | More flexible, overlapping functions              |

**TCP/IP Model Layers:** Application (FTP, SMTP, DNS, HTTP) → Transport (TCP, UDP) → Internet (IP, ICMP, IGMP) → Link (Ethernet, PPP, wireless)

### Solved PYQ Example (2023-24)

**Q: Describe all layers of the OSI model with a well-labeled diagram.**

**Answer Structure:** (This will score maximum marks with diagram)

_Introduction (2 lines):_ Define OSI as 7-layer framework for network communication.

_Explanation (Body):_

- Create diagram (see diagrams/OSI_model.svg)
- Describe each layer with 2-3 key points
- Mention data unit at each layer
- Show direction of data flow (downward at sender, upward at receiver)

_Layer Details:_

1. **Application Layer** - User applications request data (HTTP, FTP, SMTP, DNS)
2. **Presentation Layer** - Encrypts/compresses data for transmission (SSL, JPEG)
3. **Session Layer** - Manages connection sessions (SYN, ACK handshakes)
4. **Transport Layer** - TCP ensures reliability, UDP for speed (Port-based delivery)
5. **Network Layer** - Routes packets using IP addresses (Routing tables)
6. **Data Link Layer** - Creates frames with MAC addresses (Switches, CRC error checking)
7. **Physical Layer** - Transmits bits through cables/wireless (Voltage levels, encoding)

_Conclusion (1 line):_ Each layer adds headers (encapsulation) at sender, removes at receiver.

### Exam Answer Tips

- **Marks:** 10 marks typically
- **Diagram is mandatory:** Without diagram, max 5 marks
- **Draw bottom-up or top-down:** Show 7 distinct layers with proper spacing
- **Add data units:** Show "Message" at Layer 7, "Segment" at Layer 4, etc.
- **Include 1-2 examples per layer:** HTTP at Layer 7, TCP at Layer 4, IP at Layer 3
- **Time:** 8-10 minutes for full answer with diagram
- **Format:** Use a table for quick revision in exam

**Expected Answer Length:** 10-12 lines of text + 1 diagram (0.5 page)

---

## 2. Network Topologies (Tier A - 3/4 Years)

**Frequency:** Appeared in 2021-22, 2022-23, 2023-24  
**Expected Questions:** Draw topologies, advantages/disadvantages, mesh topology calculation, topology comparison

### Definition

A network topology is the physical or logical arrangement of network devices (nodes/hosts) and the interconnections between them. Physical topology is the actual cable layout; logical topology is how data flows.

### 6 Main Network Topologies

#### 1. **Mesh Topology**

- **Structure:** Every node connects to every other node
- **Connections:** Complete mesh = n(n-1)/2 links for n nodes
- **Advantages:**
  - ✓ Most redundant (fault-tolerant) - if one link fails, others work
  - ✓ No single point of failure
  - ✓ Parallel transmission possible
  - ✓ High security (dedicated links)
- **Disadvantages:**
  - ✗ Highest cost - many cables needed
  - ✗ Complex installation and maintenance
  - ✗ Difficult to add new nodes
  - ✗ Scaling problems
- **Use Case:** Military networks, critical infrastructure, backbone networks

#### 2. **Star Topology**

- **Structure:** All nodes connect to central hub/switch
- **Connections:** Linear = (n-1) links for n nodes
- **Advantages:**
  - ✓ Easy to install and manage
  - ✓ Easy to add/remove nodes
  - ✓ Minimal cable usage
  - ✓ Failure isolation (one failure doesn't affect others)
- **Disadvantages:**
  - ✗ Single point of failure (hub down = network down)
  - ✗ Hub becomes bottleneck
  - ✗ Central hub capacity limited
- **Use Case:** Most common in LANs (Ethernet networks, modern offices)

#### 3. **Ring Topology**

- **Structure:** Nodes connected in circular chain; each node has exactly 2 neighbors
- **Connections:** n links for n nodes
- **Data Flow:** Unidirectional (token ring) or bidirectional
- **Advantages:**
  - ✓ Equal access for all nodes (token-based)
  - ✓ Consistent performance (no congestion at one point)
  - ✓ Moderate cable cost
  - ✓ Easy to install cable run
- **Disadvantages:**
  - ✗ One failure breaks entire ring (unless dual-ring)
  - ✗ Adding/removing nodes disrupts network
  - ✗ Troubleshooting difficult
- **Use Case:** Token Ring (IBM), FDDI (Fiber Distributed Data Interface)

#### 4. **Bus Topology**

- **Structure:** All nodes connected to single shared cable (backbone)
- **Connections:** Linear chain
- **Access Method:** CSMA/CD (Collision detection)
- **Advantages:**
  - ✓ Simple, cheap installation
  - ✓ Minimal cable required
  - ✓ Easy to add nodes
- **Disadvantages:**
  - ✗ Single cable failure breaks network
  - ✗ Collision problems with many nodes
  - ✗ Performance degrades as nodes increase
  - ✗ Difficult to isolate faults
- **Use Case:** Legacy Ethernet (10BASE5, 10BASE2), coaxial cable networks

#### 5. **Tree (Hierarchical) Topology**

- **Structure:** Hybrid of star and bus; has root node, internal nodes, and leaf nodes
- **Connections:** n-1 links for n nodes
- **Advantages:**
  - ✓ Hierarchical organization
  - ✓ Easy expansion
  - ✓ Fault isolation possible
  - ✓ Scalable to large networks
- **Disadvantages:**
  - ✗ Heavy reliance on backbone
  - ✗ Root node is critical
  - ✗ Complex configuration
- **Use Case:** Large enterprise networks, WAN backbone

#### 6. **Point-to-Point (P2P) Topology**

- **Structure:** Direct connection between two nodes
- **Advantages:**
  - ✓ Highest speed and security
  - ✓ No contention
  - ✓ Easy to troubleshoot
- **Disadvantages:**
  - ✗ Limited to 2 nodes
  - ✗ Not scalable
  - ✗ High per-link cost
- **Use Case:** Leased lines, direct server connections, WAN links

### Solved PYQ Examples

**Example 1 (2024-25): Mesh Topology Calculation**

_Q: Determine the number of links needed for a fully connected mesh topology with 10 nodes._

**Solution:**
Formula: Links = n(n-1)/2, where n = number of nodes

For n = 10:
Links = 10 × 9 / 2 = 45 links

Each node connects to (n-1) = 9 other nodes.
Total connection points = 10 × 9 = 90
But each link connects 2 nodes, so: 90/2 = 45 links

**Answer: 45 links required**

**Example 2 (2023-24): Topology Comparison**

_Q: Differentiate between various topologies with well-labeled diagrams._

**Answer Structure:**
Create a comparison table:

| Topology | Structure      | # Links  | Best For       | Fault Tolerance |
| -------- | -------------- | -------- | -------------- | --------------- |
| Mesh     | Every to every | n(n-1)/2 | Military       | Excellent       |
| Star     | To hub         | n-1      | Modern LANs    | Good            |
| Ring     | Circular       | n        | Token passing  | Fair            |
| Bus      | Linear shared  | 1        | Legacy LANs    | Poor            |
| Tree     | Hierarchical   | n-1      | Large networks | Good            |
| P2P      | Direct pair    | 1        | Point links    | N/A             |

**Example 3 (2023-24): Mesh Topology Advantages/Disadvantages**

_Q: Write advantages and disadvantages of Mesh Topology._

**Answer:**
**Advantages:**

1. Fully redundant - any single link failure doesn't break network
2. Provides data security (dedicated private links between nodes)
3. Allows simultaneous data transmission (parallel paths)
4. High bandwidth availability
5. No single point of failure

**Disadvantages:**

1. Very expensive - requires n(n-1)/2 cables and interfaces
2. Installation and configuration extremely complex
3. Difficult to add or remove nodes (requires rewiring)
4. Power consumption high (each interface active)
5. Not practical for networks with many nodes
6. Maintenance overhead significant

### Exam Answer Tips

- **Marks:** 8-10 marks typically
- **Diagram is MANDATORY:** Required for each topology - draw neat boxes and connecting lines
- **Include 5+ topologies:** Don't skip any
- **Add pros/cons:** At least 3 each
- **Use table format:** For comparison questions, table scores better than prose
- **Time:** 12-15 minutes with neat diagrams
- **Common trick:** Question might ask mesh topology with 8 nodes (calculate 28 links)

---

## 📘 TIER B TOPICS (Medium Priority - Appeared 2-3 Years)

---

## 3. TCP/IP Protocol Suite Model (Tier B - 2/4 Years)

**Frequency:** 2022-23, 2023-24  
**Expected Questions:** Explain TCP/IP model, compare with OSI

### Definition

TCP/IP model is a 4-layer framework (Application, Transport, Internet, Link) on which the modern internet is based. It is less formal but more practical than OSI model.

### 4 Layers of TCP/IP Model

| Layer | Name            | Protocols                                 | Functions                               |
| ----- | --------------- | ----------------------------------------- | --------------------------------------- |
| **4** | **Application** | HTTP, HTTPS, FTP, SMTP, DNS, Telnet, SNMP | User services, data formatting          |
| **3** | **Transport**   | TCP (reliable), UDP (fast)                | End-to-end delivery, flow control       |
| **2** | **Internet**    | IP, ICMP, IGMP, ARP                       | Routing, logical addressing, forwarding |
| **1** | **Link**        | Ethernet, PPP, 802.11 (WiFi), DSL         | Physical transmission, MAC addressing   |

### OSI vs TCP/IP Comparison Table

| Feature                  | OSI (7-layer)         | TCP/IP (4-layer)            |
| ------------------------ | --------------------- | --------------------------- |
| **Layers**               | 7 layers              | 4 layers                    |
| **Model Type**           | Theoretical/Standard  | Practical/Real-world        |
| **Development**          | ISO standard          | Military DoD standard       |
| **Popularity**           | Teaching/concepts     | Internet standard           |
| **Presentation/Session** | Separate layers       | Merged into Application     |
| **Flexibility**          | Strict layering       | Loose boundaries            |
| **Protocol Binding**     | Not protocol-specific | Built around TCP/IP         |
| **Adoption**             | Limited in practice   | Universal (entire internet) |

---

## 4. Network Devices (Tier B - 2/4 Years)

**Frequency:** 2022-23, 2023-24  
**Expected Questions:** Name and explain network devices on each OSI layer

### Network Devices by Layer

| Layer         | Devices                                            | Function                               |
| ------------- | -------------------------------------------------- | -------------------------------------- |
| **Layer 7**   | Gateway, Proxy Server                              | Convert protocols, filter content      |
| **Layer 5-6** | Gateway, Load Balancer                             | Session management, data conversion    |
| **Layer 4**   | Firewall, Load Balancer                            | Port filtering, connection management  |
| **Layer 3**   | Router, Layer-3 Switch, Gateway                    | IP routing, forwarding                 |
| **Layer 2**   | Switch, Bridge, MAC Bridge                         | Frame forwarding via MAC address       |
| **Layer 1**   | Repeater, Hub, Modem, Network Interface Card (NIC) | Signal amplification, bit transmission |

### Device Details

**Repeater:** Regenerates weak signals; operates at Layer 1 (Physical)
**Hub:** Connects multiple devices; broadcasts to all ports (Layer 1)
**Bridge:** Filters frames based on MAC address (Layer 2); learning bridge maintains MAC table
**Switch:** Intelligent bridge; creates VLAN, checks MAC table for port forwarding (Layer 2)
**Router:** Routes packets using IP address and routing table (Layer 3); can be Layer-3 switch
**Gateway:** Converts between different protocols; operates at higher layers (Layer 5-7)

---

## 5. Signal Transmission and Encoding (Tier B - 2/4 Years)

**Frequency:** 2021-22, 2022-23  
**Expected Questions:** Explain encoding types (NRZ, Manchester, Differential Manchester)

### Encoding Types (Converts Binary 0,1 to Voltage Levels)

#### 1. **NRZ-L (Non-Return-to-Zero Level)**

- **Encoding:** 0 = Low voltage, 1 = High voltage
- **Advantage:** Simple
- **Disadvantage:** Loses synchronization if long string of 0s or 1s (receiver clock drifts)
- **Example:** Binary 01001110 → voltage pattern (high-low-low-low-high-high-high-low)

#### 2. **NRZ-I (Non-Return-to-Zero Inverted)**

- **Encoding:** 0 = No change in voltage, 1 = Change voltage level (flip)
- **Advantage:** Better at maintaining clock synchronization than NRZ-L
- **Disadvantage:** Still loses sync on long 0s
- **Example:** For 01001110 → (start low: L-L-H-H-L-L-L-H)

#### 3. **Manchester Encoding**

- **Encoding:** Each bit represented by 2 transitions: 0 = Low-High, 1 = High-Low
- **Advantage:** Self-clocking; always has transition in middle (maintains sync perfectly)
- **Disadvantage:** Requires twice the bandwidth (2 levels per bit)
- **Use:** Ethernet (10BASE-T)
- **Example:** 01 → (High-Low, Low-High) on signal

#### 4. **Differential Manchester**

- **Encoding:** 0 = Transition at start, 1 = No transition at start; always transition at middle
- **Advantage:** Better than Manchester for noise immunity
- **Disadvantage:** Most complex, highest bandwidth
- **Use:** Token Ring

### Solved PYQ Example (2022-23)

_Q: Construct the Polar NRZ-L and NRZ-I schemes for the following Data: 01001110_

**Solution:**

**NRZ-L:** (0=Low, 1=High)

```
0   1   0   0   1   1   1   0
L   H   L   L   H   H   H   L
```

**NRZ-I:** (0=No change, 1=Change/Flip)
Starting with Low voltage:

```
0        1        0        0        1        1        1        0
(No    (Change  (No    (No    (Change  (No    (No    (Change
change)  to H)   change) change) to L)   change) change) to H)
L       H        H        H        L        L        L        H
```

---

## 6. Transmission Impairments (Tier B - 1/4 Years)

**Frequency:** 2022-23  
**Expected Questions:** Explain network performance and transmission impairments

### Types of Transmission Impairments

1. **Attenuation:** Signal strength decreases with distance (measured in dB)
   - Causes: Resistance in cable, absorption in medium
   - Solution: Repeaters to regenerate signal

2. **Distortion:** Signal shape changes during transmission
   - Causes: Different frequency components travel at different speeds
   - Solution: Equalization, error correction

3. **Noise:** Unwanted signals mixed with data
   - Thermal noise: Random motion of electrons
   - Crosstalk: Signal bleeding from adjacent cables
   - Impulse noise: Sudden spikes (lightning, switching)
   - Solution: Error correction, shielding, filtering

4. **Delay Distortion (Dispersion):** Different frequencies arrive at different times
   - Causes: Medium properties vary with frequency
   - Solution: Bandwidth limitation, fiber optics

### Solved PYQ Example (2024-25)

_Q: A signal is transmitted with an initial power of 2W and experiences an attenuation of -3 dB. Calculate the received power._

**Solution:**

**Formula:** Attenuation (dB) = 10 log₁₀(P_out / P_in)

Given:

- Initial power P_in = 2W
- Attenuation = -3 dB

Calculation:
-3 = 10 log₁₀(P_out / 2)
-0.3 = log₁₀(P_out / 2)
10^(-0.3) = P_out / 2
0.501 = P_out / 2
**P_out = 1.002 W ≈ 1 W**

---

## 7. Bit Rate vs Baud Rate (Tier B - 1/4 Years)

**Frequency:** 2022-23

### Definition

**Baud Rate:** Number of signal changes per second (symbols/sec)

- Unit: Baud (Bd)
- Formula: Baud Rate = 1 / Bit Duration

**Bit Rate:** Number of bits transmitted per second (bits/sec)

- Unit: bits/second (bps)
- Formula: Bit Rate = Baud Rate × Log₂(N), where N = number of levels

### Comparison

| Aspect         | Baud Rate                 | Bit Rate                         |
| -------------- | ------------------------- | -------------------------------- |
| **Definition** | Signal changes per second | Bits transmitted per second      |
| **Symbol**     | Bd                        | bps                              |
| **Relation**   | Br = Bd × log₂(M)         | --                               |
| **Example**    | 1 signal change = 1 Baud  | 2 bits = 1 signal change = 2 bps |

### Example Calculation

If Baud Rate = 1000 Bd and we use 16 levels (4 bits per level):

- Bit Rate = 1000 × log₂(16) = 1000 × 4 = **4000 bps**

---

## 8. Transmission Media (Tier B - 1/4 Years)

**Frequency:** 2021-22  
**Expected Questions:** Discuss about transmission mediums in networking

### Guided Media (Physical cables)

1. **Twisted Pair (TP):**
   - Two insulated copper wires twisted around each other
   - **UTP (Unshielded):** No shield, cheaper, susceptible to interference
   - **STP (Shielded):** Metal foil shield, better protection
   - **Use:** Ethernet (Cat 5e, Cat 6, Cat 8), telephone lines
   - **Distance:** Up to 100 meters
   - **Bandwidth:** 10 Mbps (UTP Cat 3) to 40 Gbps (Cat 8)
   - **Cost:** Cheapest
   - **Installation:** Easiest

2. **Coaxial Cable:**
   - Central conductor surrounded by insulation and outer conductor mesh
   - **Use:** Cable TV, older Ethernet (10BASE5, 10BASE2)
   - **Distance:** Longer than TP (500m for 10BASE5)
   - **Bandwidth:** Medium (10 Mbps for Ethernet)
   - **Cost:** Moderate
   - **Advantage:** Better immunity to interference than UTP

3. **Fiber Optic:**
   - Glass/plastic strands transmit light pulses
   - **Single Mode:** Small core (~8 μm), long distance, expensive
   - **Multi Mode:** Large core (~50 μm), short distance, cheaper
   - **Use:** High-speed backbone, long-distance (intercontinental)
   - **Distance:** 100s of kilometers without repeater
   - **Bandwidth:** Highest (Terabits/sec)
   - **Advantage:** Immune to electromagnetic interference, secure
   - **Disadvantage:** Most expensive, requires special connectors (SC, ST, LC)

### Unguided Media (Wireless)

1. **Radio Waves:**
   - Frequency: 1 MHz - 1000 MHz
   - Range: Few meters to kilometers
   - Use: Cellular, WiFi (802.11), Bluetooth short range
   - Advantage: Mobility
   - Disadvantage: Interference, security

2. **Microwave:**
   - Frequency: 1 GHz - 40 GHz
   - Range: Long distance (line-of-sight)
   - Use: Satellite communication, backhaul links
   - Advantage: Point-to-point, long distance
   - Disadvantage: Expensive, requires clear path

3. **Infrared:**
   - Frequency: THz range
   - Range: Very short (room distance)
   - Use: TV remote, laser communication
   - Advantage: Secure, high speed
   - Disadvantage: Blocked by obstacles

---

## 9. Network Performance Metrics (Tier B - 1/4 Years)

**Frequency:** 2021-22

### Key Performance Metrics

1. **Bandwidth:** Maximum data transmission rate (bits/sec)
   - Measured: Gbps, Mbps, kbps
   - Network bandwidth limited by slowest link

2. **Latency (Delay):** Time for data to travel from source to destination
   - **Propagation Delay:** Distance / Speed of signal
   - **Transmission Delay:** Packet size / Bandwidth
   - **Processing Delay:** Router processing time
   - **Queuing Delay:** Wait time in buffer
   - **Total Latency:** Sum of all above

3. **Throughput:** Actual data transmission rate (often less than bandwidth)
   - Affected by latency, packet loss, retransmissions

4. **Packet Loss Rate:** Percentage of packets dropped
   - Caused by: Buffer overflow, corruption
   - Affects: Quality of service

### Solved PYQ Example (2021-22)

_Q: Assume we want to send data from S to R and there are 2 routers in between. What will be the total time taken if total number of packets are 5? Data: Tp=0 ms, Data size=1000 bytes, BW=1 Mbps, Header=100 bytes_

**Solution:**

**Formula:** Total Time = Transmission Delay + Propagation Delay + Processing Delay

For each packet:

- Total size = Data (1000) + Header (100) = 1100 bytes = 8800 bits
- Transmission Delay (Tt) = 8800 bits / 1,000,000 bps = 8.8 ms

With 5 packets and pipelined transmission:

- First packet: Tt = 8.8 ms
- Next 4 packets arrive every 8.8 ms (no additional delay as propagation is 0)
- **Total Time for 5 packets = 8.8 × 5 = 44 ms**

Or with routers:

- Time at S: 8.8 ms
- Propagation to R1: 0 ms (Tp=0)
- Processing at R1: ~1 ms (if given)
- Time at R1 to send to R2: 8.8 ms
- Time at R2 to send to R: 8.8 ms
- **Total for single packet ≈ 26.4 ms**
- **For 5 packets pipelined ≈ 26.4 + 4×8.8 = 61.6 ms**

---

## Exam Answer Tips (Unit 1)

### For Short Questions (Section A - 2 marks):

- **Definition (1 line)** + Key points (3-4 bullet points)
- Example: Mesh topology = "Every node connects to every other node (n(n-1)/2 links). Advantages: Redundant, secure. Disadvantages: Expensive, complex."
- **Time:** 2-3 minutes

### For Long Questions (Section B/C - 10 marks):

- **Introduction (2 lines):** Define topic
- **Explanation (6-8 lines):** Detailed points, examples
- **Diagram (0.5 page):** Well-labeled, neat
- **Conclusion (1 line):** Summary
- **Time:** 10-12 minutes

### Mandatory Elements for Each Topic:

- [ ] **OSI Model:** 7-layer diagram with data units and device examples
- [ ] **Topologies:** All 6 types with structure, advantages, disadvantages
- [ ] **Encoding:** Show conversion from binary to voltage for all 4 types
- [ ] **Transmission Media:** Comparison table (cable type, distance, bandwidth, cost)

### High-Scoring Strategy:

1. **Always draw diagrams:** Worth 3-4 marks alone
2. **Use tables for comparison:** Cleaner, more professional
3. **Include formulas:** For calculations (mesh links, delay, attenuation)
4. **Add real-world examples:** Ethernet for Star topology, cable TV for coax
5. **Label everything:** Diagram titles, axis labels, color/shading

---

**Study Checklist:**

- [ ] Draw OSI model 7 layers from memory without notes
- [ ] Name advantages/disadvantages of 6 topologies
- [ ] Calculate mesh links for n=8,10,12 nodes
- [ ] Explain NRZ-L and NRZ-I for 5-bit binary string
- [ ] Compare TCP/IP with OSI (5+ differences)
- [ ] Solve 2 signal attenuation problems
- [ ] Define Baud rate and Bit rate with examples
