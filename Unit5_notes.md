# UNIT 5: Application Layer

**Coverage:** DNS, HTTP/HTTPS, FTP, SMTP, SNMP, Telnet, Cryptography, Data compression

---

## ⭐ TIER A TOPICS (High Priority - Appeared 3-4 Years)

---

## 1. FTP (File Transfer Protocol) (Tier A - 4/4 Years)

**Frequency:** All 4 years (2021-22, 2022-23, 2023-24, 2024-25)  
**Expected Questions:** FTP protocol, commands, active vs passive mode, FTP vs HTTP

### Definition

FTP is an application layer protocol for reliable transfer of files between client and server over TCP.

### FTP Architecture

**Two TCP connections:**

1. **Control Connection (Port 21):** Command/response (persistent for session)
2. **Data Connection (Port 20 for active):** Actual file transfer (creates/closes per file)

### FTP Modes

**Active Mode (PORT):**

- Client initiates control connection (port 21)
- Client tells server: "Listen on my IP:port X"
- Server connects back to client on port X for data transfer
- **Problem:** Firewalls block incoming connections
- **Advantage:** Server initiates, so server knows where data goes

**Passive Mode (PASV):**

- Client initiates control connection (port 21)
- Client asks server: "What port can I connect to?"
- Server responds: "Listen on my IP:port Y"
- Client connects to server on port Y for data transfer
- **Advantage:** Both connections initiated by client (firewalls allow)
- **Disadvantage:** Server must listen on multiple ports

### Key FTP Commands

| Command         | Purpose                  | Response                   |
| --------------- | ------------------------ | -------------------------- |
| `USER`          | Send username            | 331 (password needed)      |
| `PASS`          | Send password            | 230 (login OK)             |
| `RETR filename` | Retrieve (download) file | 125 (starting), 226 (done) |
| `STOR filename` | Store (upload) file      | 125 (starting), 226 (done) |
| `LIST`          | List files in directory  | 150 (list follows)         |
| `CWD /dir`      | Change working directory | 250 (OK)                   |
| `MKD dirname`   | Make directory           | 257 (created)              |
| `DELE filename` | Delete file              | 250 (deleted)              |
| `PWD`           | Print working directory  | 257 (path returned)        |
| `QUIT`          | Logout, close connection | 221 (goodbye)              |
| `TYPE A/I`      | Set mode ASCII/Binary    | 200 (OK)                   |

### Solved PYQ Examples

**Example 1 (2023-24)**

_Q: Differentiate between FTP and HTTP._

**Answer Table:**

| Aspect          | FTP                            | HTTP                        |
| --------------- | ------------------------------ | --------------------------- |
| **Purpose**     | File transfer                  | Web document transfer       |
| **Port**        | 21 (control), 20 (data)        | 80 (HTTP), 443 (HTTPS)      |
| **Protocol**    | Dedicated file transfer        | General-purpose web         |
| **Connections** | 2 connections (control + data) | 1 connection (persistent)   |
| **Reliability** | Always reliable (TCP)          | Reliable (TCP)              |
| **User Auth**   | Username/password              | HTTP Basic or cookies       |
| **Efficiency**  | Efficient (dedicated)          | Efficient for web documents |
| **Use Case**    | Large file transfers, archives | Web pages, APIs, content    |
| **Stateful**    | Yes (session maintained)       | Stateless (connectionless)  |
| **Modes**       | Active/passive                 | Request/response            |

**Example 2 (2024-25)**

_Q: Explain the following: (i) FTP (ii) HTTP (iii) Telnet_

**FTP Answer (Concise):**

- File Transfer Protocol for reliable file transfer
- Uses 2 connections: control (port 21) and data (port 20)
- Modes: Active (server initiates data), Passive (client initiates)
- Commands: USER, PASS, RETR (download), STOR (upload), LIST, DELE
- More efficient than HTTP for bulk file transfers

---

## 2. DNS (Domain Name System) (Tier A - 4/4 Years)

**Frequency:** All 4 years  
**Expected Questions:** DNS resolution process, DNS hierarchy, DNS query types

### Definition

DNS translates human-readable domain names (www.google.com) into IP addresses (142.251.32.14) using distributed database.

### DNS Hierarchy

```
                        Root Server (.)
                              |
                ________________|________________
               |        |        |        |        |
              .com     .org     .edu    .net     .in
               |
         __________|__________
        |                     |
    google.com             facebook.com
        |
    ____|____
   |        |
  www       mail
```

**DNS Server Types:**

