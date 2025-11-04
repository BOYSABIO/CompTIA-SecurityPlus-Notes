# Zero Trust (Architecture)
**Zero Trust** = *"Never trust, always verify"*

This is different from older security models and assumes:
- Every device, user, and application could be compromised
- No implicit trust exists, even within your internal network
- Access must be **continuously verified** based on identity, context, and policy

---

### Why Zero Trust Exists
Traditionally, organizations relied on *castle-and-moat* model:
- **Once you're inside** the corporate network - you're trusted
- But modern environments have **cloud services, remote users, and mobile devices**
- Compromised credentials
- Insider threats
- Misconfigured cloud access

`Zero Trust` flips the model and treats every request as if it originates from an **untrusted network**

---

### Key Principles (Messer + NIST 800-207)
| Principle | Description | Example |
| --- | --- | --- |
| Verify explicitly | Always authenticate and authorize based on *identity, location, device health, data sensitivity, etc.* | MFA, device posture checks |
| Least Privilege Access | Give users only the access they need - and for as long as they need it | Just-In-Time(JIT) access, RBAC |
| Assume Breach | Design systems as if attackers are already inside. | Microsegmentation, logging, continuous monitoring | 
| Microsegmentation | Break networks into smaller zones with granular access control | Separate internal subnets, container segmentation |
| Strong Identity Controls | Identity becomes the new **perimeter** | MFA, SSO, Identity Federation |

---

### Key Technologies Supporting Zero Trust
| Technology | Role |
| --- | --- |
| MFA (Multi-Factor Authentication) | Confirms identity using multiple factors | 
| Identity Providers (IdPs) | Manage and verify user identity (Azure AD, Okta) |
| Network Access Control (NAC) | Ensures devices meet security policy before connection |
| Microsegmentation | Divides network zones for fine-grained control |
| Software-Defined Perimeter (SDP) | Creates dynamic encrypted connections between verified entities | 
| Behavioural Analytics / Continuous Monitoring | Detects anomalies in user or device activity | 
| Conditional Access Policies | Enforce access rules based on device, location, risk score |

---

### How It Fits With AAA
