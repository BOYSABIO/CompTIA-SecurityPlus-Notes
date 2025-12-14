# Network Appliances
This topic builds directly on **Intrusion Prevention**.  
Now we focus on the **actual devices and services** that enforce security, control traffic, inspect data, and support secure network operations.

Think of this as the **“toolbox” layer** of secure infrastructure.

---
### **Firewalls (Core Network Appliance)**
#### **1.1 Packet-Filtering Firewall**
- Filters based on IP, port, protocol
- Stateless (does not track sessions)

Used for:
- Simple, fast filtering
- Backbone routing controls

Limitation:
- No deep inspection

#### **1.2 Stateful Firewall**
- Tracks active connections (sessions)
- Allows return traffic automatically

Security+ default “firewall” unless otherwise specified.

#### **1.3 Next-Generation Firewall (NGFW)**
Adds:
- Application awareness
- Deep packet inspection
- Integrated IPS
- User identity awareness

Exam trigger:
> “Identify traffic by application, not port” → NGFW

---
### **IDS / IPS Appliances (Quick Reinforcement)**
We just covered these, but here’s how they appear as appliances:
- **NIDS/NIPS** → Dedicated hardware or virtual appliances
- Inline for IPS, passive for IDS
- Often integrated into NGFWs

Exam trap:
> “Stops malicious traffic inline” → IPS appliance

---
### **Web Application Firewall (WAF)**
Purpose:
- Protects **web applications**, not networks

Stops:
- SQL injection
- Cross-site scripting (XSS)
- CSRF
- Directory traversal

Placement:
- In front of web servers
- Often behind load balancers

Exam trigger:
> “Protect web applications” → WAF

---
### **Proxy Servers**

#### **4.1 Forward Proxy**
- Client → proxy → internet
- Hides internal clients
- Enforces content filtering

Used for:
- URL filtering
- DLP
- Malware scanning

#### **4.2 Reverse Proxy**
- Internet → proxy → internal servers
- Hides internal server structure
- Often performs TLS termination

Used for:
- Load balancing
- WAF placement
- DoS mitigation

---
### **Load Balancers**
Distribute traffic across backend servers.

Types:
- **Layer 4** (TCP/UDP-based)
- **Layer 7** (HTTP-aware)

Security benefits:
- [[02-The-CIA-Triad#Availability|Availability]]
- [[44-Denial-Of-Service#**DDoS (Distributed DoS)**|DDoS]] resistance
- SSL/TLS offloading

---
### **VPN Concentrators**
Dedicated devices that:
- Terminate VPN tunnels
- Authenticate users/devices
- Encrypt traffic

Supports:
- Site-to-site VPNs
- Remote access VPNs

Exam phrase:
> “Central device managing many VPN connections” → VPN concentrator

---
### **Network Access Control (NAC) Appliances**
Enforces:
- Device authentication
- Posture checks (patch level, AV, OS version)

Uses:
- 802.1X (port-based authentication standard)

Purpose:
- Prevent unauthorized devices from joining the network

---
### **Email Security Appliances**
Protect mail flow by:
- Filtering spam
- Blocking phishing
- Scanning attachments
- Enforcing DMARC/DKIM/SPF
	- DMARC (Domain-based Message Authentication, Reporting, and Conformance): DMARC is an email authentication framework that helps prevent phishing attacks by verifying the identity of the sender's domain.
	- DKIM (DomainKeys Identified Mail): DKIM is an email authentication protocol that helps prevent spam and phishing attacks by verifying the identity of the sender's domain.
	- SPF (Sender Policy Framework): SPF is an email authentication protocol that helps prevent spam and phishing attacks by verifying the identity of the sender's domain.
	- DMARC helps verify the identity of the sender's domain, DKIM verifies the authenticity of the email using a private key, and SPF verifies the identity of the sender's IP address.

Often deployed:
- At network edge
- As cloud-based appliances

---
### **Data Loss Prevention (DLP) Appliances**
Purpose:
- Prevent sensitive data from leaving the organization

Monitors:
- Email
- Web uploads
- File transfers

Triggers on:
- PII (Personally Identifiable Information)
- PHI (Protected Health Information)
- Financial data

Exam trigger:
> “Prevent data exfiltration” → DLP

---
### **Unified Threat Management (UTM)**
“All-in-one” security appliance.

Combines:
- Firewall
- IDS/IPS
- VPN
- Content filtering
- Malware protection

Trade-off:
- Simplified management
- Less scalable than best-of-breed solutions

Exam phrase:
> “Single appliance providing multiple security functions” → UTM

---
### **Network Monitoring & Management Appliances**

#### **11.1 SIEM (Security Information and Event Management)**
Central log collection + correlation.

Not inline — **detective control**.

#### **11.2 NMS (Network Management System)**
Monitors:
- Device health
- Performance
- Availability

Uses:
- SNMPv3 (secure management protocol)

---
### **Hardware vs Virtual Appliances**
Many appliances exist as:
- Physical devices
- Virtual machines
- Cloud-native services

Exam angle:
> “Elastic scaling, cloud-native security” → virtual/cloud appliances

---
### **How Network Appliances Connect to Previous Topics**

| Appliance        | Connects To                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| Firewall / NGFW  | [[52-Segmentation-&-Access-Control\|Segmentation]], [[59-Secure-Infrastructure\|secure infrastructure]] |
| IDS / IPS        | Intrusion prevention, [[51-Indicators-Of-Compromise\|IoCs]]                                             |
| WAF              | [[50-Application-Attacks\|Application attacks]]                                                         |
| Proxy            | [[54-Hardening-Techniques\|Hardening]], [[53-Mitigation-Techniques\|mitigation]]                        |
| Load balancer    | Availability, [[58-Infrastructure-Considerations\|infrastructure considerations]]                       |
| VPN concentrator | Secure remote access                                                                                    |
| NAC              | [[06-Zero-Trust\|Zero Trust]], [[52-Segmentation-&-Access-Control\|access control]]                     |
| DLP              | Data protection, exfiltration IoCs                                                                      |
| SIEM             | Monitoring, incident response                                                                           |

Network appliances are the **enforcement mechanisms** for all the principles we’ve been learning.