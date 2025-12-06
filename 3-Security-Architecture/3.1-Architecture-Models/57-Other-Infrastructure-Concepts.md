# Other Infrastructure Concepts
This topic expands the infrastructure picture into the types of systems and technologies that exist **around** traditional networks:
- Virtualization support systems
- ICS / SCADA
- Remote access infrastructure
- Out-of-band management
- Proxying and brokering components
- Directory services
- Edge devices
- SDN and network virtualization

These are often tested in _scenario form_ because they’re about **choosing the right type of infrastructure for the right security requirement**.

---
### **OOB Management (Out-of-Band Management)**
_(OOB = a separate management network or interface used to administer devices even when the main network is down.)_

Purpose:
- Manage routers, switches, firewalls, servers _outside_ normal traffic paths
- Diagnose failures during outages
- Provide secure admin access without exposing management ports to production networks

Examples:
- **iLO (Integrated Lights-Out)** on HP servers
- **DRAC / iDRAC** on Dell servers
- **Console servers** that aggregate serial console ports

Security:
- Must be isolated
- MFA enforced
- No internet exposure

Exam trigger:
> “Admin access required during outages” → OOB management.

---
### **Jump Servers / Bastion Hosts**
_(A hardened, controlled system used to access sensitive networks.)_

Used when:
- Admins need to manage highly secure systems
- You want a single audited control point
- Remote access must be strictly controlled

Characteristics:
- Strong authentication
- Logging/recording of sessions
- No internet access
- Often deployed in DMZ or a management subnet

Exam phrase:
> “Administrators must first authenticate to an intermediary server before accessing internal systems” → Bastion/Jump box.

---
### **Directory Services (Core to Enterprise Infrastructure)**
Common system: **Active Directory (AD)**  
Provides:
- Centralized authentication
- Group Policy
- LDAP directory (Lightweight Directory Access Protocol—used for querying identities and attributes)
- Kerberos authentication (ticket-based SSO protocol)

Security relevance:
- Compromise of AD = total domain compromise
- Kerberoasting and Golden Ticket attacks
- Harden DCs, restrict privileged access

---
### **DHCP Infrastructure Considerations**
DHCP = IP assignment system.  
_But it’s also a classic attack vector._

Security controls include:
- DHCP snooping (switch feature that prevents rogue DHCP servers)
- Reserving IPs for known MAC addresses
- Isolation of DHCP servers

Exam scenario:
> “Users receive incorrect IP settings from an attacker’s device” → Rogue DHCP → Enabled DHCP snooping.

---
### **DNS Infrastructure Concepts**
DNS = cornerstone of network operation.  
Security+ wants you to know key security components:

##### **5.1 Split DNS (Split-Horizon DNS)**
Internal users get internal DNS answers.  
External users get external DNS answers.

Used for:
- Hiding internal infrastructure
- Preventing reconnaissance

##### **5.2 DNSSEC**
Adds cryptographic signing to DNS records to prevent tampering.

Purpose:
- Protects integrity, not confidentiality.

##### **5.3 DNS Sinkhole**
Redirects malicious DNS queries to a safe internal server.

---
### **NTP (Network Time Protocol)**
Time synchronization is critical for:
- Kerberos authentication
- Log correlation
- Certificates
- Cloud services

Security considerations:
- Use authenticated NTP or internal NTP servers
- Prevent NTP amplification attacks (a form of DDoS)

---
### **ICS / SCADA Infrastructure (Industrial Control Systems)**
SCADA = Supervisory Control And Data Acquisition  
ICS = infrastructure controlling physical devices (power grids, water treatment, factories).

Characteristics:
- Real-time operation
- Often legacy systems
- High availability required
- Cannot patch easily

Security model:
- Air-gapping or strong segmentation
- No direct internet connections
- Strict remote access controls
- Protocols like Modbus and DNP3 (usually unencrypted)

Exam tip:
> “System controls valves, pumps, industrial equipment” → ICS/SCADA.

---
### **VoIP Infrastructure (Voice Over IP)**
VoIP phones connect through network switches and communicate using SIP/RTP (signaling and voice streams).

Security concerns:
- VLAN separation recommended
- Eavesdropping if not encrypted
- SIP registration brute-force attacks
- QoS (Quality of Service) must be configured

---
### **SDN (Software-Defined Networking)**
_(SDN separates the “control plane” (decisions) from the “data plane” (traffic forwarding).)_

Key components:
- **Controller** (central brain)
- **Switches** (forwarding devices)

