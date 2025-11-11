# Authentication, Authorization & Accounting (AAA)
These three form the core of how organizations manage **access control** and **user accountability**. They always work together in this order:
1. **Authentication** - Who are you?
2. **Authorization** - What are you allowed to do?
3. **Accounting** - What did you do?

---

### Authentication - Verifying Identity
*Can you prove you are who you say you are?* 

This step confirms a user's identity **before granting access**.

| Factor Type | Description | Example |
| --- | --- | --- | 
| Something you know | Knowledge-based | Passwords, PINs, security questions | 
| Something you have | Possession-based | Smart card, key fob, phone token |
| Something you are | Inherence-based | Fingerprint, face scan, iris pattern | 
| Somewhere you are | Location-based | Geolocation, IP address | 
| Something you do | Behavioral | Typing rhythm, gait recognition |

**Multi-Factor Authentication (MFA)** = using *two or more* different factors (not two of the same type).
Could be using a password(something you know), as well as fingerprint(something you are).

As a cybersecurity professional, you will have access to thousands or more devices that could be located around the world and most of the time, you will never even see them. So you need to be able to verify that a computer that is trying to connect is authorized. To provide this further authentication, in many cases a `certificate` is put onto the device that is digitally signed and that is checked during the login process. That proves that it is a company device.
- You must have a **Certificate Authority** (CA). This is responsible for managing all those certificates
- The organization creates a certificate for a device and then digitally signs the certificate with the organization's **Certificate Authority (CA)** to be able to verify later that it is real
- You put that certificate on the laptop as an authentication factor and the CA's digital signature is used to validate the certificate

---

### Authorization - Granting Access
*Now that I know who you are, what are you allowed to do?*
Once authenticated, the system checks **permissions and privileges** to determine access.

Common Authorization Models:

| Model                                     | Description                          | Example                                         |     |
| ----------------------------------------- | ------------------------------------ | ----------------------------------------------- | --- |
| **RBAC** (Role-Based Access Control)      | Access based on job role             | HR role -> access to payroll data               |     |
| **MAC** (Mandatory Access Control)        | Access based on classification level | Top Secret vs Secret clearance                  |     |
| **DAC** (Discretionary Access Control)    | Owner sets permissions               | File owner sets read/write access               |     |
| **ABAC** (Attribute-Based Access Control) | Based on attributes and policies     | "Allow if department = finance & location = HQ" |     |

`Authorization` happens after `Authentication`

`Authorization Model` will be used for authorization. There are many different models. Users will have access to certain types of data or applications. The way in which you scale this to many users is by taking this authorization model and putting it in the middle between the users and services right before you access. 
- No auth model would mean you would have to manually do the authorization for each user and each user could be completely different. 
- Therefore you use an Authorization model or **Abstraction** which creates a clear relationship between the user and the resource.
- Administration becomes streamlined as it is easier to udnerstand the authorizations and it supports any number of users or resources.
- This is done by creating almost a group for a function for example and that group itself has access to certain areas so you don't have to manually map each user but just add them to a group.

---

### Accounting - Tracking Activity
*What did you do while you were logged in?*

This is about **monitoring, logging, and auditing** user actions.

Examples:
- Logging user logins and logouts
- Tracking changes to files or configurations
- Auditing access to sensitive data
- Using network monitoring systems (like RADIUS/TACACS+)

Why it matters:
- Supports `non-repudiation` (proof of who did what)
- Enables `incident response` and compliance reporting

---

### AAA in Real-World Use
**RADIUS** and **TACACS** are `AAA` protocols used in networks
- **RADIUS**: Centralized authentication for VPNs, wireless, remote access
- **TACACS+**: Cisco protocol, seperates authentication, authorization, and accounting for better control.

You'll often see `AAA` mentioned alongside `RADIUS Server` in questions on the exam.

Both **RADIUS** and **TACACS+** are protocols that hand `Authentication`, `Authorization`, and `Accounting` for users who are trying to connect to a network service like a VPN, switch, wifi, etc. 
- **RADIUS**: Like a bouncer at the network door, who checks ID by calling a central secruity office before letting you in. Originally used for dial-up connections but now used for:
    - Wi-Fi authentication (like WPA2-Enterprise)
    - VPNs and remote access servers
    - Network devices (routers, switches, firewalls)

The main advantages include a centralized user management system to add or revoke users, it is suppoed by nearly all network equipment and it handles authentication for large remote user bases (like enterprises, universities, ISPs). On the other hand, the disadvantages include that it runs on UDP (less reliable, no guaranteed delivery), only the password is encrypted so other data is visible and less tunneled, and it combines `Authentication` and `Authorization` together so it has less granular control.

- **TACACS+**: More of an advanced and secure cousin of `RADIUS` and is mainly used in enterprise network infrustructure - like routers, switches, and firewalls - especially in Cisco environments. Same general idea (centralized AAA), but some key differences:
    - The network device (like a cisco router), sends login info to the **TACACS+ server**
    - The server handles `Authentication`, `Authorization`, and `Accounting` as three seperate functions
    - The **TACACS+ server** returns detailed permissions like "allow access to show commands only" and logs on all activity

The main advantages are that it has a strong encryption for all communication, it has better control - per command authorization, it uses TCP for reliable delivery, and it is designed for managing administrative access to network devices. On the other hand, the limitiations include, that it is slightly more complex to set up, and it is not as widely supported outside enterprise or Cisco environments. 

---

### How It Flows Together
1. You enter your username & password -> **AUTHENTICATION**
2. System checks your group/role -> **AUTHORIZATION**
3. System logs your login, commands, and logout time -> **ACCOUNTING**

**IMPORTANT NOTE:**
- `Authentication` = proving identity
- `Authorization` = granting permissions 
- `Accounting` = logging actions
- `Non-repudiation` often depends on `Accounting` logs and **Digital Signatures**
- MFA != strong password - it's about different factor categories, not multiple passwords

---

### Simple Practical Example
*Logging into a VPN server so you can then access an internal file server*

1. Client on internet, provides username & password to firewall / VPN concentrator
2. Concentrator has no information about usernames etc. This is stored on central server or AAA server. This server recieves a copy of the username and password and the request
3. If the match is true, the AAA Server will send info back to the concentrator saying that they are approved or denied
4. Concentrator allows access to the internal file server
