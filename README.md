# Windows IT Support & Active Directory Administration Lab

A hands-on Windows IT support and systems administration lab designed to simulate a small business Active Directory environment.

This project demonstrates practical experience with **Windows Server 2022, Active Directory Domain Services (AD DS), DNS, Windows 11 domain clients, Group Policy, user and group administration, network configuration, authentication, and structured troubleshooting**.

The lab was independently designed and built to strengthen practical skills relevant to **L1 IT Support, Service Desk, Desktop Support, Technical Support, and Junior Systems Administration** roles.

---

## Project Overview

The goal of this lab was to build and administer a functional Windows domain environment from the ground up.

The environment simulates a small organization called **Albion Corporation**, with centralized identity management provided by a Windows Server 2022 domain controller and Windows 11 client computers.

The project covers the complete workflow from:

**Server deployment → Network configuration → Active Directory → DNS → Users & Groups → Group Policy → Domain Join → Authentication → Troubleshooting → Verification**

Rather than only configuring individual technologies, the lab focuses on understanding how these components work together in a real IT support environment.

---

## Business Scenario

Albion Corporation requires a centralized Windows environment where IT administrators can:

* Manage employee accounts centrally
* Organize users by department
* Control access using security groups
* Apply standardized security policies
* Authenticate Windows clients against Active Directory
* Manage DNS for the internal domain
* Join Windows workstations to the corporate domain
* Troubleshoot authentication and connectivity issues
* Establish repeatable administrative procedures

The lab was designed to replicate these requirements in an isolated virtual environment.

---

## Lab Architecture

```text
                         Internet
                            │
                           NAT
                            │
                  ┌─────────────────────┐
                  │ Windows Server 2022  │
                  │        DC            │
                  │                     │
                  │ AD DS               │
                  │ DNS                 │
                  │ Group Policy        │
                  │ Domain Controller   │
                  │                     │
                  │ 192.168.56.20       │
                  └──────────┬──────────┘
                             │
                    Host-Only Network
                    192.168.56.0/24
                             │
                  ┌──────────┴──────────┐
                  │                     │
          ┌───────────────┐     ┌───────────────┐
          │ Windows 11    │     │ Future Clients │
          │ Domain Client │     │ / Lab Systems  │
          │               │     │                │
          │ 192.168.56.10 │     │    Planned     │
          └───────────────┘     └───────────────┘
```

### Network Configuration

| Device     | Role                    | IP Address      | DNS             |
| ---------- | ----------------------- | --------------- | --------------- |
| `DC`       | Domain Controller / DNS | `192.168.56.20` | Local DNS       |
| Windows 11 | Domain Client           | `192.168.56.10` | `192.168.56.20` |

**Subnet:** `255.255.255.0`

The Host-Only network provides isolated communication between the domain controller and Windows 11 client, while NAT provides external connectivity where required.

---

# Technologies Used

### Microsoft / Windows

* Windows Server 2022
* Windows 11
* Active Directory Domain Services
* DNS
* Group Policy
* Active Directory Users and Computers
* Organizational Units
* Security Groups
* Domain Authentication
* Windows networking

### Administration & Troubleshooting

* PowerShell
* Command Prompt
* `gpupdate`
* `gpresult`
* `ipconfig`
* `ping`
* `nslookup`
* `whoami`
* `hostname`

### Virtualization

* Oracle VirtualBox
* NAT networking
* Host-Only networking

---

# Implementation

## 1. Windows Server 2022 Deployment

A Windows Server 2022 virtual machine was deployed using Oracle VirtualBox.

The server was configured as the primary domain controller for the lab environment.

### Server Configuration

* Hostname: `DC`
* Operating System: Windows Server 2022
* Role: Domain Controller
* DNS Server: Enabled
* Network: Host-Only + NAT

The initial server configuration was verified before proceeding with Active Directory deployment.

---

## 2. Static IP & DNS Configuration

The domain controller was configured with a static IP address:

```text
IP Address:      192.168.56.20
Subnet Mask:     255.255.255.0
```

The Windows 11 client was configured with:

```text
IP Address:      192.168.56.10
Subnet Mask:     255.255.255.0
Preferred DNS:   192.168.56.20
```

Using the domain controller as the client's DNS server is critical for reliable Active Directory name resolution and domain authentication.

---

## 3. Active Directory Domain Services

Active Directory Domain Services was installed and the Windows Server was promoted to a domain controller.

### Domain

```text
corp.albion.local
```

### Configuration

* New forest created
* DNS Server installed
* Global Catalog enabled
* Domain Controller configured
* NetBIOS name: `CORP`
* Forest functional level: Windows Server 2016
* Domain functional level: Windows Server 2016

The domain controller was restarted after promotion and verified before continuing with client configuration.

---

## 4. Active Directory Organizational Structure

