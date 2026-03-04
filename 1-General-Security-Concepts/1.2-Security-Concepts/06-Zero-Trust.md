# Zero Trust (Architecture)
**Zero Trust** = *"Never trust, always verify"*

This is different from older security models and assumes:
- Every device, user, and application could be compromised
- No implicit trust exists, even within your internal network
- Access must be **continuously verified** based on identity, context, and policy

Once through the firewall, there are relatively few security controls. The change is towards `Zero Trust` which is the authentication and verification everytime for every user when something is wanted to be accessed. 

---

### Why Zero Trust Exists
Traditionally, organizations relied on *castle-and-moat* model:
- **Once you're inside** the corporate network - you're trusted
- But modern environments have **cloud services, remote users, and mobile devices**
- Compromised credentials
- Insider threats
- Misconfigured cloud access

`Zero Trust` flips the model and treats every request as if it originates from an **untrusted network**

**Adaptive Identity**: This is where you are examining the identity of an individual and applying security controls on them based on all information and not just what the identity tells us. This might be the source, where the data is located, where their IP address is located, if they match for example. Just in general used to make identification or authentication stronger. 

**Threat Scope Reduction**: Limit the amount of places that one can use in order to get into the network. Limit entry points to people only in the building or through a VPN ONLY. 

**Policy Driven Access Control**: Once all are implemented, you can then create a policy driven access control that examines all of the individual data points, puts them together, and then decides what type of authentication process should be taken. 

---

### Key Principles (Messer + NIST 800-207)
| Principle | Description | Example |
| --- | --- | --- |
| Verify explicitly | Always authenticate and authorize based on *identity, location, device health, data sensitivity, etc.* | MFA, device posture checks |
| Least Privilege Access | Give users only the access they need - and for as long as they need it | Just-In-Time(JIT) access, RBAC |
| Assume Breach | Design systems as if attackers are already inside. | Microsegmentation, logging, continuous monitoring | 
| Microsegmentation | Break networks into smaller zones with granular access control | Separate internal subnets, container segmentation |
| Strong Identity Controls | Identity becomes the new **perimeter** | MFA, SSO, Identity Federation |

**Splitting the network** into various smaller components. This is called seperate planes of operation. And these control planes can be applied. You can have a plane for data (part of device performing actual security process). May be switch, router, or firewall that is processing the frames, packets, and network data in real time. The data plane would be processing forwarding, trunking, encrypting, NAT. It needs to have management and control and this would be performed in the Control plane. (Policies / rules)

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

**On a Physical Device**: For example a switch. At the bottom of the switch you have the data plane as all the data runs through there. However this plane needs some policies or control and these changes would all take place in the Control plane which is the top part of the device. It's not just specific to physical devices but could be virtual. Also applies to cloud based security controls. 

**Security Zones**: This allows to expland from a 1-to-1 relationship of a user logging into a system, into an overall path of the conversation. (Where connecing from and where connecting to) (Untrusted network to trusted network). Could even create seperate VPN's for seperate functions. Automatically deny access from untrusted zones to trusted. 

---

### How It Fits With AAA
`Zero Trust` extends AAA principles across the entire environment:
- **Authentication**: Continuous and context-aware (not just once at login)
- **Authorization**: Dynamic (permissions reevaluated in real time)
- **Accounting**: Full visibility of user behaviour and system activity

Essentially, `Zero Trust` is `AAA` + `Modern Verification` applied everywhere - not just at the perimeter.

---

### Example In Practice
**Without Zero Trust (Old Model)**
- A user logs into the corporate VPN once and gets broad network access.

**With Zero Trust**
1. User logs in with MFA `Authentication`
2. Device health is checked (up to date, encrypted drive, secure network)
3. Access granted only to specific apps or data `Authorization`
4. Activity is monitored and logged `Accounting`
5. If behaviour deviates (login from new country, odd data access), session is terminated or re-authenticated

**Benefits**
- Reduces attack surface
- Limites lateral movement inside networks
- Improves visibility and control
- Enhances compliance and incident response

**Challenges**
- Requires cultural and architectural change
- Complex integration (identity, network, endpoint)
- Continuous monitoring demands automation and analytics tools

**POLICY ENFORCEMENT POINT**: Any subjects or systems communicating through this network will be subject to the Policy Enforcement Point (PEP). These subjects and systems are users or systems or applications. It's almost like a gatekeeper and traffic must pass through in order to make authorization decisions. Usually this would be multiple devices working together in order to test authentication.
- **IMPORTANT**: This does not provide the decision. It gathers all the information and provides it to a **Policy Decision Point**
- This examines the authentication and makes a decision as to whether it is allowed. 

**POLICY ENGINE**: Evaluates each access decision based on policy and other information sources (grant, deny, or revoke)

**POLICY ADMINISTRATOR**: Communicates with **Policy Enforcement Point**, generates access tokens or credentials, and tells the PEP to allow or disallow access.

**ACROSS ALL PLANES**:
1. Starts with Subject / System
2. Communicating from an untrusted zone and through the policy enforcement point
3. If there is a policy that needs to take place, this PEP will provide that to the policy administrator which communicates to the policy decision as to whetehr this traffic is allowed
4. Result is passed down to the Policy Administrator which provides that to the policy enforcement point
5. If traffic is allowed, the policy enforcement point the provides the traffic to the trusted zone.

---

**Exam Tip**: CompTIA may frame it like, "An organization wants to move away from a perimeter-based model and enforce continuous authentication and verification for all users and devices." The answer would be `Zero Trust` and not **defence-in-depth** (that's layered security), and not `Least Privilege` alone (that's part of `Zero Trust`).

---

## Related Notes
- [[04-Authentication-Authorization-&-Accounting]]
- [[52-Segmentation-&-Access-Control]]
- [[59-Secure-Infrastructure]]
