# UNIT 4: Transport Layer

**Coverage:** TCP, UDP, connection management, flow control, congestion control, QoS

---

## ⭐ TIER A TOPICS (High Priority - Appeared 3-4 Years)

---

## 1. TCP vs UDP (Tier A - 3/4 Years)

**Frequency:** 2021-22, 2022-23, 2023-24  
**Expected Questions:** Detailed comparison, when to use each, header format comparison

### Definition

**TCP (Transmission Control Protocol):** Connection-oriented, reliable, ordered delivery of data. Ensures no packet loss.

**UDP (User Datagram Protocol):** Connectionless, unreliable, fast delivery. Packets may be lost/reordered.

### Detailed Comparison Table

| Feature                | TCP                                           | UDP                             |
| ---------------------- | --------------------------------------------- | ------------------------------- |
| **Connection**         | Establishes connection (3-way handshake)      | No connection setup             |
| **Reliability**        | Guaranteed delivery (with ACK/retransmission) | No guarantee, may lose packets  |
| **Ordering**           | Packets arrive in order (sequence numbers)    | No ordering guarantee           |
| **Speed**              | Slower (overhead of reliability)              | Faster (minimal overhead)       |
| **Header Size**        | 20-60 bytes                                   | 8 bytes (minimal)               |
| **Flow Control**       | Yes (sliding window)                          | No                              |
| **Error Checking**     | Full checksum                                 | Checksum (optional)             |
| **Broadcasting**       | No                                            | Yes (can broadcast to multiple) |
| **Use Cases**          | File transfer, email, web (HTTP)              | Streaming, gaming, VoIP, DNS    |
| **Port Numbers**       | Well-known ports (80=HTTP, 443=HTTPS)         | DNS (53), NTP (123), SNMP (161) |
| **Congestion Control** | Yes (TCP congestion control)                  | No                              |
| **Resource Usage**     | High (maintains connection state)             | Low                             |
| **Complexity**         | Complex implementation                        | Simple implementation           |

### TCP Header Format (20-60 bytes)

```
0               8              16              24              31
+-------+-------+-------+-------+-------+-------+-------+-------+
|          Source Port (16)            |       Dest Port (16)  |
+-------+-------+-------+-------+-------+-------+-------+-------+
|                    Sequence Number (32)                       |
+-------+-------+-------+-------+-------+-------+-------+-------+
|                  Acknowledgment Number (32)                   |
+-------+-------+-------+-------+-------+-------+-------+-------+
|  HL   | Res  |C|E|U|A|P|R|S|F|        Window Size (16)        |
+-------+-------+-------+-------+-------+-------+-------+-------+
|         Checksum (16)           |      Urgent Pointer (16)   |
+-------+-------+-------+-------+-------+-------+-------+-------+
|                    Options (variable)                         |
+-------+-------+-------+-------+-------+-------+-------+-------+
```

**Field Descriptions:**

1. **Source Port (16 bits):** Sending port (1024-65535 for client)
2. **Destination Port (16 bits):** Receiving port (well-known: 1-1023)
3. **Sequence Number (32 bits):** Byte sequence number of data in segment
4. **Acknowledgment Number (32 bits):** Expected sequence number from other side
5. **Header Length (4 bits):** Length in 32-bit words (5 = 20 bytes minimum)
6. **Flags (9 bits):**
   - C (Congestion): Congestion window reduced
   - E (ECN-Echo): ECN echo flag
   - U (Urgent): Urgent data present
   - A (ACK): Acknowledgment valid
   - P (Push): Push function
   - R (Reset): Reset connection
   - S (Syn): Synchronization (connection start)
   - F (Fin): Finish (connection end)
7. **Window Size (16 bits):** Receiver advertises buffer space (flow control)
8. **Checksum (16 bits):** Error detection (mandatory)
9. **Urgent Pointer (16 bits):** Offset to urgent data (if U flag set)
10. **Options (variable):** MSS, window scaling, timestamps, SACK