A basic organizational structure was created to represent different departments.

```text
corp.albion.local
│
├── Users
│   ├── IT
│   ├── HR
│   ├── Finance
│   └── Sales
│
└── Groups
```

Organizational Units provide a logical structure for managing users and applying administrative policies.

---

## 5. Test User Accounts

Four test users were created to simulate employees from different departments.

| User          | Username  | Department |
| ------------- | --------- | ---------- |
| Alex Morgan   | `amorgan` | IT         |
| Taylor Morgan | `tmorgan` | HR         |
| Jordan Lee    | `jlee`    | Finance    |
| Sarah Chen    | `schen`   | Sales      |

These accounts were used to test domain authentication and group-based administration.

---

## 6. Security Groups

Department and administrative security groups were created.

```text
IT-Admins
IT-Support
HR-Users
Finance-Users
Sales-Users
```

### Group Membership

| Group         | Assigned User |
| ------------- | ------------- |
| IT-Admins     | Alex Morgan   |
| IT-Support    | Alex Morgan   |
| HR-Users      | Taylor Morgan |
| Finance-Users | Jordan Lee    |
| Sales-Users   | Sarah Chen    |

The groups were configured as **Global Security Groups**.

This demonstrates a basic role-based approach to account and access management.

---

# 7. Group Policy

A domain-level Group Policy Object named:

```text
Corp-Password-Policy
```

was created and linked to the domain.

The policy establishes standardized password and account lockout requirements.

## Password Policy

Configured settings include:

| Policy                  | Configuration |
| ----------------------- | ------------- |
| Password history        | 5 passwords   |
| Maximum password age    | 90 days       |
| Minimum password age    | 1 day         |
| Minimum password length | 8 characters  |
| Password complexity     | Enabled       |
| Reversible encryption   | Disabled      |

## Account Lockout Policy

| Policy            | Configuration      |
| ----------------- | ------------------ |
| Lockout threshold | 5 invalid attempts |
| Lockout duration  | 15 minutes         |
| Reset counter     | 15 minutes         |

These controls simulate common baseline security requirements used in Windows enterprise environments.

---

# 8. Windows 11 Domain Client

A Windows 11 virtual machine was configured as the domain client.

### Network Configuration

```text
IP Address:      192.168.56.10
Subnet Mask:     255.255.255.0
Preferred DNS:   192.168.56.20
```

Connectivity to the domain controller was verified before attempting the domain join.

---

# 9. Domain Join & Authentication

The Windows 11 workstation was successfully joined to:

```text
corp.albion.local
```

A domain user was then used to verify centralized authentication.

Example verification:

```cmd
whoami
```

Expected result:

```text
corp\amorgan
```

The domain controller responsible for authentication was also verified using:

```cmd
echo %LOGONSERVER%
```

Expected result:

```text
\\DC
```

This demonstrates successful communication between the Windows 11 client and the Active Directory domain controller.

---

# 10. DNS Verification

DNS resolution was tested from the Windows 11 client using:

```cmd
nslookup DC
```

and:

```cmd
nslookup corp.albion.local
```

Active Directory DNS service is particularly important because Windows domain operations depend heavily on DNS for locating domain controllers and services.

---

# 11. Group Policy Verification

Group Policy processing can be verified from the Windows 11 client using:

```cmd
gpupdate /force
```

followed by:

```cmd
gpresult /r
```

The expected result is that:

```text
Corp-Password-Policy
```

appears under:

```text
Applied Group Policy Objects
```

This provides evidence that the domain policy is being processed by the Windows client.

---

# Troubleshooting Methodology

The lab was approached using a structured IT troubleshooting methodology:

```text
Identify
   ↓
Investigate
   ↓
Isolate
   ↓
Resolve
   ↓
Verify
   ↓
Document
```

### Examples

During domain configuration, DNS and network connectivity were verified before attempting domain operations.

Useful troubleshooting commands included:

```cmd
ipconfig /all
ping 192.168.56.20
nslookup DC
nslookup corp.albion.local
whoami
hostname
gpupdate /force
gpresult /r
```

This approach helps separate **network problems, DNS problems, authentication problems, and Group Policy problems** instead of treating them as a single issue.

---

# Evidence & Verification

Screenshots are included in the repository to document key implementation stages.

Current evidence:

```text
screenshots/
├── 01-server-baseline.png
├── 02-static-ip-dns.png
├── 03-domain-join.png
├── 04-domain-login-verification.png
├── 05-domain-computer-in-ad.png
├── 07-password-policy.png
└── 07b-account-lockout-policy.png
```

The screenshots provide visual evidence of the server configuration, networking, domain join, authentication, Active Directory computer object, and security policy configuration.

Additional verification evidence can be added as the lab is expanded.

---

# IT Support Scenarios

