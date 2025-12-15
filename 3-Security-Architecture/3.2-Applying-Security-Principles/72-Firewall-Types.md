# Firewall Types
Firewalls are one of the **highest-yield exam topics** in Security+.  
Questions often test **what type of firewall to use**, **what it can/can’t see**, and **where it sits in the network**.

This section is about **classification by capability**, not placement.

---
### **What a Firewall Fundamentally Does**
A firewall is a **traffic control device** that:
- Allows or denies traffic
- Based on rules
- At defined trust boundaries

Firewalls operate at **different OSI layers**, and that determines what they can inspect.

---

### **Packet-Filtering Firewall (Stateless Firewall)**
#### **What it is**
- Examines **individual packets**
- No awareness of session state
- Decisions based on:
    - Source IP
    - Destination IP
    - Port
    - Protocol

Operates mainly at:
- **Layer 3 (Network)** (The Network Layer, also known as Layer 3, is responsible for routing data between different networks. It's the layer where IP addresses are used to identify devices on a network and where packets are routed to their destination.)
- **Layer 4 (Transport)** (The Transport Layer, or Layer 4, is responsible for providing reliable data transfer between devices on a network. It ensures that packets are delivered correctly and in the correct order, and it also handles errors and exceptions.)

#### **Strengths**
- Fast
- Low overhead
- Simple rules

#### **Limitations**
- Cannot track sessions
- Cannot detect application attacks
- Easy to bypass with spoofed packets

#### **Exam triggers**
> “Filters traffic using IP addresses and ports only”  
> → **Packet-filtering firewall**

---

### **Stateful Inspection Firewall**
#### **What it is**
- Tracks **connection state** (session awareness)
- Maintains a **state table**

Example:
- Allows return traffic automatically if session was initiated internally

#### **Strengths**
- More secure than stateless
- Prevents many spoofing attacks

#### **Limitations**
- Limited application awareness
- Doesn’t deeply inspect payloads

#### **Exam triggers**
> “Tracks active connections”  
> “Allows return traffic automatically”  
> → **Stateful firewall**

This is the **default “firewall” assumption** unless specified otherwise.

---
### **Circuit-Level Gateway**
#### **What it is**
- Verifies TCP handshakes (sessions)
- Does **not inspect payloads**

Classic example:
- **SOCKS proxy** (Session-based proxy)

#### **Purpose**
- Ensures sessions are legitimate
- Hides internal network structure

#### **Exam note**
Rarely deployed today, but still tested conceptually.
> “Validates session establishment only”  
> → **Circuit-level gateway**

---
### **Application-Layer Firewall / Proxy Firewall**
#### **What it is**
- Operates at **Layer 7 (Application)**
- Acts as an **intermediary** between client and server
- Fully understands application protocols (HTTP, FTP, SMTP)

#### **Capabilities**
- Inspects payloads
- Can block application-specific attacks
- Can enforce protocol compliance

#### **Trade-offs**
- Slower
- More resource-intensive
- Requires protocol-specific configuration

#### **Exam triggers**
> “Fully inspects application data”  
> “Acts as an intermediary”  
> → **Application-layer firewall**

---
### **Next-Generation Firewall (NGFW)**
#### **What it is**
A modern firewall combining:
- Stateful inspection
- Application awareness
- Integrated IDS/IPS
- User identity awareness
- SSL/TLS inspection

#### **Key feature**
**Application-based filtering**, not just port-based.

Example:
- Blocking Facebook regardless of port used

#### **Exam triggers**
> “Identifies traffic by application”  
> “Integrated IPS”  
> → **NGFW**

This is **very heavily tested**.

---
### **Web Application Firewall (WAF)**
#### **What it is**
- Specialized firewall for **web applications**
- Operates at **Layer 7**

#### **Protects against**
- SQL injection
- XSS
- CSRF
- Directory traversal

#### **Placement**
- In front of web servers
- Often behind a load balancer

#### **Exam shortcut**
> “Protect web apps” → **WAF**

Not a general-purpose firewall.

---
### **Unified Threat Management (UTM)**
#### **What it is**
“All-in-one” security appliance.

Includes:
- Firewall
- IDS/IPS
- VPN
- Content filtering
- Malware protection

#### **Pros**
- Easy to manage
- Lower cost

#### **Cons**
- Less scalable
- Single point of failure

#### **Exam triggers**
> “Single appliance providing multiple security functions”  
> → **UTM**

---
### **Firewall Deployment Models (Quick Context)**
(Not a full topic yet, but relevant here.)
- **Network firewall** → protects network segments
- **Host-based firewall** → protects individual systems
- **Virtual firewall** → cloud/VM-based

Security+ may ask **which type fits a scenario best**.

---
###  **Firewall Types — Quick Comparison Table**

| Firewall Type     | Layer | Tracks Sessions | Payload Inspection | Typical Use        |
| ----------------- | ----- | --------------- | ------------------ | ------------------ |
| Packet-filtering  | L3/L4 | ❌ No            | ❌ No               | Basic filtering    |
| Stateful          | L3/L4 | ✅ Yes           | ❌ Limited          | Standard perimeter |
| Circuit-level     | L5    | ✅ Yes           | ❌ No               | Session validation |
| Application-layer | L7    | ✅ Yes           | ✅ Yes              | Deep inspection    |
| NGFW              | L3–L7 | ✅ Yes           | ✅ Yes              | Modern enterprise  |
| WAF               | L7    | ✅ Yes           | ✅ Yes              | Web app protection |
| UTM               | Multi | ✅ Yes           | ✅ Yes              | SMB environments   |

---
### **How Firewall Types Connect to Previous Topics**

| Previous Topic                                         | Connection                             |
| ------------------------------------------------------ | -------------------------------------- |
| **[[70-Network-Appliances\|Network Appliances]]**      | Firewalls are core enforcement devices |
| **[[60-Intrusion-Prevention\|Intrusion Prevention]]**  | NGFW often includes IPS                |
| **[[50-Application-Attacks\|Application Attacks]]**    | WAF mitigates SQLi, XSS                |
| **[[52-Segmentation-&-Access-Control\|Segmentation]]** | Firewalls enforce trust boundaries     |
| **[[06-Zero-Trust\|Zero Trust]]**                      | Firewalls enforce policy per flow      |
| **[[55-Cloud-Infrastructure\|Cloud Infrastructure]]**  | Security groups = firewall logic       |
| **[[54-Hardening-Techniques\|Hardening]]**             | Firewall rules reduce attack surface   |

Firewalls are **where architecture meets enforcement**.