### UDP Header Format (8 bytes - Minimal)

```
0               8              16              24              31
+-------+-------+-------+-------+-------+-------+-------+-------+
|          Source Port (16)            |       Dest Port (16)  |
+-------+-------+-------+-------+-------+-------+-------+-------+
|         Length (16)              |        Checksum (16)     |
+-------+-------+-------+-------+-------+-------+-------+-------+
```

**UDP Fields:**

- **Source Port:** Sending port
- **Destination Port:** Receiving port
- **Length:** Entire UDP segment (header + data)
- **Checksum:** Optional (set to 0 if not used)

### Solved PYQ Examples

**Example 1 (2021-22)**

_Q: Write detailed note on "TCP vs UDP"._

**Answer Structure:**

**Introduction:** TCP and UDP are Layer 4 (Transport) protocols with different philosophies. TCP prioritizes reliability; UDP prioritizes speed.

**TCP - Reliable Transport:**

1. Connection-oriented (3-way handshake)
2. Guarantees delivery via ACK/retransmission
3. Maintains sequence numbers for ordering
4. Flow control using sliding window
5. Congestion control mechanisms
6. Used for: HTTP/HTTPS, FTP, SMTP, SSH, Telnet

**UDP - Fast Transport:**

1. Connectionless (no handshake)
2. No delivery guarantee (fire-and-forget)
3. No sequence/ordering
4. No flow control (can overwhelm receiver)
5. No congestion control (floods network if possible)
6. Used for: DNS, VoIP, Gaming, Video streaming, NTP

**Header Comparison:**

- TCP: 20+ bytes with many fields
- UDP: 8 bytes minimal overhead

**When to Choose:**

- **TCP:** When data integrity crucial (banking, email, file transfer)
- **UDP:** When speed matters more than completeness (real-time video, gaming)

**Example 2 (2023-24)**

_Q: Differentiate TCP and UDP in context of the header format._

**Answer:**

| Aspect             | TCP                                | UDP                         |
| ------------------ | ---------------------------------- | --------------------------- |
| **Size**           | 20-60 bytes                        | 8 bytes                     |
| **Sequence #**     | Yes (32-bit)                       | No                          |
| **ACK #**          | Yes (32-bit)                       | No                          |
| **Checksum**       | Mandatory                          | Optional                    |
| **Flags**          | 9 flags (SYN, ACK, FIN, RST, etc.) | None                        |
| **Window**         | Yes (flow control)                 | No                          |
| **Urgent Pointer** | Yes                                | No                          |
| **Port fields**    | Source + Dest (16-bit each)        | Source + Dest (16-bit each) |

---

## 📘 TIER B TOPICS (Medium Priority)

---

## 2. TCP Connection Management (Tier B - 2/4 Years)

**Frequency:** 2023-24, 2024-25  
**Expected Questions:** 3-way handshake, connection states, closing sequence

### TCP Connection States

```
LISTEN ──SYN──→ SYN_RECEIVED ──ACK──→ ESTABLISHED
                                              ↓
                                          (data transfer)
                                              ↓
                                         FIN_WAIT_1
                                              ↓
                                         CLOSE_WAIT
```

### 3-Way Handshake (Connection Establishment)

**Step 1: SYN (Synchronization)**

- Client sends TCP segment with SYN flag = 1, Seq = x
- Client state: SYN_SENT

**Step 2: SYN-ACK (Server response)**

- Server sends TCP segment with SYN = 1, ACK = 1
- Seq = y, ACK # = x+1
- Server state: SYN_RECEIVED

**Step 3: ACK (Client acknowledgment)**

- Client sends TCP segment with ACK = 1
- Seq = x+1, ACK # = y+1
- Both in ESTABLISHED state

**Why 3-way?**

