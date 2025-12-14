# Intrusion Prevention
This topic sits right after **Secure Infrastructure** for a reason:  
Once infrastructure is **designed securely**, intrusion prevention is about **actively detecting and stopping attacks in real time**.

Think of this as the **active enforcement layer** of everything we’ve built so far.

---
### **IDS vs IPS (Foundational Distinction – Very Testable)**

#### **IDS – Intrusion Detection System**
- **Detects** suspicious or malicious activity
- Generates alerts/logs
- **Does NOT block traffic**

Placement:
- Network-based IDS (NIDS) → monitors traffic via SPAN/TAP
	- A SPAN port is a dedicated port on a switch that is used to copy traffic from the main network to a monitoring device
	- A TAP (Test and Monitoring Point) is a specific type of SPAN port that is used for testing and monitoring network devices.
	- SPAN/TAP tools are used to extract traffic from a live network and direct it to a monitoring device for analysis, allowing security teams to monitor and analyze network traffic in real-time.
- Host-based IDS (HIDS) → monitors logs, system activity

Exam trigger:
> “Detects but does not stop” → **IDS**

#### **IPS – Intrusion Prevention System**
- **Detects AND blocks** malicious traffic
- Inline device (traffic flows through it)
- Can drop packets, reset connections, block IPs

Exam trigger:
> “Stops an attack in real time” → **IPS**

#### **IDS vs IPS Quick Table**

| Feature                 | IDS        | IPS           |
| ----------------------- | ---------- | ------------- |
| Traffic blocking        | ❌ No       | ✅ Yes         |
| Inline                  | ❌ No       | ✅ Yes         |
| Alerting                | ✅ Yes      | ✅ Yes         |
| Risk of false positives | Low impact | Higher impact |

**Exam trap:**  
If the question says _“alert only”_ → IDS  
If it says _“block/prevent”_ → IPS

---
### **Detection Methods (How Intrusions Are Identified)**

#### **2.1 Signature-Based Detection**
Matches traffic against known attack patterns (signatures).

Pros:
- Low false positives
- Accurate for known threats

Cons:
- Cannot detect zero-day attacks

Exam phrase:
> “Known attack pattern” → Signature-based detection

#### **2.2 Anomaly-Based Detection**
Establishes a **baseline** of normal behavior, then alerts on deviations.

Pros:
- Can detect unknown/zero-day attacks

Cons:
- Higher false positives

Exam phrase:
> “Behavior deviates from baseline” → Anomaly-based detection

#### **2.3 Heuristic / Behavioral Detection**
Looks for suspicious behaviors (e.g., unusual system calls, execution chains).

Often used in:
- Host-based IPS
- EDR/XDR tools
	- EDR (Endpoint Detection and Response) and XDR (Extended Detection and Response) tools are security solutions that detect and respond to cyber threats on endpoint devices, such as laptops, desktops, and mobile devices. These tools provide advanced threat detection capabilities beyond what traditional antivirus software can offer

---
### **Placement of IDS/IPS (Architecture Matters)**

#### **3.1 Network-Based IDS/IPS (NIDS/NIPS)**
Placed:
- At network perimeter
- Between segments
- At ingress/egress points (the points in a network where traffic enters or leaves the network, respectively)

Protects:
- Entire network segments

Limitations:
- Cannot inspect encrypted traffic unless TLS is terminated earlier

#### **3.2 Host-Based IDS/IPS (HIDS/HIPS)**
Runs on the endpoint/server itself.

Monitors:
- System calls
- File integrity
- Registry changes
- Log files

Strong against:
- Insider threats
- Encrypted traffic (because it’s already decrypted on host)

---
### **Inline vs Passive Monitoring**
- **Inline** → IPS (can block traffic)
- **Passive** → IDS (copy of traffic only)

Security+ often frames this as:
> “Which system could disrupt traffic if misconfigured?” → IPS

---
### **False Positives & False Negatives**
Critical exam concept.
- **False positive** = benign activity flagged as malicious
- **False negative** = malicious activity not detected

IPS tuning is required to:
- Reduce false positives (to avoid blocking legit traffic)
- Maintain detection accuracy

Exam phrase:
> “Blocking legitimate traffic” → false positive issue
---
### **Encrypted Traffic Considerations**
Modern networks use TLS everywhere.

Problem:
- IDS/IPS cannot inspect encrypted payloads by default

Solutions:
- TLS termination at load balancer or reverse proxy
- Decrypt → inspect → re-encrypt

Trade-off:
- Privacy concerns
- Performance impact
---
### **IPS vs Firewall vs WAF (Common Confusion)**

#### **Firewall**
- Controls traffic based on IPs, ports, protocols
- Does NOT inspect payload deeply

#### **IPS**
- Inspects traffic payloads for malicious patterns
- Can block attacks that pass firewall rules

#### **WAF (Web Application Firewall)**
- Protects web apps specifically
- Stops SQLi, XSS, CSRF (Continuous Authentication) is a security attack where an attacker tricks a user into executing unintended actions on a web application.
- Operates at Layer 7 (HTTP)

**Exam shortcut:**
- Network attacks → IPS
- Web attacks → WAF
---
### **Intrusion Prevention in Cloud Environments**
Cloud equivalents:
- Network IPS appliances
- Cloud-native IDS/IPS services
- Traffic mirroring for NIDS: Network-Based Intrusion Detection Systems (NIDS) is a technique used to capture and analyze network traffic in order to detect potential security threats. The concept of traffic mirroring involves duplicating or "mirroring" the original network traffic, allowing the NIDS system to inspect and analyze the traffic without affecting the original flow of data.
- Host-based agents for HIPS

Cloud-specific challenge:
- East–West traffic visibility
- Encrypted service-to-service communication

This ties back to **microsegmentation and Zero Trust**.

---
### **Automation & Response Integration**
Modern IPS systems integrate with:
- SIEM (log correlation)
- SOAR (automated response playbooks) (Security Orchestration, Automation, and Response) a set of technologies used to automate security incident response and remediation.

Example:
- IPS blocks IP
- SIEM correlates IoCs
- SOAR disables account automatically

This bridges **detection → response**, which we’ll expand on later topics.

---
### **How Intrusion Prevention Connects to Previous Topics**
This topic is a _direct continuation_ of what we’ve already covered:

| Previous Topic                                          | Connection                                            |
| ------------------------------------------------------- | ----------------------------------------------------- |
| **[[59-Secure-Infrastructure\|Secure Infrastructure]]** | IPS enforces secure network boundaries                |
| **[[52-Segmentation-&-Access-Control\|Segmentation]]**  | IPS placed between segments to stop lateral movement  |
| **[[06-Zero-Trust\|Zero Trust]]**                       | Continuous inspection of all traffic                  |
| **[[51-Indicators-Of-Compromise\|IoCs]]**               | IPS rules often trigger on IoCs                       |
| **[[53-Mitigation-Techniques\|Mitigation Techniques]]** | IPS is an active mitigation control                   |
| **[[50-Application-Attacks\|Application Attacks]]**     | IPS/WAF stop SQLi, XSS                                |
| **[[55-Cloud-Infrastructure\|Cloud Infrastructure]]**   | Host-based IPS needed for encrypted east–west traffic |
| **[[54-Hardening-Techniques\|Hardening]]**              | Proper IPS tuning reduces attack surface              |

Intrusion prevention is **where theory becomes action**.