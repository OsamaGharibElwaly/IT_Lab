For **Windows Administration / MCSA (Microsoft Certified Solutions Associate)**, these are the **rules of thumb (mental shortcuts)** for the most important terminologies. Think of them as the concepts an IT Support / System Administrator should instantly recognize.

---

# 1. Windows Server Core Concepts

| Term                | Rule of Thumb                                                             |
| ------------------- | ------------------------------------------------------------------------- |
| **Windows Server**  | The operating system designed to provide services to many users/computers |
| **Client OS**       | Windows 10/11 → used by end users                                         |
| **Server OS**       | Windows Server → manages users, resources, applications                   |
| **Role**            | A major function a server provides                                        |
| **Feature**         | Additional capability that supports roles                                 |
| **Role vs Feature** | Role = "what the server does"; Feature = "extra ability"                  |

Example:

* Install **AD DS Role** → server becomes Domain Controller
* Install **Backup Feature** → adds backup capability

---

# 2. Active Directory (AD) Terminology

## Active Directory Domain Services (AD DS)

**Rule:**

> AD DS = Database + Authentication + Authorization

It stores:

* Users
* Computers
* Groups
* Policies
* Resources

---

## Domain

**Rule:**

> Domain = Security boundary + centralized management area

Example:

```
company.local
     |
 ----------------
 |      |        |
PC1    PC2     Users
```

A domain allows:

* Single login
* Central policies
* User management

---

## Domain Controller (DC)

**Rule:**

> DC = Server running Active Directory

Responsibilities:

* Authenticates users
* Stores AD database
* Applies policies

Example:

User logs in:

```
PC
 |
 |
Domain Controller
 |
 |
Check username/password
 |
Allow/Deny
```

---

## Forest

**Rule:**

> Forest = Collection of Domains

Largest AD container.

Example:

```
Forest
 |
 |---- Domain A
 |
 |---- Domain B
 |
 |---- Domain C
```

---

## Tree

**Rule:**

> Tree = Group of related domains sharing namespace

Example:

```
Tree:

company.com

 |
 |
sales.company.com
hr.company.com
```

---

## Organizational Unit (OU)

**Rule:**

> OU = Folder for organizing and applying policies

Example:

```
Company.local

OU=HR
   |
   Users

OU=IT
   |
   Computers
```

Used for:

* Group Policy
* Delegation
* Organization

---

# 3. User and Security Terminology

## User Account

**Rule:**

> Identity that can authenticate

Example:

```
Ahmed
Password
Permissions
```

---

## Group

**Rule:**

> Manage permissions once, apply to many users

Instead of:

```
Ahmed → Permission
Ali → Permission
Sara → Permission
```

Use:

```
IT_Group
 |
 Ahmed
 Ali
 Sara

Permission → IT_Group
```

---

## Security Group

Used for:

* Permissions

Example:

```
Finance_Group
    |
    Users

Permission:
Read Finance Folder
```

---

## Distribution Group

Used for:

* Email lists

Example:

```
AllEmployees@
```

No security permissions.

---

# 4. Group Policy (GPO)

**Rule:**

> GPO = Central configuration rules

Controls:

* Password policies
* Desktop settings
* Software installation
* Security settings

Hierarchy:

```
Domain
 |
 OU
 |
 User / Computer
```

Example:

Disable USB:

```
GPO
 |
OU=Employees
 |
Disable USB Storage
```

---

# 5. DNS Terminology

**Rule:**

> DNS = Name → IP translation

Example:

```
google.com
      |
      |
142.250.x.x
```

Windows AD depends heavily on DNS.

---

## DNS Record Types

| Record | Rule             |
| ------ | ---------------- |
| A      | Name → IPv4      |
| AAAA   | Name → IPv6      |
| CNAME  | Alias            |
| MX     | Mail server      |
| PTR    | IP → Name        |
| SRV    | Service location |

Important for AD:

```
_SRV records

Find Domain Controllers
```

---

# 6. DHCP Terminology

**Rule:**

> DHCP gives network settings automatically

Provides:

* IP address
* Subnet mask
* Gateway
* DNS

Process:

## DORA

Remember:

```
D
Discover

O
Offer

R
Request

A
Acknowledge
```

---

# 7. File System Terminology

## NTFS

**Rule:**

> NTFS = Windows security filesystem

Supports:

* Permissions
* Encryption
* Compression
* Large files

---

## FAT32

**Rule:**

> FAT32 = Simple compatibility filesystem

Limitations:

* No NTFS permissions
* 4GB maximum file size

---

## Share Permission

Network access:

```
\\Server\Folder
```

Example:

```
Share:
Everyone Read
```

---

## NTFS Permission

Local + Network security:

Examples:

* Full Control
* Modify
* Read
* Write

Rule:

```
Effective Permission =
Most restrictive between Share + NTFS
```

Example:

Share:

```
Everyone = Full
```

NTFS:

```
Ahmed = Read
```

Result:

```
Ahmed = Read
```

---

# 8. Windows Services

**Rule:**

> Service = Background program

Examples:

| Service        | Function        |
| -------------- | --------------- |
| DNS Server     | Name resolution |
| DHCP Server    | IP assignment   |
| Print Spooler  | Printing        |
| Windows Update | Updates         |

---

# 9. Registry

**Rule:**

> Registry = Windows configuration database

Stores:

* OS settings
* Application settings
* Hardware configuration

Main keys:

```
HKLM
Computer settings

HKCU
User settings
```

---

# 10. Virtualization Terminology

## Hyper-V

**Rule:**

> Microsoft virtualization platform

Creates:

```
Physical Server

 |
Hyper-V

 |
 ----------------
VM1     VM2     VM3
```

---

## Virtual Machine (VM)

**Rule:**

> Software computer running inside physical computer

Contains:

* Virtual CPU
* Virtual RAM
* Virtual Disk
* Virtual NIC

---

# 11. Remote Administration

## RDP

**Rule:**

> Remote Desktop = GUI remote access

Port:

```
TCP 3389
```

---

## PowerShell

**Rule:**

> Command-line automation for Windows administration

Examples:

Users:

```powershell
Get-ADUser
```

Services:

```powershell
Get-Service
```

Network:

```powershell
Get-NetIPConfiguration
```

---

# 12. Permissions Terminology

## Authentication

**Rule:**

> Authentication = Who are you?

Example:

```
Username + Password
```

---

## Authorization

**Rule:**

> Authorization = What can you do?

Example:

```
Ahmed:
Can read folder
Cannot delete
```

---

# 13. MCSA Administrator Mental Model

When troubleshooting Windows Server think in this order:

```
1. Identity
   |
   AD Users / Groups

2. Network
   |
   IP / DNS / DHCP

3. Permissions
   |
   NTFS / Share

4. Policies
   |
   GPO

5. Services
   |
   Server Roles

6. Logs
   |
   Event Viewer
```

---

# Golden Rule for Windows Admin

```
Active Directory
        +
DNS
        +
Group Policy
        +
Permissions
        +
PowerShell
        =
Windows Administrator
```

If you master these five areas, you cover ~80% of daily Windows Server administration tasks.