- Step 1: Client tells server "I'm here" (x)
- Step 2: Server tells client "I heard you" (confirms x+1) and "Here's my seq" (y)
- Step 3: Client tells server "I heard you" (confirms y+1)
- **No ambiguity:** Both sides confirmed both directions work

### Connection Termination (Graceful Shutdown)

**Step 1: FIN from client**

- Client sends FIN flag = 1
- Client state: FIN_WAIT_1

**Step 2: ACK from server**

- Server acknowledges FIN
- Server state: CLOSE_WAIT
- Client state: FIN_WAIT_2

**Step 3: FIN from server**

- Server sends FIN flag = 1
- Server state: LAST_ACK

**Step 4: ACK from client**

- Client sends ACK
- Client state: TIME_WAIT
- Server state: CLOSED

**TIME_WAIT:** Client waits 2×MSL (Maximum Segment Lifetime) to handle delayed packets

### Solved PYQ Example (2023-24)

_Q: Define Connection Management. Explain how Three-way handshaking using diagram._

**Answer:**

**Definition:** Connection management handles TCP connection setup (establishment), data transfer, and termination (graceful close) to ensure reliable communication.

**3-Way Handshake Diagram:**

```
Client (Active Open)          |          Server (Passive Open)

SYN_SENT    ──SYN(seq=x)───→  |  LISTEN
                               |
                              SYN_RECEIVED
           ←──SYN-ACK(seq=y, ack=x+1)──┐
                               |
ESTABLISHED ──ACK(seq=x+1, ack=y+1)──→ |
                               |     ESTABLISHED
                (Connection established)
```

**Why Needed:**

1. **Seq synchronization:** Both sides agree on starting sequence numbers
2. **Resource allocation:** Both sides allocate buffers
3. **Parameter negotiation:** Agree on window size, MSS, options
4. **Reliability:** Confirm both directions functional

---

## 3. TCP Congestion Control (Tier B - 2/4 Years)

**Frequency:** 2022-23, 2023-24

### Concept

When network congested (packet loss, timeout), TCP reduces sending rate. When network clear, increases rate.

### Congestion Window (cwnd)

**Definition:** TCP maintains `cwnd` (congestion window) - max bytes in flight.

**Actual window = min(receiver window, congestion window)**

### TCP Congestion Control Phases

**Phase 1: Slow Start**

- cwnd starts = 1 MSS (Maximum Segment Size)
- After each ACK, cwnd += 1 MSS
- **Growth:** Exponential (doubles each RTT)
- **Until:** cwnd reaches ssthresh OR timeout occurs

**Phase 2: Congestion Avoidance**

- cwnd increases linearly (by 1 MSS per RTT)
- Continues until packet loss detected
- **Timeout:** cwnd resets to 1 MSS

**Phase 3: Fast Recovery** (TCP Reno/modern TCP)

- On duplicate ACKs (not timeout), cwnd = ssthresh/2
- Increases linearly
- Faster recovery than full reset

### Solved PYQ Example (2022-23)

_Q: Explain the working principle of the Congestion Control mechanism with a well-labeled diagram._

**Answer Structure:**

**Introduction:** TCP congestion control prevents overwhelming network by reducing sending rate when congestion detected.

**Mechanism:**

1. **Slow Start:** cwnd = 1 MSS, doubles each RTT
2. **Threshold:** At ssthresh (default = 65KB), switch to linear growth
3. **Congestion Avoidance:** cwnd += 1 MSS per RTT (linear)
4. **Timeout/Loss:** Reset cwnd = 1 MSS, ssthresh = old cwnd/2
5. **Repeat:** Ramp up again

**Diagram:** Show cwnd growth over time (exponential then linear, then reset)

---

## 4. Token Bucket vs Leaky Bucket (Tier B - 2/4 Years)

**Frequency:** 2023-24, 2024-25

### Leaky Bucket Algorithm

**Concept:** Fixed-rate output like bucket with leak. Packets queued, drain at constant rate.

**How it works:**