Security implications:
- Controller becomes a high-value target
- Policies can be enforced centrally
- Microsegmentation becomes easier

Exam trigger:
> “Dynamic, programmable network configuration” → SDN.

---
### **Virtual Network Functions (VNFs) & NFV (Network Function Virtualization)**
Instead of dedicated appliances, network services run as **virtual machines or containers**.

Examples:
- Virtual firewalls
- Virtual routers
- Virtual load balancers

Benefit:
- Scalability
- Rapid provisioning
- Automation (works with IaC)

---
### **Edge Infrastructure Concepts**

##### **11.1 CDN (Content Delivery Network)**
Globally distributed servers caching content closer to users.

Used for:
- Low latency
- DDoS protection
- Offloading origin servers

##### **11.2 SD-WAN (Software-Defined WAN)**
Uses software to dynamically route WAN traffic across multiple links (MPLS, broadband, LTE).

Security relevance:
- Encrypted tunnels
- Central policy control
- Cloud-optimized paths

---
### **Putting It All Together — Why This Topic Matters**
All of these “other” components support secure enterprise architecture:
- **OOB** → secure management
- **Jump servers** → controlled privileged access
- **Directory services** → identity backbone
- **DNS/DHCP/NTP** → foundational network services
- **ICS/SCADA** → specialized high-risk environments
- **SDN/NFV** → modern cloud-like networks
- **CDN/Edge** → performance + security distribution

These show up in scenario questions like:
- “Which infrastructure component allows secure remote administration during outages?”
- “What system provides centralized authentication for enterprise devices?”
- “Which technology lets you virtualize firewalls and routers?”

---
### How This Connects To Previous Topics
| **Infrastructure Concept**                           | **What It Is**                               | **Connection to Previous Topics**                                                                                                       | **Why It Matters for Security+**                                                  |
| ---------------------------------------------------- | -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| **OOB Management**                                   | Separate management network/interfaces       | [[54-Hardening-Techniques\|Hardening]], [[52-Segmentation-&-Access-Control\|segmentation]], [[07-Physical-Security\|physical security]] | Prevents exposure of admin interfaces; supports secure device recovery.           |
| **Jump Server / Bastion Host**                       | Controlled entry point for admin access      | [[04-Authentication-Authorization-&-Accounting\|AAA]], [[06-Zero-Trust\|Zero Trust]], privileged access control                         | Enforces least privilege and central auditing for sensitive access.               |
| **Directory Services (AD, LDAP)**                    | Centralized identity & authentication system | Authentication/Authorization/Accounting, [[11-Public-Key-Infrastructure\|PKI]], Kerberos                                                | Core to enterprise identity security; compromise = domain takeover.               |
| **DNS Infrastructure (DNSSEC, Sinkhole, Split DNS)** | Name resolution systems and protections      | [[47-On-path-Attacks\|On-path attacks]], [[51-Indicators-Of-Compromise\|IoCs]], [[50-Application-Attacks\|application attacks]]         | Prevents redirection, phishing amplification, DNS poisoning.                      |
| **DHCP Infrastructure (DHCP Snooping)**              | Automatic IP assignment service              | Network attacks, segmentation, hardening                                                                                                | Stops rogue DHCP servers (common IoC scenario).                                   |
| **NTP**                                              | Network time synchronization                 | PKI, logging, certificates, SIEM                                                                                                        | Time drift breaks Kerberos, logging correlation, and cert validation.             |
| **ICS / SCADA**                                      | Industrial control systems                   | Vulnerabilities, segmentation, physical security                                                                                        | Legacy, hard-to-patch systems → require strict isolation & compensating controls. |
| **SDN (Software-Defined Networking)**                | Centralized network control plane            | Zero Trust, segmentation, automation                                                                                                    | Enables microsegmentation and centralized policy enforcement.                     |
| **NFV / VNFs (Virtualized Firewalls, Routers)**      | Virtualized network appliances               | [[55-Cloud-Infrastructure\|Cloud infrastructure]], hardening, mitigation                                                                | Extends security controls into virtual/cloud environments.                        |
| **VoIP Infrastructure**                              | Voice over IP communication                  | Network attacks, segmentation                                                                                                           | Susceptible to eavesdropping, SIP attacks; requires isolation and QoS.            |
| **CDN / Edge Infrastructure**                        | Distributed content/service delivery         | Cloud security, [[44-Denial-Of-Service\|DDoS mitigation]]                                                                               | Offloads traffic, improves performance, and protects origin servers.              |