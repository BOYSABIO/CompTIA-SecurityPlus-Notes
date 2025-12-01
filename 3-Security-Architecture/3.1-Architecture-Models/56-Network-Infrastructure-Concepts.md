# Network Infrastructure Concepts
This topic is core Security+ material. It explains **how networks are built**, **how traffic moves**, and **where security controls fit into the topology**.

This is _not_ about configuration — that was segmentation & hardening.  
This is about the **fundamental components** that make a secure network.

---
### **Basic Network Building Blocks**
These are the physical + logical components that make a network function.

##### **1.1 Routers**
Devices that forward traffic between networks using IP addresses.  
They define the network’s **routing boundaries**.

Security relevance:
- ACLs (Access Control Lists)
- Routing security (preventing route injection attacks)

##### **1.2 Switches**
Devices that forward traffic within a network using MAC addresses.  
Operate at **Layer 2** (data link).

Security relevance:
- VLANs (Virtual LANs—network segmentation inside a switch)
- Port security (restricting devices allowed per port)
- STP (Spanning Tree Protocol—prevents switching loops)

##### **1.3 Firewalls**
Devices that permit or deny traffic based on rules.

Types:
- **Packet filtering firewall** (simple IP/port filtering)
- **Stateful firewall** (remembers active sessions)
- **Next-Gen Firewall** (application-aware, can inspect payloads)

Exam trigger:
> “Application identification” → Next-gen firewall.

##### **1.4 Load Balancers**
Distribute incoming traffic across multiple backend servers.

Types:
- **Layer 4 load balancing** (TCP/UDP-based)
- **Layer 7 load balancing** (HTTP/HTTPS application-aware)

Benefits:
- Scalability
- Redundancy
- DDoS resistance

---
### **Key Network Infrastructure Concepts**

##### **2.1 DMZ (Demilitarized Zone)**
A network segment exposed to the internet but isolated from internal networks.  
Used for:
- Public web servers
- Reverse proxies
- Email gateways

Exam trick:
> “Add a buffer between the internet and internal LAN → DMZ.”

##### **2.2 Network Segmentation**
Breaking a network into smaller isolated units using:
- VLANs
- Firewalls
- Subnets
- ACLs

Purpose:
- Reduce attack surface
- Limit lateral movement
- Improve performance

##### **2.3 Air Gaps**
Physical separation between networks (no connection at all).

Used in:
- SCADA systems
- Industrial control systems
- High-security environments

##### **2.4 Proxy Servers**
Servers that mediate traffic between clients and the internet.

Types:
- **Forward proxy** (client → proxy → internet)
- **Reverse proxy** (internet → proxy → internal servers)

Reverse proxies are crucial for:
- Load balancing
- Hiding internal structure
- TLS termination (decrypting traffic before forwarding)

##### **2.5 VPNs (Virtual Private Networks)**
Encrypted tunnels across untrusted networks.

Types:
- **IPsec VPN** (common site-to-site VPN technology)
- **SSL VPN** (browser-based remote access)

Purpose:
- Confidentiality
- Integrity
- Remote access

##### **2.6 NAC (Network Access Control)**
Enforces device authentication before granting network access.  
Often uses **802.1X** (standard for port-based authentication).

> “Prevent unknown devices from plugging into Ethernet ports → NAC.”

---
### **Network Address Translation (NAT)**

##### **3.1 Purpose of NAT**
Conserve IP addresses and hide internal systems.

Types:
- **PAT (Port Address Translation)** — many internal hosts share one public IP.
- **Static NAT** — one-to-one mapping between internal and public addresses.

Security note:  
NAT is _not_ security by itself, but provides **basic [[15-Obfuscation|obfuscation]]**.

---
### **Routing Concepts**

##### **4.1 Static Routing**
Manually configured routes.  
Pros: predictable, secure  
Cons: no automatic failover

##### **4.2 Dynamic Routing**
Routers share routes automatically using routing protocols:

Examples:
- **OSPF** (Open Shortest Path First—internal routing)
- **BGP** (Border Gateway Protocol—used on the internet)

Security concern:
- Route injection attacks (malicious manipulation of routing tables)

---
### **High Availability Network Concepts**

##### **5.1 Redundancy**
- Multiple routers
- Multiple load balancers
- Multiple connections

Purpose: eliminate single points of failure.

##### **5.2 Clustering**
Multiple devices act as one logical unit.

Examples:
- Firewalls in active/standby mode
- Load balancer clusters

##### **5.3 NIC Bonding / Link Aggregation (LACP)**
Combines network interfaces for:
- Higher throughput
- Redundancy

---
### **Wireless Infrastructure Concepts (High-Level)**
Cloud + enterprise often mix wired and wireless.

Components:
- **WLC (Wireless LAN Controller)** — centralized AP management
- **CAPWAP** (Control And Provisioning of Wireless Access Points—protocol connecting APs to WLCs)
- **SSID** (network name)
- **MIMO** (multiple antennas increasing throughput)

Security issues:
- Rogue APs
- Evil twin attacks
- Misconfigured encryption

---
### **Putting It All Together (Exam Framing)**
Security+ expects you to know **how** these components form a secure architecture:
- DMZ protects public-facing assets
- Segmentation isolates sensitive subnets
- Proxies hide internal servers
- Load balancers increase availability
- Firewalls control trust boundaries
- VPNs secure remote access
- NAT hides internal IPs
- Routers control traffic paths
- Switches control internal traffic flow
- NAC ensures only authorized devices connect

---
### **Linking to Previous Topics (Memory Reinforcement)**
This topic directly reinstates prior security concepts:
- **[[52-Segmentation-&-Access-Control|Segmentation]]** → VLANs, ACLs, subnets
- **[[53-Mitigation-Techniques|Mitigation]]** → firewalls, proxies, NAC
- **[[54-Hardening-Techniques|Hardening]]** → secure device configuration, disable unused ports
- **[[06-Zero-Trust|Zero Trust]]** → identity everywhere + microsegmentation
- **[[51-Indicators-Of-Compromise|Indicators of Compromise]]** → route anomalies, ARP poisoning, rogue DHCP
- **[[50-Application-Attacks|Application attacks]]** → reverse proxy and WAF sit inside this architecture
- **[[55-Cloud-Infrastructure|Cloud infrastructure]]** → VPCs mimic these concepts virtually

Understanding this section makes the cloud and on-prem models merge conceptually.