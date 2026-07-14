\# BarnesLab - Active Directory Home Lab



\## Overview

BarnesLab is a self-built virtual enterprise lab environment created using VMware Workstation and Windows Server 2022. The purpose of this project was to strengthen hands-on infrastructure, networking, Active Directory, file sharing, and application server support skills.



## Demo Video

[Watch the BarnesLab build demo](https://youtube.com)



\## Lab Environment

\- \*\*Domain Controller:\*\* BarnesLab

\- \*\*Domain:\*\* barneslab.local

\- \*\*File Server:\*\* FS1

\- \*\*Application Server:\*\* APP1

\- \*\*Platform:\*\* VMware Workstation

\- \*\*Operating System:\*\* Windows Server 2022



\## Network Configuration

| Server | Role | IP Address |

|---|---|---|

| BarnesLab | Domain Controller / DNS | 192.168.190.10 |

| FS1 | File Server | 192.168.190.20 |

| APP1 | IIS Application Server | 192.168.190.30 |



\## What I Built

\- Deployed a Windows Server 2022 Domain Controller

\- Configured static IP addressing and DNS

\- Joined FS1 and APP1 to the barneslab.local domain

\- Created a file server with shared departmental folders

\- Installed IIS on APP1

\- Built a basic internal web application landing page

\- Validated communication between servers



\## Skills Demonstrated

\- Windows Server Administration

\- Active Directory Domain Services

\- DNS Configuration

\- VMware Workstation Virtualization

\- Static IP Configuration

\- Domain Joining

\- File Sharing

\- IIS Web Server Deployment

\- Infrastructure Troubleshooting

\- Documentation



\## Screenshots / Demo

Screenshots and screen recordings are included in the repository to show the lab build process and final validation.



\## Purpose

This lab was built as part of my continued growth into systems administration, application support, cloud, and infrastructure engineering roles.








# BarnesLab — Active Directory Home Lab

![Status](https://img.shields.io/badge/Status-Active-brightgreen)
![Platform](https://img.shields.io/badge/Platform-VMware%20Workstation-blue)
![OS](https://img.shields.io/badge/OS-Windows%20Server%202022-0078D4?logo=windows)

## Overview

BarnesLab is a self-built virtual enterprise lab environment designed to simulate a real-world corporate Active Directory infrastructure. Built using VMware Workstation Pro and Windows Server 2022, this lab demonstrates hands-on proficiency in Windows Server administration, Active Directory Domain Services, DNS, Group Policy, file services, and domain-joined endpoint management.

This project was built to strengthen practical skills aligned with Systems Administrator, Cloud Administrator, and IT Infrastructure Engineer roles — and to demonstrate working knowledge that goes beyond certifications alone.

📺 **Demo Video:** [Watch the BarnesLab Build Walkthrough on YouTube](#) *(link coming soon)*

---

## Lab Architecture

```
+---------------------------+        +---------------------------+
|      BARNESLAB-DC         |        |          WKSTN1           |
|  Windows Server 2022      |        |     Windows 10 Enterprise |
|  Domain Controller / DNS  |<------>|    Domain-Joined Client   |
|  IP: 192.168.10.10        |        |    IP: 192.168.10.20      |
+---------------------------+        +---------------------------+
           |
    barneslab.local
    (AD DS / DNS)
           |
  VMware NAT Network
  Subnet: 192.168.10.0/24
  Gateway: 192.168.10.2
```

---

## Environment Specifications

| Component | Details |
|---|---|
| Host Machine | Lenovo ThinkCentre M73 Tiny |
| Host CPU | Intel Core i5-4570T (up to 3.6GHz) |
| Host RAM | 16GB |
| Host Storage | 128GB SSD |
| Host OS | Windows 10 Pro |
| Virtualization Platform | VMware Workstation Pro 17 |
| Domain Name | barneslab.local |
| Forest / Domain Functional Level | Windows Server 2016 |

---

## Virtual Machines

### BARNESLAB-DC — Domain Controller

| Setting | Value |
|---|---|
| Operating System | Windows Server 2022 Standard (Desktop Experience) |
| Role | Primary Domain Controller, DNS Server |
| IP Address | 192.168.10.10 (Static) |
| vCPUs | 2 |
| RAM | 2GB |
| Disk | 40GB (thin provisioned) |

**Roles & Features Installed:**
- Active Directory Domain Services (AD DS)
- DNS Server
- File and Storage Services
- IIS Web Server (APP1 simulation)

---

### WKSTN1 — Domain-Joined Workstation

| Setting | Value |
|---|---|
| Operating System | Windows 10 Enterprise |
| Role | Domain-Joined Client Workstation |
| IP Address | 192.168.10.20 (Static) |
| vCPUs | 2 |
| RAM | 2GB |
| Disk | 30GB (thin provisioned) |
| DNS | 192.168.10.10 (points to DC) |

---

## Active Directory Structure

```
barneslab.local
├── Builtin
├── Computers
│   └── WKSTN1
├── Domain Controllers
│   └── BARNESLAB-DC
└── BarnesLab OUs
    ├── IT
    │   ├── Users: jsmith (John Smith)
    │   └── Groups: IT-Admins
    ├── HR
    │   └── Users: mjohnson (Mary Johnson)
    ├── Finance
    │   └── Users: rbrown (Robert Brown)
    └── Workstations
        └── WKSTN1
```

---

## What I Built

### Active Directory Domain Services
- Deployed Windows Server 2022 and promoted it to a Primary Domain Controller
- Created a new forest and domain: `barneslab.local`
- Configured Organizational Units (OUs) for IT, HR, Finance, and Workstations
- Created domain user accounts within appropriate OUs
- Created Security Groups and assigned user memberships (e.g., IT-Admins)

### DNS Configuration
- Configured the DC as the authoritative DNS server for `barneslab.local`
- Created forward lookup zones for internal name resolution
- Validated DNS resolution between DC and domain-joined workstation
- Troubleshot and resolved DNS-related domain join failures

### Group Policy
- Created and linked Group Policy Objects (GPOs) to specific OUs
- Applied desktop configuration policies to the HR OU
- Forced Group Policy refresh using `gpupdate /force`
- Validated GPO application on WKSTN1 using `gpresult /r`

### Domain Join & Authentication
- Joined WKSTN1 to `barneslab.local` domain
- Validated domain authentication using domain user credentials
- Tested user login from WKSTN1 using accounts created in AD
- Verified domain membership with `whoami` and `net user /domain`

### File Services
- Created shared departmental folders on the DC
- Configured NTFS permissions and share permissions per department
- Validated share access from WKSTN1 using UNC paths (`\\BARNESLAB-DC\IT`)

### IIS Web Server
- Installed IIS on the DC (simulating APP1 application server role)
- Deployed a basic internal web landing page
- Validated IIS service and page accessibility from WKSTN1 browser

---

## Key Commands Used

```powershell
# Verify domain membership
whoami
net user /domain

# Test DNS and connectivity
ping barneslab-dc
nslookup barneslab.local
ipconfig /all

# Force Group Policy update
gpupdate /force

# View applied Group Policies
gpresult /r

# Check AD replication (when scaling to multi-DC)
repadmin /showrepl

# List domain computers
Get-ADComputer -Filter * | Select Name

# List domain users
Get-ADUser -Filter * | Select Name, SamAccountName
```

---

## Troubleshooting Scenarios Practiced

| Issue | Root Cause | Resolution |
|---|---|---|
| Domain join failed | WKSTN1 DNS pointed to wrong server | Changed DNS to 192.168.10.10 (DC IP) |
| User login denied on WKSTN1 | Account not in correct OU | Moved user object to correct OU in ADUC |
| GPO not applying | GPO linked to wrong OU | Re-linked GPO, ran gpupdate /force |
| Ping to DC failing | VMware network set to Host-only instead of NAT | Changed VM network adapter to NAT |
| DNS resolution failing | Static IP not set on DC | Configured static IP and restarted DNS service |

---

## Skills Demonstrated

| Skill Category | Specific Skills |
|---|---|
| Windows Server Administration | Installation, configuration, role management, Server Manager |
| Active Directory | AD DS deployment, OUs, users, groups, domain join, FSMO roles |
| DNS | Forward lookup zones, A records, name resolution, troubleshooting |
| Group Policy | GPO creation, linking, filtering, enforcement, gpresult |
| Networking | Static IP configuration, TCP/IP, DNS/DHCP concepts, VMware NAT |
| Virtualization | VMware Workstation Pro, VM creation, snapshots, thin provisioning |
| PowerShell | AD cmdlets, user/computer queries, policy management |
| Troubleshooting | Systematic root cause analysis, event log review, connectivity testing |
| Documentation | Network diagrams, lab runbooks, structured README |

---

## Screenshots

> Screenshots of the completed lab environment are included in the `/screenshots` folder of this repository.

- `ad-structure.png` — Active Directory Users and Computers showing OU hierarchy
- `domain-join-success.png` — WKSTN1 welcome to domain confirmation
- `gpo-applied.png` — gpresult output showing applied policies
- `dns-manager.png` — DNS forward lookup zone for barneslab.local
- `whoami-output.png` — Terminal showing BARNESLAB\jsmith authenticated

---

## Next Phase

This lab is Phase 1 of a multi-phase project. Phase 2 adds a Splunk SIEM layer for security monitoring:

➡️ [BarnesLab SOC — Splunk SIEM + Attack Detection Lab](#) *(see repository)*

**Planned additions:**
- Sysmon deployment on DC and WKSTN1 for enhanced endpoint telemetry
- Splunk Universal Forwarder to ship Windows Event Logs and Sysmon data
- Splunk Free instance on Ubuntu Server for log aggregation and detection
- Simulated attack scenarios (brute force, PowerShell abuse, account creation)
- Detection rules mapped to MITRE ATT&CK framework

---

## Resources Used

- [Microsoft Evaluation Center — Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)
- [Microsoft Evaluation Center — Windows 10 Enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise)
- [VMware Workstation Pro (Free for Personal Use)](https://www.vmware.com/products/workstation-pro.html)
- [Microsoft AD DS Documentation](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview)

---

## About This Project

Built by **Lloyd Barnes** — Systems & Cloud Administration | Network & Infrastructure Engineering | CompTIA CySA+

- 🔗 LinkedIn: [linkedin.com/in/lloyd-barnes-ii](https://www.linkedin.com/in/lloyd-barnes-ii)
- 🏅 Credly: [credly.com/users/lloyd-barnes.6c44ecd1](https://www.credly.com/users/lloyd-barnes.6c44ecd1)
- 💻 GitHub: [github.com/lbarnes86](https://www.github.com/lbarnes86)

