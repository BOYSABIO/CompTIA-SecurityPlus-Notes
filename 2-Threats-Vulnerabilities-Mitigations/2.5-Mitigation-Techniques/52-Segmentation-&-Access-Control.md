# Segmentation & Access Control
**Segmentation** = dividing a network into smaller zones with controlled communication between them.

It reduces:
- attack surface
- broadcast domains
- lateral movement
- damage from breaches

It increases:
- security
- performance
- manageability

---
### **1. VLAN Segmentation**
Virtual Local Area Networks separate traffic at Layer 2.

Examples:
- VLAN 10 → Sales
- VLAN 20 → HR
- VLAN 30 → Guest Wi-Fi
- VLAN 40 → Servers

Communication between VLANs requires a **router or L3 switch**, allowing enforced ACLs.

**Exam trigger:**
> “Guests cannot access internal resources due to VLAN segmentation.”

---
### **2. Physical Segmentation**
Separate physical networks:
- air-gapped networks
- separate switches
- separate cabling

Used for:
- ICS / SCADA
- highly sensitive environments

---
### **3. Firewall Segmentation**
Firewalls separate zones via:
- DMZ
- internal LAN
- management network
- database subnet
- external internet

Applies rules based on:
- source/destination
- protocol
- user identity
- application type

---
### **4. Microsegmentation (Zero Trust)**
Next-gen segmentation:
- divides even internal networks into very small zones
- uses identity-based policies
- host-to-host restrictions

Used in:
- cloud computing
- Kubernetes
- Zero Trust environments

Exam trigger:
> “Policy restricts communication at the workload or application level.”

---
### **5. Subnetting / IP Segmentation**
Subnetting divides networks at Layer 3:
- restricts traffic
- hides internal structure
- enables routing policies
- reduces broadcast traffic

---
### Access Control Models (VERY important for the exam)
Security+ wants you to know **how permissions are enforced**.
#### **1. DAC — Discretionary Access Control**
Owner controls access.
- permissions set by owner
- common on Windows and UNIX
- flexible, but less secure

#### **2. MAC — Mandatory Access Control**
System-enforced access based on labels.

Used in:
- government
- high security environments

Labels:
- Top Secret
- Secret
- Confidential

Exam trigger:
> “Subjects and objects are assigned security labels.”

#### **3. RBAC — Role-Based Access Control**
Permissions grouped into roles.

Examples:
- HR role → access to HR systems
- Admin role → privileged access

Users inherit permissions from roles.

This is one of the most widely used enterprise models.

#### **4. ABAC — Attribute-Based Access Control**
Access based on attributes:
- user attributes (department, clearance)
- resource attributes (classification)
- environment attributes (location, time)

Allows fine-grained, dynamic access.

**Exam trigger:**
> “Access depends on user department AND time of day.”

#### **5. Rule-Based Access Control**
System applies rules like:
- deny all traffic except port 443
- block outside business hours
- allow only specific IPs

Typically implemented via
- firewalls
- routers
- NAC solutions

---
### Access Control Methods
##### ✔ ACLs (Access Control Lists)
Used to allow/deny traffic or permissions.

Types:
- File system ACLs
- Network ACLs
- Router/switch ACLs
- Firewall rules

ACLs operate on:
- IP
- protocol
- port
- direction

Exam trigger:
> “Traffic denied by ACL rule.”

##### ✔ Port Security
Switch-level access control:
- bind specific MAC addresses
- limit # of MAC addresses on a port
- shut down port on violation

Defends against:
- CAM table overflow
- rogue devices

##### ✔ 802.1X Authentication
Used for:
- wired networks
- wireless networks

Provides:
- network access control
- port-based authentication
- integration with RADIUS

Stops rogue devices from automatically connecting.

##### ✔ NAC (Network Access Control)
Validates devices before granting access.

Checks:
- OS version
- patches
- antivirus enabled
- compliance posture

Types:
- **Pre-admission NAC** (before access)
- **Post-admission NAC** (continuous monitoring)

##### ✔ Implicit Deny
Critical firewall concept.

Rules operate top to bottom.  
If no rule matches → traffic is **denied**.

Exam trigger:
> “Traffic was blocked because no rule allowed it.”

---
### Principle of Least Privilege (Foundational)
Users and systems receive the **minimum access necessary** to perform their tasks.

Violations include:
- admin accounts for normal tasks
- global read access
- shared passwords
- overprivileged service accounts

---
### Privilege Creep
Users accumulate permissions over time as job roles change.  
Violates least privilege.

Mitigation:
- regular audits
- access reviews
- role recertification

---
### Separation of Duties
No single person should control critical processes end-to-end.

Purpose:
- reduce fraud
- prevent abuse
- enforce checks and balances

Examples:
- developer cannot deploy code to production
- financial approval requires 2 people

---
### Dual Control
A variation of separation of duties:
- requires two people to complete a sensitive action  
    (e.g., launching missiles, accessing a vault)

---
### Segmentation + Access Control = Zero Trust Architecture
Zero Trust enforces:
- verify every request
- no implicit trust
- microsegmentation
- continuous authentication
- least privilege everywhere

“Never trust, always verify.”

---
# How This Connects to Everything You've Learned

| Topic                                                     | Connection                                      |
| --------------------------------------------------------- | ----------------------------------------------- |
| **[[47-On-path-Attacks\|On-path attacks]]**               | Segmentation reduces ARP poisoning blast radius |
| **[[39-An-Overview-Of-Malware\|Malware]]**                | Least privilege prevents malware escalation     |
| **[[06-Zero-Trust\|Zero Trust]]**                         | Segmentation + access control = Zero Trust core |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud security]]** | ABAC and microsegmentation are cloud-native     |
| **[[46-Wireless-Attacks\|Wireless attacks]]**             | 802.1X prevents rogue device access             |
| **[[01-Security-Controls\|Management controls]]**         | Separation of duties + access reviews           |
