# Cloud Infrastructure
Cloud Infrastructure in Security+ is about _how cloud environments are built, managed, isolated, and secured_.  
This topic is foundational because **every other cloud security control sits on top of this architecture**.

This is not about "basic cloud definitions" — we already assume technical literacy.  
Instead, this will focus on the Security+-relevant architecture concepts tested on the exam.

---
### **Cloud Deployment Models (Exam Core)**
Security+ cares heavily about the _shared responsibility model_ and distinctions between cloud types.

##### **1.1 Public Cloud**
- Multitenant (shared hardware)
- Hosted by provider (AWS, GCP, Azure)
- Most scalability and elasticity
- Most common exam scenario for misconfigurations (S3 bucket exposure, open security groups)

**Security responsibilities:**
- Cloud provider: infra, hardware, hypervisor
- Customer: identity, access control, data, misconfigurations

##### **1.2 Private Cloud**
- Single-tenant
- Full control of networking + hardware
- Enables stricter compliance
- Often seen in government or high-regulated industries

Exam trigger:  
“Data sovereignty, complete control, regulatory requirement → Private cloud.”

##### **1.3 Hybrid Cloud**
- Mix of on-prem + cloud
- Requires secure connectivity (VPN or direct connect)
- Identity federation and SSO often needed

Exam trigger:  
“Legacy systems must remain on-prem, but scalability needed → Hybrid.”

##### **1.4 Community Cloud**
- Shared by organizations with common goals
- Rarely deployed but appears in questions
- Example: Universities, research alliances

---
### **Cloud Service Models (IaaS / PaaS / SaaS / FaaS)**

##### **2.1 IaaS (Infrastructure as a Service)**
You manage:
- OS
- Network segmentation
- Patch management
- Applications

Provider manages:
- Datacenter
- Hardware
- Hypervisor

**Exam attack surface:**
- Misconfigured VMs
- Open ports
- Poor access control
- Insecure virtual networking

##### **2.2 PaaS (Platform as a Service)**
You manage:
- Code
- Application config

Provider manages:
- OS
- Runtime
- Middleware
- Scaling

Common risk:
- Insecure API keys / tokens
- Dependency vulnerabilities

##### **2.3 SaaS**
You only use the application.  
Security responsibility is mostly identity + data governance.

Risks:
- Weak authentication
- Poor access control
- Data leakage between tenants (rare but tested)

##### **2.4 FaaS / Serverless**
You deploy functions; provider handles runtime, scaling, patching.

Security focus:
- Permissions of the function
- Event triggers
- Excessive IAM privileges

Exam trigger:  
“Event-driven architecture with minimal management → FaaS/serverless.”

---
### **Virtualization & Multi-Tenancy**
Cloud = virtualization at massive scale.  
The exam wants you to understand the _security implications_:

##### **3.1 Hypervisor Security**
- Hypervisor is critical; compromise = access to every tenant
- Provider hardens + patches it
- Customers have no direct access

