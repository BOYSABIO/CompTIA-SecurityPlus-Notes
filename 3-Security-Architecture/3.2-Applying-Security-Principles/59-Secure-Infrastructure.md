This topic builds directly on everything we’ve been doing with infrastructure, but now shifts to **how to secure the infrastructure holistically** — from design principles to the security controls applied to hardware, networks, cloud, and supporting systems.

Think of this as the _security architecture layer_ above the infrastructure concepts we’ve already covered.

---
### **Security Architecture Principles**
These are the foundational principles used to secure infrastructure at scale:

##### **1.1 Defense in Depth**
Layered protections so that if one control fails, others still block the attack.

Example layers:
- Network segmentation
- Firewalls
- IDS/IPS
- MFA
- Application allowlisting
- Logging + monitoring

Exam trigger:
> “Multiple overlapping controls” → Defense in depth.

##### **1.2 Least Privilege**
Give identities, systems, and services **only the permissions they require**.

Applied to:
- IAM roles
- Admin accounts
- API keys
- Firewall rules
- Serverless functions

We’ve touched this everywhere — now it becomes an architectural requirement.

##### **1.3 Zero Trust Architecture**
Never trust by default — verify every connection, every identity, every request.

Applied through:
- Microsegmentation
- Strong identity verification
- Device health checks
- Continuous authorization

Exam shorthand:
> “Never trust, always verify” = Zero Trust.

##### **1.4 Secure-by-Default / Secure-by-Design**
Systems should ship with secure settings without requiring extra configuration.

Examples:
- Default disablement of insecure protocols
- Strong cipher suites shipped by default
- Containers running non-root by default

---
### **Network Security Architecture**
This topic focuses on how to build a network layout that is inherently secure.

##### **2.1 DMZ Design (Demilitarized Zone)**
Public-facing but isolated zone hosting:
- Web servers
- Email gateways
- Reverse proxies

DMZ protects internal networks from the internet.

##### **2.2 East-West vs North-South Traffic**
_(New term, so brief explanation)_
- **North–South:** Traffic entering/leaving the datacenter
- **East–West:** Internal traffic moving within the datacenter

Why it matters:
- Attackers often spread using East–West movement → segmentation must address this.

##### **2.3 Microsegmentation**
Small, granular network segments secured individually.

Tools:
- SDN
- Host firewalls
- Cloud security groups

Purpose:
- Limit lateral movement
- Enforce Zero Trust

##### **2.4 Secure Routing & Switching**
Key components:
- ACLs
- DHCP snooping
- Dynamic ARP inspection
- BPDU Guard (protects STP from manipulation)

These protect against classic Layer 2/3 attacks.

---
### **Server & Application Infrastructure Security**

##### **3.1 Hardened Baselines**
All servers must adhere to:
- CIS benchmarks
- Vendor best practices
- Disabled unused services
- Secure protocols only

##### **3.2 Jump Servers / Privileged Admin Workstations**
Critical for securing admin access.

Admins **never** log directly into production servers from personal workstations.

##### **3.3 Certificate Management & PKI Integration**
Infrastructure requires:
- Proper SSL/TLS
- Certificate rotation
- Revocation checking (OCSP, CRL)
- Protection of private keys (HSM recommended)

---
### **Virtualized Infrastructure Security**

##### **4.1 Hypervisor Security**
Hypervisor = layer below all VMs; compromise = catastrophic.

Controls:
- Patch hypervisor
- Restrict admin access
- Use hardware virtualization extensions (VT-x, AMD-V)
- Protect VM escape surfaces

##### **4.2 Secure VM Templates / Images**
Golden images must be:
- Hardened
- Patched
- Free of unnecessary software
- Scanned for vulnerabilities

##### **4.3 VM Isolation & Virtual Firewalls**
VMs should be isolated via:
- Virtual switches
- Virtual firewalls
- L2/L3 segmentation inside the hypervisor

This ties back to SDN/NFV from earlier.

---
### **Container Infrastructure Security**
Containers differ from VMs — they share a host kernel.

Key controls:
- Enforce **non-root** containers
- Signed images (to prevent malicious images)
- Image scanning (SCA = Software Composition Analysis)
- Network policies for east-west container communication
- Limit container capabilities (using Linux namespaces/cgroups)

---
### **Cloud Infrastructure Secure Architecture**
The exam expects you to map on-prem concepts to cloud patterns:

##### **6.1 Security Groups (cloud firewalls)**
Stateful, instance-level rules.

##### **6.2 Network ACLs**
Stateless, subnet-level rules.

##### **6.3 Private Endpoints**
Private access to cloud services without touching the public internet.

##### **6.4 IAM Role Segmentation**
Identity replaces network trust boundaries in the cloud.

##### **6.5 WAF and API Gateways**
Protect cloud-native applications.

---
### **Infrastructure Monitoring & Observability**

##### **7.1 SIEM Integration**
Infrastructure logs feed into:
- Network logs
- Firewall logs
- IDS/IPS
- CloudTrail (AWS)
- Azure Monitor

Exam triggers:
> “Detect early-stage attacks” → central logging + SIEM.

##### **7.2 Metrics & Health Monitoring**
Tools like:
- SNMPv3 (secure version of Simple Network Management Protocol)
- NetFlow / IPFIX (traffic flow analytics)

Used to detect:
- Baseline deviations
- IoCs
- Network anomalies

---
### **Resilience & High Availability Infrastructure**
Secure infrastructure = **available infrastructure**.

Components:
- Load balancers
- Failover clusters
- Redundant uplinks
- UPS + generators
- Multi-AZ cloud deployments

Availability is just as important as confidentiality.

---
### **How “Secure Infrastructure” Connects to Previous Topics**

Quick table summary:

| Previous Topic                                              | Connection                                                 |
| ----------------------------------------------------------- | ---------------------------------------------------------- |
| **[[54-Hardening-Techniques\|Hardening]]**                  | Secure baselines, disabling services, hardened images      |
| **[[52-Segmentation-&-Access-Control\|Segmentation]]**      | Microsegmentation, secure routing, East–West isolation     |
| **[[06-Zero-Trust\|Zero Trust]]**                           | Continuous verification, identity-based access, jump boxes |
| **[[55-Cloud-Infrastructure\|Cloud Infrastructure]]**       | SGs/NACLs, IAM-based access, secure endpoints              |
| **[[56-Network-Infrastructure-Concepts\|Network Attacks]]** | ARP protection, secure L2, rogue DHCP defenses             |
| **[[53-Mitigation-Techniques\|Mitigation Techniques]]**     | Defense in depth, least privilege, secure design           |
| **[[51-Indicators-Of-Compromise\|IoCs]]**                   | Network flow anomalies, C2 detection, SIEM correlations    |
| **[[50-Application-Attacks\|Application Security]]**        | WAF, secure routing to apps, API gateways                  |

This topic essentially **ties the entire Security+ architecture model together**.