# Resiliency
Resiliency is the ability of systems, networks, and data to:
> **Continue operating — or recover quickly — despite failures, attacks, or disasters.**

This topic focuses primarily on **availability (CIA)**, but it also touches integrity and recovery planning.

---

### **Resiliency vs Recovery (Critical Distinction)**
Security+ separates these ideas intentionally.

| Term           | Meaning                               |
| -------------- | ------------------------------------- |
| **Resiliency** | Ability to _withstand_ disruption     |
| **Recovery**   | Ability to _restore_ after disruption |

Think:
- Resiliency = _stay online_
- Recovery = _come back online_

This section is about **resiliency**.

---
### **Core Resiliency Concepts (Must Know)**
#### **2.1 Redundancy**
Having **duplicate components** so one failure doesn’t cause downtime.

Examples:
- Multiple power supplies
- Redundant routers/switches
- Multiple disks (RAID)
- Multiple ISPs

Exam trigger:
> “Eliminate single point of failure” → **Redundancy**

#### **2.2 Fault Tolerance**
The system continues operating **with no interruption** when a component fails.

Examples:
- Active/active clusters
- Hot-swappable hardware
- Synchronous replication

Fault tolerance is **stronger than redundancy**.

#### **2.3 High Availability (HA)**
Design approach to **maximize uptime**.

Characteristics:
- Fast failover
- Minimal service interruption
- Often uses redundancy + automation

Exam trigger:
> “Minimize downtime” → **High availability**

---
### **Failover & Load Distribution**
#### **3.1 Failover**
Automatic switching to a standby system when the primary fails.

Types:
- **Active/passive** (primary + standby)
- **Active/active** (both handle traffic)

Exam clue:
> “Automatically switches when failure occurs” → **Failover**

#### **3.2 Load Balancing**
Distributes traffic across multiple systems.

Benefits:
- Improved availability
- Improved performance
- Built-in redundancy

Security+ often frames load balancers as **availability controls**, not security devices.

---
### **Geographic Resiliency**
#### **4.1 Site Redundancy**
Multiple physical locations.

Types:
- Primary data center
- Secondary (hot, warm, cold) site

#### **4.2 Cloud Availability Zones & Regions**
Cloud-native resiliency:
- **Availability Zone (AZ)** = independent data center
- **Region** = geographic area

Exam trigger:
> “Survive data center outage” → **Multi-AZ deployment**

---
### **Data Resiliency (Ties Directly to Protecting Data)**
#### **5.1 Replication**
Keeping copies of data synchronized.

Types:
- **Synchronous** (real-time, low latency, costly)
- **Asynchronous** (delayed, cheaper, common)

#### **5.2 Snapshots**
Point-in-time copies of data.

Used for:
- Fast restoration
- Ransomware recovery

Snapshots ≠ backups, but they support resiliency.

---
### **Backup Strategies (Resiliency Angle)**
Even though backups are often recovery-focused, they still support resiliency planning.

Key ideas:
- **Full, incremental, differential backups**
- **Offline / immutable backups** (critical for ransomware)
- **Encrypted backups**
- **Regular testing**

Exam trigger:
> “Recover from ransomware” → **Backups**
---
### **Power & Environmental Resiliency**
Infrastructure resiliency includes **non-cyber failures**.

Controls:
- UPS
- Generators
- Redundant power feeds
- HVAC redundancy

Exam mindset:
> Availability failures aren’t always cyberattacks.
---
### **Network Resiliency**
Key controls:
- Multiple ISPs
- Redundant routers
- Dynamic routing (failover paths)
- SD-WAN (automatic path selection)

Exam trigger:
> “Maintain connectivity during link failure” → **Network redundancy**
---
### **Service-Level Metrics (Very Testable)**
Security+ expects conceptual understanding of **resiliency metrics**.

| Metric   | Meaning                                  |
| -------- | ---------------------------------------- |
| **MTBF** | Mean Time Between Failures               |
| **MTTR** | Mean Time To Repair                      |
| **RTO**  | Recovery Time Objective (max downtime)   |
| **RPO**  | Recovery Point Objective (max data loss) |

Resiliency goal:
- High MTBF
- Low MTTR

---
### **Resiliency vs Security Controls (Important Balance)**
Sometimes resiliency **conflicts** with security:
- More redundancy = more attack surface
- More replication = more data exposure

Security+ expects you to recognize **trade-offs**, not absolutes.

---
### **How Resiliency Connects to Previous Topics**
This topic ties together nearly everything we’ve covered:

| Previous Topic                                                          | Connection                 |
| ----------------------------------------------------------------------- | -------------------------- |
| **[[02-The-CIA-Triad#Availability\|CIA Triad]]**                        | Resiliency = Availability  |
| **[[58-Infrastructure-Considerations\|Infrastructure Considerations]]** | Power, cooling, redundancy |
| **[[55-Cloud-Infrastructure\|Cloud Infrastructure]]**                   | Multi-AZ, autoscaling      |
| **[[76-Protecting-Data\|Protecting Data]]**                             | Replication, backups       |
| **[[59-Secure-Infrastructure\|Secure Infrastructure]]**                 | HA design                  |
| **Incident Response**                                                   | Limit impact of incidents  |
| **[[42-Other-Malware-Types\|Ransomware]]**                              | Offline backups, snapshots |
| **[[44-Denial-Of-Service\|DDoS Attacks]]**                              | Load balancing, redundancy |

Resiliency is what **keeps the business alive** when prevention fails.