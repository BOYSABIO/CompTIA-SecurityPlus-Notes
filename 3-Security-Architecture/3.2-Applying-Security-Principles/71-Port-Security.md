# Port Security
This topic is a **direct extension of Network Appliances and Secure Infrastructure**, but now zooms in on **Layer 2 (switch-level) security controls**.

Think of Port Security as **where physical access meets logical access control**.

---
### **What Port Security Is (and Is Not)**
**Port Security** is a **Layer 2 switch feature** that:
- Restricts which devices can connect to a switch port
- Uses **MAC addresses** (hardware identifiers)
- Prevents unauthorized devices from gaining network access

Port Security is:
- Preventive
- Enforcement-based
- Often applied to access-layer switches

Port Security is **NOT**:
- Authentication (that’s NAC / 802.1X)
- Encryption
- Routing

---
### **How Port Security Works**
A switch port is configured to allow:
- A specific MAC address
- Or a limited number of MAC addresses

If a violation occurs, the switch takes action.

#### **MAC Address Types**
- **Static MAC** – manually configured (highest control)
- **Dynamic MAC** – learned automatically
- **Sticky MAC** – learned dynamically, then saved to config

Exam tip:
> “Automatically learns and remembers MAC addresses” → **Sticky MAC**

---

### **Port Security Violation Modes (Very Testable)**
#### **3.1 Protect Mode**
- Drops traffic from unknown MACs
- No alert, no port shutdown

#### **3.2 Restrict Mode**
- Drops traffic
- Generates logs/SNMP alerts
- Increments violation counter (every time a traffic drop occurs due to a violation, the violation counter is incremented. This counter keeps track of the number of times the port has been in violation, and it can be used as an indicator of potential security threats or as a trigger for automated actions such as generating logs or SNMP alerts.)

#### **3.3 Shutdown Mode (Default)**
- Puts port into **err-disabled** state
- Requires manual or automatic recovery

Exam trigger:
> “Port is disabled after violation” → **Shutdown mode**

---
### **Why Port Security Matters**
Port security protects against:
- Rogue devices
- Unauthorized laptops
- Malicious insiders
- Simple MAC flooding attacks (an attack where an attacker overwhelms a switch's Content-Addressable Memory (CAM) table with false MAC addresses, forcing the switch to drop traffic from all unknown MAC addresses. This can lead to a denial-of-service condition and is one of the security threats that Port Security aims to mitigate)

**MAC flooding** = attacker overwhelms switch CAM table to force broadcast behavior.

---
### **Port Security vs NAC (Common Exam Comparison)**

| Feature         | Port Security | NAC (802.1X)             |
| --------------- | ------------- | ------------------------ |
| Layer           | Layer 2       | Layer 2/3                |
| Auth method     | MAC address   | Credentials/certificates |
| Device identity | Weak          | Strong                   |
| Scalability     | Limited       | High                     |
| User awareness  | None          | Yes                      |

Exam shortcut:
- _Simple device restriction_ → Port Security
- _Identity-based access_ → NAC

---
### **Port Security vs Firewall (Another Exam Trap)**
- **Port security** controls _devices_ on switch ports
- **Firewalls** control _traffic between networks_

Different layers, different purposes.

---
### **Integration with Other Layer 2 Protections**
Port Security is often deployed with:
- **DHCP snooping** (prevents rogue DHCP servers)
- **Dynamic ARP Inspection (DAI)** (prevents ARP spoofing)
- **BPDU Guard** (prevents STP manipulation) (an attack where an attacker tries to manipulate the Spanning Tree Protocol (STP) to bypass security controls or cause a denial-of-service condition. This can be done by sending false bridge ID or bridge path messages to the switches, causing them to forward traffic through an unauthorized path, leading to a security breach)

Together, these form **switch hardening**.

---
### **Operational Considerations**
#### **8.1 Legitimate Changes**
Problems with:
- Desk moves
- Docking stations
- IP phones + PCs on same port

Solutions:
- Increase MAC limit
- Use sticky MAC carefully
- Prefer NAC in dynamic environments

#### **8.2 Port Recovery**
Ports in shutdown mode may:
- Require manual re-enable
- Use errdisable recovery timers

---
### **Cloud & Virtual Switch Context**
Traditional port security:
- Applies to physical switches

Cloud equivalent:
- Security groups
- Network policies
- Virtual switch ACLs

Conceptual match:
> “Restrict which endpoints can connect”

---
### **How Port Security Connects to Previous Topics**
Here’s how this fits into everything we’ve already covered:

| Previous Topic                                              | Connection                                 |
| ----------------------------------------------------------- | ------------------------------------------ |
| **[[07-Physical-Security\|Physical Security]]**             | Prevents rogue devices plugging into ports |
| **[[52-Segmentation-&-Access-Control\|Segmentation]]**      | Enforces access-layer segmentation         |
| **[[06-Zero-Trust\|Zero Trust]]**                           | Verifies devices before granting access    |
| **NAC**                                                     | Port security is a lightweight alternative |
| **[[56-Network-Infrastructure-Concepts\|Network Attacks]]** | Mitigates MAC flooding                     |
| **[[53-Mitigation-Techniques\|Mitigation Techniques]]**     | Preventive control                         |
| **[[59-Secure-Infrastructure\|Secure Infrastructure]]**     | Access-layer enforcement                   |

Port security is a **foundational access control** — simple, but very testable.