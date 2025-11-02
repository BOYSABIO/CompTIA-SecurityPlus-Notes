# Gap Analysis
*A **Gap analysis** is a comparison between where you are and where you need to be in terms of security posture or compliance*

**Here's what we're currently doing vs. what the standard or policy says we should be doing**

---

### Purpose Of A Gap Analysis
*The goal is to find the **gaps** - the msising or insufficient controls, processes, or policies - and then how to close them*

This helps:
- Identify weaknesses or areas for improvement
- Prioritize resources and security investments
- Prepare for audits or certifications (`ISO 27001`, `NIST 800-53`, `PCI DSS`, etc.)

---

### Gap Analysis Example
*In the context of complying with `NIST Cybersecurity Framework (CSF)`*

| NIST Requirement | Current Practice | Gap | Recommendation |
| --- | --- | --- | --- |
| Multi-factor authentication required | Only passwords used | **MFA MISSING** | Implement MFA for all admin logs |
| Security awareness training annually | Done quarterly | **Meets requirements** | Maintain Schedule | 

This is the gap analysis in actin - comparing actual vs desired and noting where you fall short

### Where It's Typically Used
- During a **risk assessment**
- Before a **security audit** or **certification**
- When implementing new **policies, frameworks, or regulations**
- As part of a **continuous improvement** in a security program

---

### Key Inputs & Outputs
**Inputs**:
- Organizational policies and procedures
- Industry or compliance standards like (`NIST`, `ISO`, `PCI DSS`, `HIPAA`)
- Risk assessment and previous audit reports

**Outputs**:
- Gap report listing what is missing or insufficient
- Recommendations for remediation or improvement
- Roadmap for achieving compliance or alignment

---

### Relationship To Risk Management
*A gap analysis is part of **risk management** and **security assessment***
- It's not about finding specific vulnerabilities (like a penetration test)
- It's about evaluating **processes and controls** against a framework or requirement set
- It helps identify where policies, controls, or implementations need improvement

---

### Types Of Gaps Commonly Found
| Category | Example Gap | Possible Solution |
| --- | --- | --- | 
| Technical | No encryption on backups | Implement AES encryption for backups | 
| Administrative | No incident response plan | Develop and document a plan | 
| Physical | Server room lacks access logs | Add keycard system or CCTV |
| Compliance | Missing HIPAA training | Conduct annual compliance training |

---

### Gap Analysis vs. Risk Assessment 
| Aspect | Gap Analysis | Risk Assessment | 
| --- | --- | --- | 
| Focus | Compare current vs. required state | Identity threats, vulnerabilities, and impacts | 
| Goal | Find missing or weak controls | Measure risk to determine mitigation priorities |
| Output | Gap report + remediation plan | Risk register with likelihood / impact ratings |
| Timing | Before compliance / audit | Ongoing pat of risk management |

They complement each other - gap analysis shows "what's missing", while risk assessment shows "how bad it is."

**EXAM TIP**: CompTIA may frame it like - An organization compares it's current security controls to the requirements of a new framework to determine what additional steps are needed
- This is a gap analysis and not a risk assessment, vulnerability scan, nor penetration test.

