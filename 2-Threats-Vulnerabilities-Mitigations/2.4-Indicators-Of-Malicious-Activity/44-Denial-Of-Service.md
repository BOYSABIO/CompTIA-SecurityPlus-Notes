# Denial Of Service
A **DoS attack** attempts to make a service **unavailable** by overwhelming, crashing, or disrupting it.  
It targets **[[02-The-CIA-Triad#Availability|availability]]** (the “A” in CIA).

DoS doesn’t necessarily steal data — it **prevents access** to resources.

---
### The Two Big Categories: DoS vs DDoS

#### **DoS (Single Source)**
- One system attacks a target
- Lower volume
- Easier to detect & block

Examples:
- Sending crafted packets to crash a service
- Overloading with repeated requests
- Resource exhaustion (single source)

#### **DDoS (Distributed DoS)**
- **Multiple systems** attack a target (often thousands)
- Usually a **botnet**
- Extremely difficult to stop
- Uses massive bandwidth

**Exam trigger:**
> “Traffic coming from thousands of IPs from around the world.”  
> → DDoS  
> “Single host crashing a server”  
> → DoS

---
### DoS/DDoS Attack Types (Security+ Must-Know)

#### **Volumetric Attacks (Bandwidth Flooding)**
Goal: overwhelm network capacity.

Examples:
- **UDP flood**
- **ICMP flood (ping flood)**
- **Amplification attacks** (DNS, NTP, SSDP)

Amplification attacks use small requests → huge responses.

**DNS amplification:**  
attacker sends small spoofed DNS request → server replies with very large response to the victim.

Exam clue:
> “10Gbps of inbound traffic from DNS servers.”

#### **Protocol / State Exhaustion Attacks**
Target network or protocol resources.
##### **SYN Flood**
Most important one.

Process:
1. Attacker sends SYN
2. Server replies with SYN/ACK
3. Attacker never sends ACK
4. Server’s TCP connection table fills
5. Legitimate connections drop

**Mitigation: SYN cookies**

Exam trigger:
> “Half-open connections filling server queue.”

#### **Application Layer Attacks**
Target specific apps like:
- web servers
- API endpoints
- login forms
- database queries

Examples:
- **HTTP GET/POST flood**
- **Slowloris** (keeps connections open indefinitely)
- **Expensive database queries repeatedly sent**

Slowloris is a classic DoS tool:
- Sends partial HTTP headers slowly
- Server keeps connections open
- Server runs out of resources

Exam trigger:
> “Web server running out of available connections.”

#### **Resource Exhaustion DoS**
Uses legitimate but excessive requests.

Examples:
- Repeated login attempts
- Creating thousands of large files
- Filling disk or memory intentionally

This often looks like a misconfiguration unless volume is suspicious.

#### **Logic-Based DoS**
Exploits a bug or flaw to crash a program instantly.

Examples:
- Sending malformed packets
- Triggering a race condition
- Causing a buffer overflow
- Packet-of-death attacks (Ping of Death, Teardrop)

These don’t require high volume — just precise input.

Exam trigger:
> “Single malformed packet crashes system.”

### DDoS Botnets
Attackers often use:
- IoT botnets (Mirai)
- Malware-infected PCs
- Compromised servers

Botnets can:
- generate massive traffic
- rotate IPs
- use C2 servers
- hide behind proxies

Mitigation:
- ISP filtering
- Cloud DDoS protection (Akamai, Cloudflare)
- Blackholing traffic
- Geoblocking
- Rate limiting
- CDNs

---
### DoS vs DDoS vs Resource Exhaustion (Exam Differences)

| Attack Type             | Description                                            |
| ----------------------- | ------------------------------------------------------ |
| **DoS**                 | One system attacks the victim                          |
| **DDoS**                | Many systems (botnet) attack the victim                |
| **Resource Exhaustion** | High usage of legitimate functions drains CPU/disk/ram |
| **Application DoS**     | Overwhelms app logic, not network                      |
| **Protocol DoS**        | SYN flood, fragmentation attacks                       |
| **Amplification**       | Spoofed packets cause large replies to victim          |

CompTIA LOVES to ask you to classify these.

---
### Common DoS Tools You Should Know
Not necessary to memorize for the exam, but helpful context:
- **LOIC / HOIC** (old but commonly referenced)
- **Slowloris**
- **Hping**
- **Mirai botnet variants**

If you see "Slowloris" on the exam → **application-layer DoS**.

---
### DoS Mitigation Methods (Exam-Focused)

#### **Network-Level**
- ACLs
- Firewalls
- Rate limiting
- Geolocation filtering
- Anti-spoofing filters
- Blackhole routing

#### **Application-Level**
- WAF (Web Application Firewall)
- Load balancers
- Reverse proxies
- Caching

#### **Host-Level**
- Patching
- SYN cookies
- Increasing connection queue sizes

#### **Cloud-Level**
- DDoS mitigation services
- Auto-scaling groups

#### **Design-Level**
- Redundancy
- Fault tolerance
- Content Delivery Networks

---
### How This Connects to Everything Else

| Topic                                                            | Relationship                                      |
| ---------------------------------------------------------------- | ------------------------------------------------- |
| **Botnets**                                                      | Used for DDoS attacks                             |
| **[[36-Misconfiguration-Vulnerabilities\|Misconfigurations]]**   | Can look like DoS or be exploited for DoS         |
| **[[38-Zero-day-Vulnerabilities\|Zero-days]]**                   | Logic DoS attacks often use unknown bugs          |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud vulnerabilities]]** | Cloud DDoS = cost-based DoS (billing explosion)   |
| **[[39-An-Overview-Of-Malware\|Malware]]**                       | Worms or Trojans often preload botnet agents      |
| **[[43-Physical Attacks\|Physical attacks]]**                    | Sometimes power disruption = DoS                  |
| **Network attacks**                                              | DoS often paired with MITM or smokescreen tactics |