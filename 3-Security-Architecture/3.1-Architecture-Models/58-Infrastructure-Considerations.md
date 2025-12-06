# Infrastructure Considerations
This topic builds on everything we’ve done from network infrastructure, segmentation, cloud, and hardening.  
It focuses on **how the environment itself impacts security decisions** — physical, environmental, logical, and operational factors that change how infrastructure must be deployed and protected.

This is an _architecture-level_ topic: what you must consider **before** building secure systems.

---
### **Site Layout & Environmental Controls**
These considerations apply to data centers, server rooms, IDF/MDF closets, and cloud edge environments.

##### **1.1 Hot/Cold Aisles**
Rack layout pattern used to improve airflow and cooling efficiency.
- Cold aisle = intake side
- Hot aisle = exhaust side

Security relevance: overheating → outages → availability failure.

##### **1.2 Fire Suppression**
Types:
- **FM-200 / Clean Agent** (safe for electronics)
- **CO₂ systems**
- **Pre-action sprinklers**

Security+ cares because **availability (CIA)** includes environmental protections.

##### **1.3 Raised Floors / Cable Management**
Used for:
- Better cooling
- Organized cabling
- Physical access control

Risk: unprotected cabling can lead to physical tapping or cutting.

##### **1.4 UPS & Power Redundancy**
- UPS = Uninterruptible Power Supply
- Generators
- Redundant power feeds

Mitigates:
- Brownouts
- Blackouts
- Power-related equipment failure

---
### **Server & Hardware Placement**

##### **2.1 Edge Computing**
Compute/storage located closer to users or sensors to reduce latency.  
Examples: CDN nodes, IoT gateways.

Security consideration:
- Edge nodes are physically distributed → greater physical risk.

##### **2.2 Data Center Tiers**
Rated Tier I–IV by Uptime Institute.
- Tier I: basic
- Tier IV: fault-tolerant (redundant everything)

Exam tip:
> “Maximum uptime and redundancy” → Tier IV.

##### **2.3 Hardware Security Modules (HSMs)**
Physical devices dedicated to securing cryptographic keys.  
Protects:
- Encryption keys
- PKI private keys
- Cloud KMS backends (equivalent)

Security considerations:
- Tamper-resistant
- Strict physical controls
- Often used for certificate authorities

---
### **Cabling Infrastructure & Its Security Impact**

##### **3.1 Fiber vs Copper**
- **Fiber** = immune to electromagnetic eavesdropping
- **Copper** = easier to tap, limited range
- Fiber often preferred in secure environments.

##### **3.2 Plenum vs Non-Plenum Cable**
- Plenum-rated cable = fire-resistant, low smoke  
    Used in spaces that supply air (ceilings, ducts).

Exam trick:
> “Fire code requirement” → plenum cable.

##### **3.3 EMI/RFI Considerations**
Electromagnetic interference sources:
- Motors
- Fluorescent lights
- Industrial equipment

Shielded cabling (STP) protects from interference and signal leakage.

---
### **Network Connectivity Considerations**

##### **4.1 Redundant Paths**
- Multiple ISPs
- Multiple routers
- Redundant switches

Purpose:
- High availability
- Faster failover

##### **4.2 Out-of-Band (OOB) Networks**
Separate network for management → improves availability + security.  
Ties back to our previous topic directly.

##### **4.3 Link Aggregation (LACP)**
Joining multiple links for:
- Increased throughput
- Failover redundancy

Exam trigger:
> “Bond multiple NICs” → LACP.

##### **4.4 Leased Lines & MPLS**
MPLS = Multi-Protocol Label Switching (a private, carrier-managed WAN).  
Considered more secure/stable than internet VPNs.

Uses:
- Corporate WANs
- High-reliability environments

---
### **Cloud Infrastructure Deployment Considerations**
Even though we covered cloud already, this topic revisits it with a focus on **physical/architectural impact**:

##### **5.1 Region & Availability Zone Choice**
Region = geographic cluster  
AZ (Availability Zone) = independent datacenter(s) within a region

Considerations:
- Latency
- Legal requirements
- Redundancy
- Data sovereignty

##### **5.2 Hybrid Connectivity**
- Direct Connect (AWS) / ExpressRoute (Azure)  
    Direct high-speed private line between on-prem and cloud.

Benefits:
- Lower latency
- More secure than internet VPNs
- No bandwidth bottlenecks

##### **5.3 Cloud Edge Locations**
CDN POPs, caching layers, edge compute.  
Security impact:
- Distributed attack surface
- Requires global policy consistency

---
### **Facility & Physical Security Considerations**
This directly relates to earlier physical security topics but applied to infrastructure specifically:

##### **6.1 Mantraps**
Two-door system preventing piggybacking into secure rooms.

##### **6.2 Access Badges / Biometrics**
Controls who can enter server rooms or racks.

##### **6.3 Locking Cabinets & Racks**
Prevents access to sensitive equipment inside shared spaces (e.g., colocation facilities).

---
### **HVAC Considerations**
The exam actually expects familiarity with HVAC in the context of:
- Maintaining optimal temperature & humidity
- Preventing condensation (too humid)
- Preventing static discharge (too dry)

Ties into **availability** under CIA.

---
### **Environmental Monitoring**
Sensors for:
- Temperature
- Humidity
- Smoke
- Flooding
- Physical movement

Often tied to SIEM or facility monitoring systems.

---
### **Control Plane vs Data Plane (High-Level Network Architecture)**
_(If unfamiliar: I’ll define succinctly.)_
- **Control plane** = makes decisions (routing tables, policies)
- **Data plane** = forwards the actual traffic

Why this matters:
- SDN separates these planes → simplifies segmentation
- Control plane compromise = catastrophic

This links directly to our SDN section in “Other Infrastructure Concepts.”

---
### **How This Topic Connects to Everything We’ve Covered**
Here is the concise connection logic:

| Concept                    | Connects To                                                                                      | Why                                                     |
| -------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------- |
| Redundancy, UPS, power     | CIA: [[02-The-CIA-Triad#Availability\|Availability]]                                             | Infrastructure must remain online despite failures.     |
| Cooling, HVAC              | [[54-Hardening-Techniques\|Hardening]], availability                                             | Prevents physical-layer outages.                        |
| Edge computing, CDN        | [[55-Cloud-Infrastructure\|Cloud infra]], [[56-Network-Infrastructure-Concepts\|network design]] | Extends attack surface; affects latency & distribution. |
| OOB management             | Hardening, [[52-Segmentation-&-Access-Control\|segmentation]]                                    | Protects admin plane separately.                        |
| Cabling & EMI              | [[07-Physical-Security\|Physical security]], network reliability                                 | Prevents interference, eavesdropping, outages.          |
| HSMs                       | [[11-Public-Key-Infrastructure\|PKI]], [[12-Encrypting-Data\|encryption]]                        | Secure storage of cryptographic keys.                   |
| Data center tiers          | [[53-Mitigation-Techniques\|Mitigation]], availability                                           | Define expected resilience and redundancy.              |
| Mantraps, restricted racks | Physical security                                                                                | Protects servers that host critical identity/data.      |
| Hybrid links               | Cloud security, segmentation                                                                     | Secure connectivity between domains.                    |
| SDN considerations         | [[06-Zero-Trust\|Zero Trust]], segmentation                                                      | Supports dynamic enforcement of security policies.      |

Infrastructure considerations are basically the **layer beneath all other controls** — the physical + architectural foundation where all cyber controls operate.