1. **Root Server:** Knows location of all TLDs (.com, .org, etc.) - 13 worldwide
2. **TLD Server:** Knows all domain registrars for a TLD
3. **Authoritative Server:** Has actual A records (domain → IP)
4. **Recursive Resolver:** Performs full resolution (usually at ISP)

### DNS Resolution Process (Recursive Query)

**Step 1: Client to Recursive Resolver (ISP)**

- Client asks: "What's IP of www.google.com?"
- Resolver caches commonly used addresses

**Step 2: Resolver to Root Server**

- Resolver asks: "Where's www.google.com?"
- Root Server responds: "Ask TLD server for .com"

**Step 3: Resolver to TLD Server**

- Resolver asks TLD server: "Where's google.com?"
- TLD Server responds: "Ask authoritative server at X.X.X.X"

**Step 4: Resolver to Authoritative Server**

- Resolver asks: "What's IP of www.google.com?"
- Authoritative Server responds: "142.251.32.14"

**Step 5: Resolver to Client**

- Resolver sends IP to client
- Client caches for future use (TTL = Time to Live)

**Total Time:** ~200-500 ms for first query, cached <1 ms

### DNS Record Types

| Type      | Purpose                | Example                               |
| --------- | ---------------------- | ------------------------------------- |
| **A**     | IPv4 address           | google.com → 142.251.32.14            |
| **AAAA**  | IPv6 address           | google.com → 2607:f8b0:4004:815::200e |
| **CNAME** | Canonical name (alias) | www.google.com → google.com           |
| **MX**    | Mail exchange          | mail.google.com for google.com        |
| **TXT**   | Text records           | SPF, DKIM for email authentication    |
| **NS**    | Nameserver             | Points to authoritative server        |
| **SOA**   | Start of Authority     | Serial, refresh, retry info           |

### Solved PYQ Examples

**Example 1 (2022-23)**

_Q: Explain DNS._

**Answer Structure:**

**Definition:** DNS translates domain names to IP addresses using distributed hierarchical database.

**Process:**