This environment can be used to simulate common entry-level IT support incidents, including:

### Account & Authentication

* User cannot log in
* Password-related issues
* Domain authentication failures
* Account lockout
* Incorrect credentials

### Windows & Endpoint

* Windows client cannot communicate with the domain
* DNS configuration problems
* Incorrect IP configuration
* Domain connectivity problems
* Group Policy not applying

### Active Directory

* User account administration
* Group membership changes
* Organizational Unit placement
* Computer account management
* Authentication troubleshooting

Each scenario can be approached using structured incident triage, technical investigation, resolution, verification, and documentation.

---

# Security Considerations

The lab demonstrates several foundational security concepts:

* Centralized identity management
* Role-based security groups
* Password complexity requirements
* Password expiration
* Account lockout protection
* Organizational Unit structure
* Group Policy-based configuration

A production environment would require additional security controls such as:

* Multi-factor authentication
* Privileged Access Management
* Microsoft Entra ID integration
* Endpoint protection
* Windows Defender configuration
* LAPS
* Tiered administrative accounts
* Security auditing
* SIEM integration
* Centralized logging
* Least-privilege access
* Network segmentation
* Backup and recovery procedures

---

# Future Lab Expansion

The project can be extended with additional enterprise administration scenarios.

Planned areas include:

* File server deployment
* NTFS permissions
* Shared folder permissions
* PowerShell administration
* Additional Group Policy configurations
* Windows troubleshooting scenarios
* User onboarding/offboarding workflows
* Permission troubleshooting
* Software deployment
* Remote administration
* Security auditing
* Additional Windows clients

These additions will further develop practical Windows infrastructure and IT support skills.

---

# Repository Structure

```text
Windows-IT-Support-Active-Directory-Lab/
│
├── README.md
│
├── screenshots/
│   ├── 01-server-baseline.png
│   ├── 02-static-ip-dns.png
│   ├── 03-domain-join.png
│   ├── 04-domain-login-verification.png
│   ├── 05-domain-computer-in-ad.png
│   ├── 07-password-policy.png
│   └── 07b-account-lockout-policy.png
│
├── documentation/
│
├── powershell/
│
└── troubleshooting/
```

The repository structure is designed to separate project documentation, visual evidence, administration scripts, and troubleshooting material as the lab grows.

---

# Skills Demonstrated

### Windows Administration

* Windows Server 2022
* Windows 11
* Active Directory Domain Services
* DNS
* Group Policy
* User administration
* Security group management
* Organizational Units
* Domain authentication

### Networking

* IPv4 configuration
* DNS troubleshooting
* TCP/IP fundamentals
* Host-Only networking
* NAT
* Client/server connectivity
* Network troubleshooting

### IT Support

* Incident investigation
* Technical troubleshooting
* Authentication troubleshooting
* Endpoint troubleshooting
* Structured problem solving
* Documentation
* Verification and validation

### Tools

* Oracle VirtualBox
* PowerShell
* Command Prompt
* Active Directory Users and Computers
* Group Policy Management
* Windows administrative utilities

---

# Portfolio Relevance

This project demonstrates practical exposure to technologies commonly encountered in entry-level IT infrastructure environments.

It is particularly relevant to:

* IT Support Technician
* Service Desk Analyst
* Help Desk Analyst
* Desktop Support Technician
* Technical Support Specialist
* MSP Support Technician
* Junior Systems Administrator
* Junior Network Support Technician

The focus is on **hands-on implementation and troubleshooting**, rather than simply listing technologies on a resume.

---

# Key Takeaways

This lab strengthened practical understanding of how a Windows enterprise environment operates from an IT support perspective.

The project demonstrates the ability to:

* Deploy and configure Windows Server
* Configure a Windows domain controller
* Implement Active Directory
* Manage users and security groups
* Organize users with Organizational Units
* Configure Group Policy
* Configure Windows client networking
* Join Windows clients to a domain
* Verify domain authentication
* Troubleshoot DNS and connectivity
* Use Windows administrative tools
* Document technical implementation and evidence

The overall workflow reinforces an important IT support principle:

> **Configure → Test → Troubleshoot → Verify → Document**

---

# Project Status

**Current status:** Active development

The core Active Directory environment, organizational structure, test accounts, security groups, Group Policy configuration, Windows 11 domain client, and domain authentication workflow have been implemented.

The lab will continue to expand with additional Windows administration, permissions, PowerShell, and troubleshooting scenarios.

---

## About This Project

This is an **independently built hands-on IT infrastructure lab** created to develop practical Windows administration and IT support skills.

**Focus Areas:**

`Windows Server` · `Active Directory` · `DNS` · `Group Policy` · `Windows 11` · `IT Support` · `Troubleshooting` · `PowerShell` · `Networking`

**Author:** Rikit Thapa