1. Bucket capacity = B
2. Leak rate = L (bits/sec)
3. Arriving packet: If space in bucket, queue it. Else drop.
4. Depart: 1 packet per (packet_size / L) seconds

**Advantages:**

- Smooths bursts
- Guarantees max rate = L
- Prevents network flooding

**Disadvantages:**

- Drops packets when full
- Fixed rate (not adaptive)
- Cannot handle brief burst above L

### Token Bucket Algorithm

**Concept:** Tokens added to bucket at constant rate. Each bit of data consumes 1 token. Burst allowed if tokens available.

**How it works:**

1. Tokens generated at rate R (tokens/sec)
2. Max tokens in bucket = B
3. Arriving packet: If tokens ≥ packet_size, send (remove tokens). Else wait/drop.
4. Allows temporary burst up to B tokens

**Advantages:**

- Allows controlled burst
- Can send up to B tokens worth immediately
- More flexible than leaky bucket
- Average rate = R, peak burst = B tokens

**Disadvantages:**

- Complex implementation
- Requires token generation mechanism

### Comparison

| Aspect             | Leaky Bucket         | Token Bucket                |
| ------------------ | -------------------- | --------------------------- |
| **Rate**           | Fixed (L bits/sec)   | Average (R), peak burst (B) |
| **Burst**          | No burst allowed     | Burst up to B tokens        |
| **Adaptation**     | No                   | Yes (to burst)              |
| **Flexibility**    | Low                  | High                        |
| **Implementation** | Simple               | Complex                     |
| **Use**            | Strict rate limiting | Traffic shaping             |

**Solved PYQ Example (2024-25)**

_Q: Define Leaky Bucket Algorithm. How does Token Bucket Algorithm provide better traffic shaping control?_

**Answer:**

**Leaky Bucket:**

- Packet queue empties at fixed rate
- Overflow dropped
- Ensures steady output but wastes burst capacity

**Token Bucket:**

- Allows temporal burst (accumulated tokens)
- Smoother burst handling
- Better for variable bitrate applications (video, VoIP)
- Can momentarily exceed average rate using accumulated tokens

**Example:**

- Average rate = 1 Mbps, Bucket size = 1 MB
- Token Bucket: Can send 1 MB burst immediately, then rate-limited to 1 Mbps
- Leaky Bucket: Strictly 1 Mbps, no burst

**Conclusion:** Token bucket provides better control for modern traffic patterns where bursts are expected.

---

## 5. Quality of Service (QoS) (Tier B - 2/4 Years)

**Frequency:** 2022-23, 2023-24

### Definition

QoS ensures network meets specific performance requirements for different applications (delay, bandwidth, loss rate, jitter).

### QoS Parameters

| Parameter           | Definition                    | Target           |
| ------------------- | ----------------------------- | ---------------- |
| **Bandwidth**       | Min guaranteed rate           | 2 Mbps for video |
| **Delay (Latency)** | Time packet traverses network | <150 ms for VoIP |
| **Jitter**          | Variation in delay            | <50 ms for VoIP  |
| **Packet Loss**     | % of packets dropped          | <0.1% for video  |

### Solved PYQ Example (2023-24)

_Q: Write about Quality-of-Service Parameters._

**Answer:**

1. **Bandwidth:** Guaranteed minimum throughput
   - Video streaming: 2-4 Mbps
   - VoIP: 128-256 kbps

2. **Latency:** Max one-way delay
   - Interactive apps: <150 ms
   - Batch: No requirement

3. **Jitter:** Delay variation (delay_max - delay_min)
   - VoIP: <50 ms (buffer can absorb)
   - Video: <100 ms

4. **Packet Loss:** % dropped packets
   - Data: 0% acceptable
   - Video: <0.1% acceptable
   - VoIP: <0.001% noticeable

### QoS Implementation

1. **Traffic Classification:** Identify flows (DiffServ, DSCP bits)
2. **Policing:** Enforce rate limits
3. **Scheduling:** Prioritize queues
4. **Buffer Management:** Drop less-important packets first (RED)