1. User types URL in browser
2. OS queries recursive resolver (ISP's DNS server)
3. Resolver queries root server
4. Root server refers to TLD server
5. TLD server refers to authoritative server
6. Authoritative server returns A record (IP address)
7. Resolver returns IP to client
8. Client connects to web server at that IP

**Caching:** Commonly accessed domains cached at each level and client (TTL limits)

**Advantages:**

- Decentralized, scalable
- Fault-tolerant (multiple servers)
- Efficient (caching reduces queries)

**Disadvantages:**

- Initial query slow (200-500 ms)
- DNS can be poisoned (security issue)
- All DNS queries visible (privacy)

---

## 3. SNMP (Simple Network Management Protocol) (Tier A - 3/4 Years)

**Frequency:** 2022-23, 2023-24, 2024-25

### Definition

SNMP allows network administrators to monitor and manage devices (routers, switches, servers, printers) from central location.

### SNMP Architecture

**Components:**

1. **SNMP Manager:** Central monitoring station (admin's computer)
2. **SNMP Agent:** Software on managed device (router, switch)
3. **MIB (Management Information Base):** Database of device variables
4. **Managed Objects:** Specific variables in MIB

### SNMP Operations

| Operation    | Direction       | Purpose                           |
| ------------ | --------------- | --------------------------------- |
| **GET**      | Manager → Agent | Request variable value            |
| **SET**      | Manager → Agent | Change variable value             |
| **GET-NEXT** | Manager → Agent | Request next variable             |
| **GET-BULK** | Manager → Agent | Request multiple variables        |
| **TRAP**     | Agent → Manager | Alert about problem (unsolicited) |

### MIB Variables Example

```
sysUpTime: Device uptime in ticks
sysDescr: Device description
ifInOctets: Bytes received on interface
ifOutOctets: Bytes sent on interface
ifInErrors: Errors on incoming interface
ifOutErrors: Errors on outgoing interface
```

### Solved PYQ Examples

**Example 1 (2023-24)**

_Q: Explain SNMP in detail._

**Answer Structure:**

**Definition:** Protocol for monitoring and managing network devices centrally.

**Architecture:**

- Manager (admin console) sends requests to agents on devices
- Agent collects MIB data and responds
- TRAP messages alert manager of problems

**Benefits:**

1. Centralized monitoring (single console for entire network)
2. Remote management (no physical visit needed)
3. Proactive alerts (TRAP messages)
4. Performance metrics (bandwidth, CPU, memory, disk)
5. Inventory management (track all devices)

**Security (SNMP v3):**

- Authentication (username)
- Privacy (encrypted messages)
- Access control (read-only vs read-write)

**Disadvantages:**

- Limited to device statistics (can't fix issues remotely)
- SNMP v1/v2 not secure (SNMP v3 fixes this)
- Overhead if too many devices

**Example 2 (2024-25)**

_Q: Describe the following: (i) SNMP (ii) DNS (iii) Data Compression_

**SNMP Answer (Concise):**

- Network management protocol (port 161/162 UDP)
- Manager sends GET/SET to agents on devices
- Agents respond with MIB values
- TRAP for unsolicited alerts
- Centralized monitoring of routers, switches, servers

---

## 4. RSA Cryptography (Tier A - 3/4 Years)

**Frequency:** 2022-23, 2023-24, 2024-25

### Definition

RSA (Rivest-Shamir-Adleman) is asymmetric cryptography using public key (encrypt) and private key (decrypt).

### RSA Algorithm Steps

**Key Generation:**

1. **Choose primes:** Select two large primes p and q
2. **Compute n:** n = p × q
3. **Compute φ(n):** φ(n) = (p-1) × (q-1)
4. **Choose e:** 1 < e < φ(n), gcd(e, φ(n)) = 1
   - Typically e = 65537 or e = 3
5. **Compute d:** d × e ≡ 1 (mod φ(n))
   - Find d such that (d × e) mod φ(n) = 1
6. **Public Key:** (e, n)
7. **Private Key:** (d, n)

**Encryption:**

- Plaintext M to Ciphertext C: C = M^e mod n

**Decryption:**

- Ciphertext C to Plaintext M: M = C^d mod n

### Solved PYQ Example (2022-23)

_Q: Explain Asymmetric cryptography. Also, write the steps used in RSA algorithm, demonstrate the transmission of character "F" using RSA._

**Answer:**

**Asymmetric Cryptography:**

- Uses two keys: Public (anyone can use) and Private (secret)
- Sender encrypts with recipient's public key
- Only recipient with private key can decrypt
- Also used for digital signatures (sign with private, verify with public)

**RSA Steps:**

1. **Select p=3, q=11** (small for demonstration; real use: 1024+ bit primes)
2. **n = 3 × 11 = 33**
3. **φ(n) = (3-1) × (11-1) = 2 × 10 = 20**
4. **Choose e:** e must satisfy gcd(e,20)=1. Let e=3
5. **Find d:** 3d ≡ 1 (mod 20)
   - Try d: 3×1=3, 3×7=21≡1 (mod 20) ✓
   - d = 7
6. **Public Key:** (3, 33) ; **Private Key:** (7, 33)

**Encrypt "F":**

- ASCII "F" = 70 (but 70 > 33, so use 70 mod 33 = 4, or use F=6 directly)
- Using M=6: C = 6^3 mod 33 = 216 mod 33 = 18
- **Ciphertext: 18**

**Decrypt:**

- M = 18^7 mod 33
- 18^7 = 612,220,032 mod 33 = 6
- **Plaintext: 6 (F)** ✓

**Security:** Finding d requires factoring n (33 = 3×11), which is easy for small numbers but computationally infeasible for 2048-bit numbers.

---

## 📘 TIER B TOPICS (Medium Priority)

---

## 5. HTTP/HTTPS (Tier B - 1-2 Years)

**Frequency:** 2021-22 (HTTP), 2022-23 (HTTP vs HTTPS), 2024-25 (HTTP)

### HTTP (Hypertext Transfer Protocol)

**Definition:** Stateless protocol for transferring web documents (HTML, CSS, images) between client and server.

**Port:** 80 (default)

**Request Methods:**

| Method     | Purpose              | Body | Idempotent   |
| ---------- | -------------------- | ---- | ------------ |
| **GET**    | Retrieve resource    | No   | Yes (safe)   |
| **POST**   | Submit data          | Yes  | No (creates) |
| **PUT**    | Update resource      | Yes  | Yes          |
| **DELETE** | Remove resource      | No   | Yes          |
| **HEAD**   | Like GET but no body | No   | Yes          |

**Response Status Codes:**

| Code | Meaning       | Example                                     |
| ---- | ------------- | ------------------------------------------- |
| 1xx  | Informational | 100 Continue                                |
| 2xx  | Success       | 200 OK, 201 Created                         |
| 3xx  | Redirection   | 301 Moved, 304 Not Modified                 |
| 4xx  | Client Error  | 400 Bad Request, 404 Not Found              |
| 5xx  | Server Error  | 500 Internal Error, 503 Service Unavailable |

### HTTPS (HTTP Secure)

**Definition:** HTTP with encryption (SSL/TLS)

**Port:** 443 (default)

**Differences:**

| Feature            | HTTP                      | HTTPS                        |
| ------------------ | ------------------------- | ---------------------------- |
| **Encryption**     | No                        | Yes (SSL/TLS)                |
| **Authentication** | No                        | Yes (certificate)            |
| **Integrity**      | Vulnerable                | Protected (MAC)              |
| **Privacy**        | No (traffic visible)      | Yes (encrypted)              |
| **Performance**    | Faster (no overhead)      | Slightly slower (encryption) |
| **Security**       | Unsafe for sensitive data | Safe for banking, login      |

**Solved PYQ Example (2022-23)**

_Q: State difference between HTTP and HTTPS._

**Answer:**

| Aspect            | HTTP           | HTTPS                      |
| ----------------- | -------------- | -------------------------- |
| **Port**          | 80             | 443                        |
| **Data Format**   | Plain text     | Encrypted (AES, TLS)       |
| **Certificate**   | None           | Required (SSL certificate) |
| **Man-in-Middle** | Vulnerable     | Protected                  |
| **Speed**         | Faster         | Slightly slower            |
| **Use**           | Public content | Sensitive data             |
| **URL**           | http://        | https://                   |
| **Lock Icon**     | No             | Yes (browser shows)        |

---

## 6. SMTP / IMAP / POP3 (Tier B - 2/4 Years)

**Frequency:** 2021-22 (SMTP), 2024-25 (SMTP, IMAP vs POP3)

### SMTP (Simple Mail Transfer Protocol)

**Purpose:** Send emails from client to server or server-to-server

**Port:** 25 (relay), 587 (submission, with authentication)

**Process:**

1. Connect to SMTP server (e.g., mail.gmail.com)
2. Authenticate with username/password
3. Specify FROM address
4. Specify TO address(es)
5. Provide message body (headers + content)
6. Server queues for delivery

**SMTP Commands:**

| Command                       | Purpose               |
| ----------------------------- | --------------------- |
| `HELO domain`                 | Introduce client      |
| `AUTH LOGIN`                  | Authenticate          |
| `MAIL FROM:sender@domain.com` | Set sender            |
| `RCPT TO:receiver@domain.com` | Add recipient         |
| `DATA`                        | Begin message content |
| `QUIT`                        | Close connection      |

### POP3 (Post Office Protocol v3)

**Purpose:** Retrieve emails from server to client

**Port:** 110 (standard), 995 (SSL)

**Process:**

1. Connect to server
2. Authenticate (username/password)
3. LIST (see messages)
4. RETR (retrieve specific message)
5. DELETE (mark for deletion)
6. QUIT (commit deletions)

**Characteristic:** Downloads email to client; server deletes original (offline access)

### IMAP4 (Internet Message Access Protocol v4)

**Purpose:** Access emails on server (like Outlook, Gmail web interface)

**Port:** 143 (standard), 993 (SSL)

**Process:**

1. Connect to server
2. Authenticate
3. SELECT folder
4. FETCH (retrieve without downloading)
5. STORE flags (mark read/unread)
6. Can access from multiple devices

**Characteristics:** Emails stay on server; can organize in folders; synced across devices

### IMAP vs POP3 Comparison

| Feature       | POP3                | IMAP                    |
| ------------- | ------------------- | ----------------------- |
| **Storage**   | Downloads to client | Stays on server         |
| **Folders**   | No server folders   | Multiple folders        |
| **Sync**      | Single device       | Multiple devices        |
| **Offline**   | Yes                 | No (needs connection)   |
| **Bandwidth** | Lower               | Higher (on-demand)      |
| **Use**       | Legacy              | Modern (Gmail, Outlook) |

**Solved PYQ Example (2024-25)**

_Q: Explain how SMTP can handle transfer of videos and images? Also, explain the advantages of IMAP4 over POP3 mail access protocols._

**SMTP with Media:**

- Media files attached to email as MIME (Multipurpose Internet Mail Extensions) attachments
- MIME encodes binary data as base64 text (increases size by 33%)
- Server queues and forwards entire message with attachment
- Limitation: Large files may exceed server limits (25 MB typical)

**IMAP4 Advantages:**

1. Multiple device sync (access from phone, laptop, desktop)
2. Folder organization (keeps emails categorized on server)
3. Partial retrieval (don't download full email immediately)
4. Flags (mark as read/unread, sync across devices)
5. Better for users with multiple mail accounts/folders

---

## 7. Telnet (Tier B - 2/4 Years)

**Frequency:** 2023-24, 2024-25

### Definition

Telnet is application protocol for remote login to computer terminals.

**Port:** 23 (standard)

**Process:**

1. Connect to remote server (port 23)
2. Authenticate with username/password
3. Execute commands as if sitting at terminal
4. Remote server executes commands and returns output

**Use Cases:**

- System administration (login to servers)
- Network device management (routers, switches)
- Testing services on specific ports

**Disadvantages:**

- **Not Secure:** Credentials sent in plain text
- **Vulnerable:** Man-in-middle can capture password
- **Replaced by:** SSH (Secure Shell, port 22)

**Comparison with SSH:**

| Feature            | Telnet   | SSH              |
| ------------------ | -------- | ---------------- |
| **Port**           | 23       | 22               |
| **Encryption**     | No       | Yes              |
| **Security**       | Weak     | Strong           |
| **Authentication** | Password | Keys or Password |
| **Use**            | Legacy   | Modern standard  |

---

## 8. Data Compression (Tier B - 2/4 Years)

**Frequency:** 2023-24, 2024-25

### Definition

Data compression reduces data size by removing redundancy.

### Lossless vs Lossy

**Lossless:**

- Original perfectly recovered
- Used for: Text, code, archives
- Compression ratio: 30-50%
- Examples: ZIP, GZIP, PNG

**Lossy:**

- Some data discarded (imperceptible)
- Used for: Images, video, audio
- Compression ratio: 90-99%
- Examples: JPEG, MP3, MPEG

### Compression Algorithms

1. **Huffman Coding:** Frequent characters → short codes
2. **LZ77/LZ78:** Replace repeated patterns with references
3. **RLE (Run Length Encoding):** Store count of repetitions
4. **Arithmetic Coding:** Represent message as fraction (high ratio)

**Solved PYQ Example (2024-25)**

_Q: Explain the following: ... (iii) Data Compression_

**Answer:**

- Reduces data size by removing redundancy
- **Lossless:** Perfect recovery (text, archives, ZIP/GZIP)
- **Lossy:** Discards imperceptible data (images/video, JPEG/MP3)
- **Huffman:** Assigns variable-length codes (frequent → short)
- **LZ:** Replace repeated patterns with back-references
- Used to save bandwidth and storage

---

## Exam Answer Tips (Unit 5)

### For Section A (2 marks):

- Protocol name + port + 1 key feature
- FTP vs HTTP: 2-3 differences
- DNS resolution: 1-line description
- SNMP: Manager/agent concept
- **Time:** 2-3 min

### For Section B/C (10 marks):

- **FTP:** Active vs passive mode, commands, advantages over HTTP
- **DNS:** Full resolution process with all 4 servers
- **SNMP:** Architecture, operations, management objects
- **RSA:** Full key generation, encryption/decryption with numbers
- **HTTP/HTTPS:** Comparison table, security benefits
- **SMTP/IMAP:** Process flow, advantages/disadvantages
- **Time:** 10-12 min

### Common Section C Patterns:

1. **Protocol explanation:** FTP, DNS, SMTP with process diagrams
2. **Cryptography:** RSA key generation and encryption example
3. **Comparison:** FTP vs HTTP, HTTP vs HTTPS, IMAP vs POP3, SMTP handling media
4. **Management:** SNMP operations, DNS hierarchy, mail access methods

### High-Scoring Tips:

- Show DNS hierarchy diagram (5 levels)
- Draw FTP active vs passive connection diagrams
- Show RSA calculation step-by-step
- Use process flowcharts (arrows showing data flow)
- Compare protocols in table format
- Include port numbers and security aspects

---

**Study Checklist:**

- [ ] FTP: 10 commands and their purposes
- [ ] Active vs passive mode differences
- [ ] DNS: 4-step resolution process explained
- [ ] DNS record types (A, CNAME, MX, NS, SOA)
- [ ] SNMP: GET, SET, TRAP operations
- [ ] MIB objects examples
- [ ] RSA: Generate keys with p=5, q=11
- [ ] RSA: Encrypt and decrypt message M=7
- [ ] HTTP vs HTTPS comparison (8+ differences)
- [ ] SMTP, POP3, IMAP workflow
- [ ] IMAP4 advantages over POP3
- [ ] Compression types and algorithms
- [ ] Telnet vs SSH comparison
- [ ] Data compression: lossless vs lossy examples