**[[33-Virtualization-Vulnerabilities#**Guest-to-Host Escape (VM Escape)**|VM escape]]** is a key threat concept:  
Malicious code escapes the VM sandbox → reaches hypervisor or other VMs.

##### **3.2 Multi-Tenancy**
Multiple customers share physical hardware.

Security implications:
- Strict isolation required
- Shared backplane networks
- Side-channel attacks (cache timing) are theoretically possible

Exam trigger phrase:  
“Ensuring one customer cannot access another tenant’s workloads → enforce virtualization isolation.”

---
### **Cloud Networking Infrastructure**
Cloud networking functions similarly to on-prem but virtualized.

##### **4.1 Virtual Private Clouds (VPCs)**
Your “private network” inside the cloud.

Includes:
- Subnets
- Routing tables
- Security groups
- Network ACLs
- NAT gateways
- Internet gateways

**Security groups vs NACLs (very testable):**

| Feature          | Security Group   | Network ACL         |
| ---------------- | ---------------- | ------------------- |
| Stateful         | Yes              | No                  |
| Applied to       | Instance level   | Subnet level        |
| Rule direction   | Ingress & egress | Inbound & outbound  |
| Default behavior | Deny all         | Allow all (usually) |

##### **4.2 Peering & Direct Connectivity**
- VPC-to-VPC peering = encrypted internal connection
- VPN/dedicated line = hybrid cloud link
- Transit gateways → multi-VPC routing

Exam trigger:  
“Connect multiple VPCs securely without exposing public internet → VPC Peering.”

---
### **Identity & Access in Cloud Infrastructure**
Identity is the #1 attack surface in cloud.

##### **5.1 IAM Fundamentals (Cloud-Specific)**
- Least privilege roles
- Policies & JSON-based ACLs
- Role assumption
- Temporary credentials
- MFA for console & API access

##### **5.2 Service Accounts / Machine Identities**
Very exam-relevant
- EC2 instance roles
- Workload identities
- Access tokens

Attack surface:
- Over-permissioned roles (“*” permissions)
- Long-lived secrets
- Hard-coded credentials

---
### **Cloud Storage Infrastructure**

##### **6.1 Object Storage (S3/GCS/Azure Blob)**
Most common misconfiguration:  
**Public access enabled unintentionally.**

Risks:
- Data leakage
- Unencrypted data at rest
- Improper lifecycle policies

Exam trigger:  
“Unrestricted bucket access → fix ACLs/policies.”

##### **6.2 Block Storage**
Used for virtual disks (EBS, Azure Disk).  
Security focus:
- Encryption at rest
- Snapshot security
- KMS-managed keys

---
### **Elasticity & High Availability Architecture**
Cloud infra provides built-in mechanisms for resilience:
- Autoscaling groups
- Load balancers (Layer 4/7)
- Multi-AZ deployments
- Replication across regions

Security considerations:
- Replicated data must be encrypted
- IAM roles propagate across regions
- Misconfigurations replicate too

Exam trigger:  
“Application must scale dynamically → use autoscaling + load balancer.”

---
### **Infrastructure as Code (IaC)**
IaC tools: Terraform, CloudFormation, ARM templates.

Security implications:
- Version-controlled infrastructure
- Declarative, reproducible configs
- Misconfigurations can scale instantly
- Template scanning required

Exam concept:  
“IaC drift detection” = ensuring live systems match declared config.

---
### **Shared Responsibility Model (Very High Exam Weight)**
The backbone of cloud security questions.

Simplified:

| Layer          | Customer  | Provider |
| -------------- | --------- | -------- |
| Data           | ✔️        |          |
| IAM            | ✔️        |          |
| Apps           | ✔️        |          |
| OS             | IaaS only |          |
| Virtualization |           | ✔️       |
| Physical       |           | ✔️       |
| Networking     | Shared    | Shared   |

Exam trick:  
People often mistakenly think “SaaS means no security responsibility.”  
Wrong → identity & data are always the customer’s responsibility.

---
### **Connecting Back to Previous Topics**
This topic ties directly to:
- **Segmentation** → VPCs, subnets, SGs, NACLs
- **[[53-Mitigation-Techniques|Mitigation techniques]]** → least privilege, patching, template scanning
- **[[51-Indicators-Of-Compromise|Indicators of compromise]]** → cloud logs (CloudTrail, Monitor)
- **[[50-Application-Attacks|Application attacks]]** → insecure APIs, misconfigured serverless functions
- **[[54-Hardening-Techniques|Hardening techniques]]** → IAM role hardening, disabling public access
- **[[06-Zero-Trust|Zero Trust]]** → identity-driven, deny-by-default cloud architecture
- **[[14-Encryption-Technologies|Encryption topics]]** → KMS, storage encryption, key rotation

Cloud infrastructure is where all previous layers converge.