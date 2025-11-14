# Supply Chain Vulnerabilities
A **supply chain vulnerability** is any weakness that allows an attacker to compromise a product **before it reaches you** — meaning during development, manufacturing, distribution, or updating.

> In simple terms:  
> Instead of attacking YOU, the attacker compromises someone YOU depend on.

This applies to:
- Software
- Hardware
- Firmware
- Cloud services
- APIs
- 3rd-party libraries
- Distribution and update channels
- Developers and tools you rely on

---
### Why Supply Chain Attacks Are So Dangerous
Because they exploit **trust**.

When you install an update or buy hardware, you _trust_ the vendor.  
Attackers aim to compromise that trust and push malicious components downstream.

Impact:
- Integrity loss
- [[02-The-CIA-Triad#Confidentiality|Confidentiality]] loss (backdoors)
- Execution of arbitrary code
- Compromise of entire infrastructure
- Often goes undetected for months or years

---
### Types of Supply Chain Vulnerabilities

#### **Compromised Software Updates (Malicious Updates)**
You already studied this — it’s the MOST common supply chain issue.

Examples:
- SolarWinds Orion backdoor
- CCleaner compromised installer
- NotPetya via MeDoc update

Exam triggers:
- “Signed update contained malware”
- “Vendor update server compromised”
- “Customers installed backdoored patch”

#### **Compromised Development Environments**
Attackers compromise the **build pipeline** or developer systems:
- Poisoned source code repository
- Malicious modifications to build scripts
- Compromised CI/CD pipeline
- Stolen [[18-Certificates|signing certificates]]
- Dependency injection attacks

Example:  
Attackers modify software during compilation → shipped to customers.

#### **3rd-Party Libraries and Dependencies**
Modern software relies heavily on external code:
- Open-source libraries
- Package managers (npm, pip, Maven, RubyGems)
- Container base images

Risks:
- Typosquatting (e.g., "reqests" instead of "requests")
- Malicious pull requests
- Dependency confusion
- Outdated or vulnerable libraries
- Backdoored packages

This is where Log4j falls in terms of widespread dependency vulnerability.

#### **Hardware and Firmware Tampering**
Hardware supply chain risks include:
- Counterfeit components
- Malicious chips added to motherboards
- Tampered NICs or embedded implants
- Malicious modifications to firmware (BIOS, UEFI, BMC)

ties to → **[[32-Hardware-Vulnerabilities|hardware vulnerabilities]]**

#### **Cloud Supply Chain (Cloud Dependencies)**
Cloud-specific supply chain risks:
- Malicious AMIs or container images
- Compromised cloud marketplace products
- Manipulated templates (Terraform, CloudFormation)
- Vendor service compromise (e.g., SaaS incident)
- Compromised API or identity provider

ties to → **[[34-Cloud-specific-Vulnerabilities|Cloud-Specific Vulnerabilities]]**

#### **Logistic / Physical Supply Chain**
Vulnerabilities in the **transport and handling** of hardware:
- Tampered packages
- Interception during shipping
- Devices modified before delivery
- Insider threats at warehouses or distributors

ties to → **Physical Security**

#### **Vendor Management Vulnerabilities**
Weaknesses in vendor processes:
- No code signing
- Weak security culture
- Outdated development practices
- Poor patch management
- Lack of secure SDLC
- No integrity verification pipeline

ties to → **[[09-Change-Management|Change Management]]** + **Governance**

---
### Major Real-World Examples (CompTIA loves these)

|Incident|Description|
|---|---|
|**SolarWinds (2020)**|Attackers compromised the vendor build system → backdoored Orion updates.|
|**CCleaner (2017)**|Vendor servers served malware-infected installers.|
|**NotPetya (2017)**|Accounting software update used to deliver destructive malware.|
|**ASUS Live Update (2019)**|Malicious update signed with ASUS’ certificate.|
|**Kaspersky USB supply chain attack**|Malware added to hardware pre-delivery.|

These demonstrate that supply chain attacks target **trusted providers**, not customers directly.

---
### How Supply Chain Attacks Work (Stages)
1. Compromise vendor or intermediary
2. Modify software, hardware, or update mechanism
3. Sign or disguise malicious component
4. Deliver to customers
5. Malicious code executes with **trusted** privileges
6. Maintain stealth and persistence

This is why **[[06-Zero-Trust|zero-trust]]** is important — trust nothing by default.

---
### Mitigations (CompTIA Exam Favorites)

#### **Vendor Management Controls**
- Vet vendors
- Require security policies
- Review SOC 2 / ISO 27001 compliance
- Contractual security requirements

#### **Integrity Controls**
- Code signing
- Hash verification
- SBOM (Software Bill of Materials)
- File integrity monitoring (FIM)

#### **Secure SDLC / CI/CD Pipeline**
- Signed commits
- Secure build systems
- Dependency scanning
- SAST/DAST tests
- Verified images and registries

#### **Zero Trust Architecture**
- Don’t trust internal updates by default
- Validate everything
- Least privilege

#### **Network Controls**
- Segmentation
- Monitor unusual traffic from trusted applications
- Restrict update servers

#### **Hardware Supply Chain Security**
- Tamper seals
- Trusted vendors
- Hardware attestation
- Firmware verification

#### **Cloud Controls**
- Validate templates
- Use trusted registries
- Scan images
- Apply principle of least privilege

---
### Connections to Earlier Topics

| Previous Topic                                                            | Relevance                                    |
| ------------------------------------------------------------------------- | -------------------------------------------- |
| **[[28-Malicious Updates\|Malicious Updates]]**                           | A _subset_ of supply chain attacks           |
| **[[32-Hardware-Vulnerabilities\|Hardware Vulnerabilities]]**             | Hardware implants & firmware tampering       |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud-specific Vulnerabilities]]** | Untrusted AMIs / marketplace images          |
| **[[06-Zero-Trust\|Zero Trust]]**                                         | Supply chain attacks break trust assumptions |
| **[[16-Hashing-&-Digital-Signatures\|Hashing & Digital Signatures]]**     | Used to verify integrity of supply chain     |
| **[[09-Change-Management\|Change Management]]**                           | Ensures updates are validated and authorized |