---

## 6. Silly Window Syndrome (Tier B - 1/4 Years)

**Frequency:** 2024-25

### Problem

When receiver window very small, sender transmits tiny segments with large overhead. Throughput plummets.

**Example:**

- Receiver window = 1 byte
- Sender sends 1 byte data + 40-byte header = 41 bytes total
- Overhead = 40/41 = 98%!

### Solutions

**Nagle's Algorithm (Sender side):**

1. Send first segment immediately
2. Buffer remaining data
3. Only send buffered data when ACK received or buffer = full MSS
4. Prevents streaming of tiny segments

**Clark's Algorithm (Receiver side):**

1. Never advertise window < MSS (unless buffer empty)
2. Even if receiver can accept data, don't advertise small window
3. Waits until buffer drains enough for MSS-sized window

**Solved PYQ Example (2024-25)**

_Q: What is Silly Window Syndrome? Explain how sender and receiver can avoid it using Nagle's and Clark's algorithms._

**Answer:**

**Problem:** Small window advertised → sender transmits tiny segments → huge overhead → low throughput

**Nagle's Algorithm (Sender):**

- Send first segment immediately
- Then accumulate data until ACK arrives or buffer full
- Result: Prevents fragmentation into small segments

**Clark's Algorithm (Receiver):**

- Advertise window = 0 until buffer drains
- Only advertise window ≥ MSS (1460 bytes typical)
- Prevents sender from sending tiny segments

**Combined Effect:** Sender waits for large window; receiver doesn't advertise small window → eliminates syndrome

---

## 7. Process-to-Process Delivery (Tier B - Implicit)

**Concept:** Transport layer ensures data delivered to correct application on destination machine.

**Mechanism:** Port numbers

- Server listens on port (well-known ports 1-1023)
- Client connects to destination IP:port
- Router uses port to identify application process

**Well-Known Ports:**

- 20,21: FTP
- 22: SSH
- 23: Telnet
- 25: SMTP
- 53: DNS
- 80: HTTP
- 110: POP3
- 143: IMAP
- 443: HTTPS
- 3306: MySQL
- 5432: PostgreSQL

---

## Exam Answer Tips (Unit 4)

### For Section A (2 marks):

- TCP vs UDP: 3-4 key differences
- Port numbers: 3 examples
- QoS parameters: Define 2-3
- **Time:** 2-3 min

### For Section B/C (10 marks):

- **TCP vs UDP:** Full header comparison table
- **3-way handshake:** Show all 3 steps with seq/ack numbers
- **Congestion control:** Explain phases with diagram showing cwnd growth
- **Token bucket:** Contrast with leaky bucket with example
- **Time:** 10-12 min

### Common Section C Patterns:

1. **Connection management:** Draw 3-way handshake + explain why 3 steps
2. **Congestion control:** Explain slow start, threshold, congestion avoidance
3. **Traffic shaping:** Compare leaky vs token bucket with numerical example
4. **Silly window syndrome:** Problem, two solutions, why combined work

### High-Scoring Tips:

- Always show TCP/UDP header fields side-by-side
- Draw 3-way handshake with timeline (not just boxes)
- Include packet numbers in handshake explanation
- Show cwnd growth graph for congestion control
- Use formulas where applicable

---

**Study Checklist:**

- [ ] TCP vs UDP: 8+ differences memorized
- [ ] Draw TCP header with all fields labeled
- [ ] Draw UDP header
- [ ] 3-way handshake explained without notes
- [ ] Connection termination process (4 steps)
- [ ] Slow start vs congestion avoidance (differences)
- [ ] Leaky bucket vs token bucket comparison (diagram)
- [ ] Nagle's and Clark's algorithms for Silly Window
- [ ] QoS parameters with real values (VoIP, video)
- [ ] Calculate window size scenarios
