# Capacity Planning
**Capacity planning** is the process of ensuring that systems have **sufficient resources** to:
- Handle **normal workloads**
- Absorb **peak demand**
- Survive **failures or attacks**
- Support **future growth**

From a Security+ lens, capacity planning primarily protects:
> 🔺 **[[02-The-CIA-Triad#Availability|Availability]] (CIA triad)**
---
### **Why Capacity Planning Is a Security Topic**
Poor capacity planning leads to:
- Performance degradation
- Service outages
- Self-inflicted denial-of-service conditions
- Inability to recover during incidents

Security+ treats **availability failures** as security failures — even if no attacker is involved.

---
### **Key Capacity Resources (Know These Categories)**
Capacity planning considers **multiple resource types**, not just CPU.
#### **3.1 Compute Capacity**
Examples:
- CPU cores
- CPU utilization %
- VM instance size
- Container limits

Exam clue:
> “High CPU usage causing slow response” → compute capacity issue

#### **3.2 Memory Capacity**
Examples:
- RAM
- Swap usage
- Memory pressure

Memory exhaustion can:
- Crash applications
- Kill processes
- Cause kernel panics

#### **3.3 Storage Capacity**
Examples:
- Disk space
- IOPS (Input/Output Operations Per Second — how fast storage can read/write)
- Throughput

Exam trigger:
> “Logs stop writing / database fails” → storage capacity issue

### **3.4 Network Capacity**
Examples:
- Bandwidth
- Throughput
- Latency

Security angle:
- Insufficient bandwidth = easy DoS
- Bottlenecks affect VPNs, backups, replication

---
### **Baseline vs Peak Usage (Extremely Testable)**
#### **Baseline**
Normal, expected usage under regular conditions.
#### **Peak**
Highest expected usage (sales events, backups, patch windows).

Security+ often asks:
> “System works normally but fails during peak usage”  
> → Capacity planning failure
---
### **Capacity Planning and Resiliency (Direct Link)**
Capacity planning supports resiliency by:
- Ensuring **failover systems can handle full load**
- Supporting **redundant components**
- Preventing overload during outages

Key concept:
> Redundancy without capacity = false resiliency
---
### **Overprovisioning vs Underprovisioning**
#### **Overprovisioning**
Provisioning more resources than needed.

Pros:
- High availability
- Performance headroom

Cons:
- Cost
- Waste

#### **Underprovisioning**
Provisioning too few resources.

Risks:
- Service outages
- Performance degradation
- Availability incidents

Security+ usually frames underprovisioning as the **problem**.

---

### **Scalability (Closely Related but Distinct)**
Capacity planning determines **how much** you need.  
Scalability determines **how you grow**.

#### **7.1 Vertical Scaling**
Add more resources to one system.

Example:
- More CPU/RAM to a server

Limit:
- Hardware ceiling

#### **7.2 Horizontal Scaling**
Add more systems.

Example:
- More servers behind a load balancer

Security+ preference:
> Horizontal scaling = more resilient
---
### **Cloud Capacity Planning**
Cloud does not eliminate capacity planning — it **changes it**.
#### **8.1 Autoscaling**
Automatically adds/removes resources based on demand.

Examples:
- CPU-based scaling
- Request-count scaling

Exam trigger:
> “Handle sudden traffic spikes” → autoscaling
---
#### **8.2 Reserved vs On-Demand Capacity**
- Reserved = cheaper, predictable
- On-demand = flexible, expensive

Poor planning here can cause:
- Cost overruns
- Resource exhaustion

---
### **Capacity Planning and Security Controls**
Security tools consume resources too:
- IDS/IPS
- Logging
- SIEM ingestion
- Encryption overhead
- DLP inspection

Exam insight:
> “Security controls slow down the system” → capacity planning oversight
---
### **Monitoring & Metrics (Feeds Capacity Planning)**
Capacity planning relies on **monitoring data**:
- CPU utilization
- Memory usage
- Disk growth
- Network throughput
- Error rates

Tools:
- Performance monitoring
- SIEM
- NMS (Network Management Systems)

Exam clue:
> “Identify trends over time” → monitoring + capacity planning
---
### **Capacity Planning Failures (Exam Scenarios)**
Security+ loves subtle failures like:
- Backup jobs failing due to disk exhaustion
- Log retention filling storage
- Failover systems unable to handle full load
- DDoS overwhelming limited bandwidth

All of these are **capacity planning problems**, not configuration bugs.

---
### **How Capacity Planning Connects to Previous Topics**

| Previous Topic                                          | Connection                                  |
| ------------------------------------------------------- | ------------------------------------------- |
| **[[77-Resiliency\|Resiliency]]**                       | Capacity ensures redundancy actually works  |
| **Availability (CIA)**                                  | Prevents outages from overload              |
| **[[44-Denial-Of-Service\|DDoS Attacks]]**              | Bandwidth capacity determines survivability |
| **[[55-Cloud-Infrastructure\|Cloud Infrastructure]]**   | Autoscaling and elasticity                  |
| **Monitoring & Logging**                                | Metrics inform planning                     |
| **Incident Response**                                   | Systems must survive response activity      |
| **[[77-Resiliency#\|Backups & Recovery]]**              | Storage and network capacity required       |
| **[[59-Secure-Infrastructure\|Secure Infrastructure]]** | Controls add resource overhead              |

Capacity planning is the **invisible foundation** of availability.