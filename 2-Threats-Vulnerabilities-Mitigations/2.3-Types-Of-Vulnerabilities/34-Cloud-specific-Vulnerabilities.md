# Cloud-specific Vulnerabilities
Cloud introduces **new attack surfaces** because the infrastructure is abstracted, multi-tenant, API-driven, and externally exposed.  
This category covers vulnerabilities that **only — or mostly — exist due to cloud architecture**, not traditional on-prem servers.

---
### **Misconfigurations (the #1 real-world cloud risk)**
This is the single biggest category. Almost all cloud breaches stem from **incorrect settings**, not exploits.

Examples:
- **Open S3 buckets** → public data exposure
- **Overly permissive IAM roles** (e.g., `*:*` permissions)
- **Unsecured API endpoints**
- **Open storage containers** (Azure Blob, GCS buckets)
- **Misconfigured security groups** (0.0.0.0/0 inbound SSH or RDP)
- **Publicly exposed databases** (MongoDB, Redis)

Why it happens:
- Cloud is “secure by design,” not “secure by default.”
- Users misconfigure shared responsibility settings.

**CIA impact:**  
Huge [[02-The-CIA-Triad#Confidentiality|confidentiality]] risk.

**Exam trigger:** “Misconfigured cloud storage was publicly accessible.”

---
### **IAM (Identity & Access Management) Weaknesses**
Cloud IAM is **incredibly complex**; attackers love it.

Common issues:
- Overly broad permissions (“admin everywhere”)
- Lack of MFA
- Long-lived access keys
- Credential leakage via GitHub or CI pipelines
- Stolen API keys
- Roles assumed via privilege escalation inside cloud accounts (IAM privilege escalation)

IAM failures = **root account compromise**, worst case.

**Exam trigger:** “Access keys leaked” → Cloud IAM vulnerability.

---
### **Insecure APIs (Cloud Control Plane Attacks)**
Every cloud environment exposes APIs:
- AWS: API Gateway, S3 API, EC2 API
- Azure: ARM API
- GCP: Cloud APIs

Vulnerabilities:
- Unauthenticated endpoints
- Weak authentication
- Lack of rate limiting
- Excessive permissions
- Injection attacks
- Poorly written cloud-based microservices

If APIs are exposed, **attackers can control cloud resources directly**.

**Exam trigger:** “Exposed management API” or “Unauthenticated cloud endpoint.”

---
### **Multi-Tenancy Risks**
You share hardware with other customers → increases the attack surface.

Types of risks:
- [[33-Virtualization-Vulnerabilities#**Guest-to-Host Escape (VM Escape)**|Hypervisor escape]]
- Side-channel attacks (Spectre, Meltdown)
- Data leakage between tenants due to shared memory or CPU cache
- Misconfigured virtual networks

This ties directly into **virtualization vulnerabilities**.

**Exam trigger:** “Shared resources across customers.”

---
### **Data Remanence**
Residual data left behind after storage deallocation.

Example:
- A cloud provider reassigns a disk block to a new customer
- Data wasn’t properly wiped
- New tenant can recover fragments

Cloud platforms must zero out blocks — but misconfigurations or older systems can fail.

**Exam trigger:** “Residual cloud storage data accessible by new users.”

---
# **Insecure Cloud Networking**
Cloud networks rely on:
- Virtual firewalls
- Routing tables
- VPCs / VNets
- Load balancers
- Subnets

Issues include:
- Wrong security group rules
- Misconfigured VPC peering
- Open management ports
- No segmentation between subnet tiers
- Shared networks allowing sniffing or ARP spoofing

**Exam trigger:**  
“Security group misconfigured to allow inbound 0.0.0.0/0.”

---
### **Insufficient Logging & Monitoring**
Cloud logs often need to be explicitly turned on:
- CloudTrail (AWS)
- Azure Monitor
- GCP Cloud Logging

Failures:
- Logging disabled for storage, API calls, or IAM
- No log retention
- No alerting (SIEM integration missing)

This is a **shared responsibility model** issue.

---
### **Shadow Admin Roles (Privilege Escalation via IAM)**
Cloud IAM is full of tricky permission paths.

Example:  
A user doesn’t have “Admin” directly, but has:
- permission to attach roles to themselves
- or modify Lambda policies
- or create new API keys

This leads to privilege escalation inside cloud accounts.

**Exam trigger:** “A non-admin user escalated privileges through role misconfiguration.”

---
### **Insecure Serverless / Containers / Microservices**
These cloud-native technologies introduce:

**Serverless vulnerabilities**
- Overprivileged execution role
- Event injection (malicious SQS → Lambda)
- Cold-start credential leakage

**Container vulnerabilities**
- Insecure images
- Outdated base layers
- Container breakout
- Shared kernel vulnerabilities

**Microservice vulnerabilities**
- API attacks
- Request forgery
- Service mesh misconfigurations
- Unencrypted service-to-service traffic

---
### **Infrastructure-as-Code (IaC) Vulnerabilities**
Tools: Terraform, CloudFormation, ARM.

Risks:
- Hard-coded secrets in templates
- Misconfigured security groups baked into deployment
- Drift between IaC configs and actual settings
- Untracked changes bypass change management

This ties to **[[09-Change-Management|Technical Change Management]]**.

---
### **Cloud Supply Chain Risks**
Cloud-specific supply chain issues include:
- Compromised base images
- Compromised cloud AMIs
- Poisoned container registries
- Forged IaC templates
- Dependency attacks in CI/CD pipelines
- Tampered cloud marketplace items

This ties directly to **[[28-Malicious Updates|Malicious Updates]]** and **[[20-Common-Threat-Vectors#Supply Chain & Third-Party Threats|Supply Chain Attacks]]**.

---
### **Billing/Resource Abuse (Cryptojacking)**
Attackers compromise cloud credentials and spin up:
- GPU instances
- High-end compute nodes
- Thousands of containers

→ You get a massive bill.

**Exam Trigger:**  
“Unexpectedly high cloud compute charges.”

