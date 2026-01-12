# Data Types and Classifications
This topic answers **two core questions**:
1. **What kind of data is this?** (data type)
2. **How sensitive is it?** (classification)

Security+ tests your ability to **apply the correct control based on data sensitivity**, not just memorize labels.

---
### **Why Data Classification Exists (Big Picture)**
Organizations classify data to:
- Apply **appropriate security controls**
- Meet **legal and regulatory requirements**
- Reduce **risk of data leakage**
- Enable **least privilege access**
- Decide **encryption, retention, and disposal policies**

> 💡 **Exam mindset:**  
> If the question asks _“Which data requires the strongest protection?”_ → classification is the driver.

---
### **Common Data Classification Levels (Very Testable)**
These labels vary by organization, but Security+ expects you to recognize the **conceptual hierarchy**.

| Classification                       | Meaning                     | Typical Controls                |
| ------------------------------------ | --------------------------- | ------------------------------- |
| **Public**                           | Intended for public release | No special controls             |
| **Internal**                         | Business use only           | Basic access control            |
| **Confidential**                     | Sensitive business data     | Encryption, ACLs                |
| **Restricted / Highly Confidential** | Severe impact if leaked     | Strong encryption, MFA, logging |

Exam trigger:
> “Most sensitive data” → **Restricted / Highly Confidential**

---
### **Government / Regulatory Classification (Know the Pattern)**
Security+ may reference **government-style labels**, even if you don’t work in gov.

| Level            | Meaning                   |
| ---------------- | ------------------------- |
| **Unclassified** | Public or low sensitivity |
| **Confidential** | Some damage if disclosed  |
| **Secret**       | Serious damage            |
| **Top Secret**   | Grave damage              |

You don’t need clearance rules — just **relative sensitivity**.

---
### **Data Types (This Is Where Exams Get Tricky)**
Security+ loves scenarios where you must identify the **type of data**, then choose the **right protection**.

#### **4.1 Personally Identifiable Information (PII)**
_(Data that identifies an individual.)_
Examples:
- Full name
- SSN
- Driver’s license number
- Passport number
- Date of birth

Risk:
- Identity theft
- Privacy violations

Controls:
- Encryption
- Access control
- DLP (Data loss prevention.) - A set of strategies and tools used to prevent unauthorized access, use, disclosure, disruption, modification, or destruction of sensitive data.

#### **4.2 Protected Health Information (PHI)**
_(PII + health/medical data.)_
Examples:
- Medical records
- Diagnoses
- Insurance info

Regulation:
- HIPAA (US)

PHI is **always sensitive**.

#### **4.3 Financial Information**
Examples:
- Credit card numbers
- Bank account details
- Transaction records

Often regulated by:
- PCI DSS (Payment Card Industry Data Security Standard)

Exam trigger:
> “Credit card data” → **PCI DSS applies**

#### **4.4 Intellectual Property (IP)**
_(Data that gives a business competitive advantage.)_
Examples:
- Source code
- Trade secrets
- Proprietary algorithms
- Product designs

Risk:
- Competitive loss

Controls:
- Strict access control
- Encryption
- NDA enforcement

#### **4.5 Operational Data**
Examples:
- Network diagrams
- Internal procedures
- Configuration files

Often overlooked but **highly sensitive**.

#### **4.6 Authentication Data**
Examples:
- Passwords
- Hashes
- API keys
- Tokens
- Private keys

This data is **always restricted**, even internally.

---
### **Data States (Extremely Important)**
Data protections depend on **where the data is**.

| State               | Meaning         | Example         |
| ------------------- | --------------- | --------------- |
| **Data at Rest**    | Stored data     | Disk, database  |
| **Data in Transit** | Moving data     | Network traffic |
| **Data in Use**     | Being processed | Memory (RAM)    |

Controls:
- At rest → disk/database encryption
- In transit → TLS / IPsec
- In use → memory protection, trusted execution

Exam trigger:
> “Protect data while being transmitted” → **encryption in transit**
---
### **Data Ownership Roles (Governance Concept)**
Security+ expects you to understand **who is responsible for data**.

| Role               | Responsibility                      |
| ------------------ | ----------------------------------- |
| **Data Owner**     | Classifies data, defines protection |
| **Data Custodian** | Implements controls                 |
| **Data Steward**   | Manages data quality and usage      |
| **User**           | Uses data appropriately             |

Exam trigger:
> “Who decides classification?” → **Data Owner**
---
### **Handling Requirements Based on Classification**
Higher classification → stronger controls.

Examples:
- **Restricted data**:
    - Encryption (at rest & transit)
    - MFA
    - Logging & monitoring
    - Limited access
- **Public data**:
    - No encryption required
    - Minimal access controls

Security+ tests **mapping**, not memorization.

---
### **Data Lifecycle (Where Classification Applies)**
Classification applies throughout the **entire lifecycle**:
1. Creation
2. Storage
3. Use
4. Sharing
5. Archival
6. Destruction

Exam trigger:
> “Ensure data is securely destroyed” → **data lifecycle management**
---
### **Cloud & Data Classification**
Cloud introduces **new risks**:
- Misconfigured storage (public buckets)
- Over-shared access
- Replicated data across regions

Key idea:
> **Data sensitivity does not change just because it’s in the cloud.**

Controls must follow classification.

---
### **How This Topic Connects to Previous Topics**
This topic **ties together many things we’ve already covered**:

| Previous Topic                                            | Connection                                |
| --------------------------------------------------------- | ----------------------------------------- |
| **DLP**                                                   | Protects sensitive data types             |
| **[[14-Encryption-Technologies\|Encryption]]**            | Based on data state & sensitivity         |
| **[[52-Segmentation-&-Access-Control\|Access Control]]**  | Least privilege depends on classification |
| **[[34-Cloud-specific-Vulnerabilities\|Cloud Security]]** | Misclassified data → exposure             |
| **[[73-Secure-Communication\|Secure Communication]]**     | Protects data in transit                  |
| **[[06-Zero-Trust\|Zero Trust]]**                         | Identity-based access to sensitive data   |
| **Incident Response**                                     | Breach severity depends on data type      |
| **Compliance**                                            | Regulations map to data types             |

Data classification is the **decision engine** behind most security controls.