# IT Interview Preparation — MCSA & CCNA Basics

> **Interview scope:** Windows Server / Active Directory + Cisco Switching
> **Main goal:** Understand the basics well enough to explain them clearly and troubleshoot common scenarios.

---

# 1. Interview Scope

According to the interview topics:

## MCSA / Windows Server

Focus on:

1. Domain
2. Active Directory
3. Domain Controller
4. DNS
5. DHCP
6. Users
7. Groups
8. Basic permissions
9. Domain Join
10. Basic troubleshooting

## CCNA / Switching

Focus on:

1. Switching fundamentals
2. VLANs
3. Access ports
4. Trunk ports
5. STP
6. EtherChannel
7. Basic troubleshooting

---

# 2. The Big Picture

Before memorizing individual definitions, understand how everything connects.

Imagine a company with:

```text
                    INTERNET
                       |
                    Router
                       |
                +--------------+
                |   Switch     |
                +--------------+
                  /     |      \
                 /      |       \
              PC-1     PC-2    Server
                               |
                    +-------------------+
                    | Windows Server    |
                    |                   |
                    | Active Directory  |
                    | DNS               |
                    | DHCP              |
                    +-------------------+
```

A typical Windows network can work like this:

```text
DHCP
  ↓
Client receives IP configuration
  ↓
Client knows DNS server
  ↓
DNS resolves company domain
  ↓
Client finds Domain Controller
  ↓
Active Directory authenticates user
  ↓
User receives permissions based on groups
  ↓
Switch/VLAN infrastructure provides connectivity
```

This relationship is extremely important for interviews.

---

# PART I — WINDOWS SERVER / ACTIVE DIRECTORY

# 3. What is Active Directory?

**Active Directory Domain Services (AD DS)** is Microsoft's directory service for managing identities and network resources centrally.

It stores information about objects such as:

* Users
* Computers
* Groups
* Servers
* Organizational Units
* Other network resources

It provides centralized identity and access management.

Microsoft describes AD DS as a hierarchical directory that stores information about network objects and supports authentication and access control.

### Simple interview answer

> Active Directory is a centralized directory service used in Windows environments to manage users, computers, groups, authentication, and access to network resources.

---

# 4. What Problem Does Active Directory Solve?

Without Active Directory:

```text
Computer 1
  User1
  User2

Computer 2
  User1
  User2

Computer 3
  User1
  User2
```

Each computer could have its own local accounts.

This becomes difficult to manage.

With Active Directory:

```text
                 Active Directory
                       |
        +--------------+--------------+
        |              |              |
      User          Computer        Group
        |
   Authentication
        |
   Access Resources
```

The organization can centrally manage:

* Accounts
* Passwords
* Computers
* Groups
* Policies
* Permissions

---

# 5. Domain

A **domain** is a logical administrative boundary in Active Directory.

Example:

```text
company.local
```

or:

```text
company.com
```

Users and computers can belong to this domain.

Example:

```text
Domain:
company.local

Users:
Ahmed
Mohamed
Sara

Computers:
PC-01
PC-02
PC-03
```

### Interview answer

> An Active Directory domain is a logical administrative and security boundary that contains users, computers, groups, and other directory objects.

---

# 6. Domain Controller

A **Domain Controller (DC)** is a Windows Server that hosts Active Directory Domain Services.

It handles important operations such as:

* Authentication
* Authorization information
* Directory queries
* User management
* Computer authentication
* Replication with other DCs

Conceptually:

```text
Client
   |
   | "I want to log in"
   ↓
Domain Controller
   |
   ↓
Active Directory
   |
   ↓
Verify credentials
   |
   ↓
Access granted / denied
```

### Important

A Domain Controller is **not the same thing as Active Directory**.

* **Active Directory** = directory service/database/system
* **Domain Controller** = server running AD DS and providing domain services

---

# 7. Domain vs Workgroup

## Workgroup

Each computer manages itself.

```text
PC1 → Local accounts
PC2 → Local accounts
PC3 → Local accounts
```

## Domain

Centralized management.

```text
             Domain Controller
                    |
       +------------+------------+
       |            |            |
      PC1          PC2          PC3
```

### Domain advantages

* Centralized authentication
* Centralized user management
* Group-based permissions
* Group Policy
* Centralized administration
* Easier management of many computers

---

# 8. Domain Join

When a Windows computer joins a domain, it becomes part of the organization's Active Directory environment.

Example:

```text
PC-01
   ↓
Join
   ↓
company.local
```

The computer then has a computer account in Active Directory.

A domain-joined user can typically log in using:

```text
COMPANY\Ahmed
```

or:

```text
ahmed@company.local
```

---

# 9. Active Directory Objects

Common objects:

```text
User
Computer
Group
OU
Printer
Shared Resource
```

Example:

```text
company.local

├── Users
│   ├── Ahmed
│   ├── Sara
│   └── Mohamed
│
├── Computers
│   ├── PC01
│   └── PC02
│
└── Groups
    ├── IT
    ├── HR
    └── Finance
```

---

# 10. Organizational Unit — OU

An **Organizational Unit (OU)** is a container used to organize objects inside a domain.

Example:

```text
company.local
│
├── IT
│   ├── Ahmed
│   └── PC01
│
├── HR
│   ├── Sara
│   └── PC02
│
└── Finance
    ├── Mohamed
    └── PC03
```

OUs are useful for:

* Organization
* Delegation
* Group Policy application

Microsoft specifically identifies OUs as containers used for administrative organization, Group Policy, and delegation.

---

# 11. Forest

A **forest** is the highest-level logical structure in Active Directory.

Simplified:

```text
Forest
  |
  +--- Domain A
  |
  +--- Domain B
  |
  +--- Domain C
```

A forest can contain multiple domains.

Microsoft describes a forest as a collection of one or more domains sharing common schema, configuration, and global catalog infrastructure.

### Interview priority

Know this:

```text
Forest
   ↓
Domain
   ↓
OU
   ↓
Objects
```

---

# 12. User Accounts

A user account represents a person or identity in Active Directory.

Example:

```text
Username: ahmed
Password: ********
Department: IT
```

A user can belong to multiple groups.

```text
Ahmed
  |
  +---- IT
  |
  +---- VPN-Users
  |
  +---- Developers
```

---

# 13. Groups

Groups allow administrators to manage permissions collectively.

Instead of:

```text
Give access to Ahmed
Give access to Sara
Give access to Mohamed
Give access to Ali
```

Create:

```text
IT-Department
```

Then:

```text
Ahmed ──┐
Sara ───┼──> IT-Department
Mohamed ┘
```

Give the group access.

All members inherit the group's permissions.

---

# 14. Security Groups vs Distribution Groups

## Security Group

Used primarily for:

* Permissions
* Authorization
* Access control

Example:

```text
IT-Users
```

Give:

```text
IT-Users → Access to IT Share
```

## Distribution Group

Primarily used for email distribution.

Example:

```text
All-Employees
```

### Interview answer

> Security groups are used to assign permissions and control access, while distribution groups are mainly used for communication such as email distribution.

---

# 15. DNS

DNS = **Domain Name System**

DNS translates names into IP addresses.

Example:

```text
server01.company.local
        ↓
    DNS lookup
        ↓
192.168.1.10
```

Instead of remembering:

```text
192.168.1.10
```

you can use:

```text
server01.company.local
```

---

# 16. Why DNS Is Extremely Important in Active Directory

This is a very common interview topic.

Active Directory depends heavily on DNS for service discovery and locating domain controllers.

Microsoft specifically documents DNS as a dependency for AD DS service discovery, domain-controller location, and replication-related operations.

Simplified:

```text
Client
  |
  | DNS query
  ↓
DNS Server
  |
  ↓
Find Domain Controller
  |
  ↓
Domain Controller
  |
  ↓
Authentication
```

### Very important interview sentence

> Active Directory relies on DNS so clients can locate domain controllers and discover domain services.

---

# 17. Common DNS Records

## A Record

Hostname → IPv4 address

```text
server01 → 192.168.1.10
```

## AAAA

Hostname → IPv6 address

## CNAME

Alias → another hostname

```text
www → server01
```

## MX

Mail server record.

## PTR

IP address → hostname.

Used for reverse lookup.

## SRV

Service location.

Very important in Active Directory.

Example concept:

```text
Where is the domain controller?
```

DNS SRV records help clients discover required services.

---

# 18. Forward vs Reverse DNS

## Forward lookup

```text
Name → IP
```

Example:

```text
server01.company.local
       ↓
192.168.1.10
```

## Reverse lookup

```text
IP → Name
```

Example:

```text
192.168.1.10
       ↓
server01.company.local
```

---

# 19. DHCP

DHCP = **Dynamic Host Configuration Protocol**

DHCP automatically provides network configuration to clients.

It can provide:

* IP address
* Subnet mask
* Default gateway
* DNS server
* Lease information

Example:

```text
Laptop
   ↓
DHCP Request
   ↓
DHCP Server
   ↓
192.168.1.25
255.255.255.0
Gateway: 192.168.1.1
DNS: 192.168.1.10
```

---

# 20. DHCP DORA Process

This is a must-know interview question.

DORA:

```text
D = Discover
O = Offer
R = Request
A = Acknowledgment
```

### Step 1 — Discover

Client broadcasts:

> Is there a DHCP server?

### Step 2 — Offer

DHCP server responds:

> I can offer you 192.168.1.20.

### Step 3 — Request

Client says:

> I want that address.

### Step 4 — ACK

Server confirms:

> 192.168.1.20 is yours for this lease.

---

# 21. DHCP vs DNS

Very common comparison.

| DHCP                               | DNS                         |
| ---------------------------------- | --------------------------- |
| Assigns network configuration      | Resolves names              |
| Gives IP addresses                 | Maps names to IPs           |
| Uses leases                        | Uses records                |
| Helps clients configure themselves | Helps clients find services |

Simple:

```text
DHCP:
"What IP should I use?"

DNS:
"Where is server01?"
```

---

# 22. DHCP Lease

DHCP addresses are normally leased for a period of time.

Example:

```text
Client receives:
192.168.1.50

Lease:
8 hours
```

The client eventually renews the lease.

---

# 23. Default Gateway

The default gateway is normally the router/interface a host uses to reach networks outside its local subnet.

Example:

```text
PC:
192.168.1.20

Gateway:
192.168.1.1
```

If the PC wants to communicate with:

```text
192.168.1.100
```

same subnet → direct communication.

If it wants:

```text
8.8.8.8
```

different network → send toward gateway.

---

# 24. Authentication vs Authorization

Very important.

## Authentication

> Who are you?

Example:

```text
Username + Password
        ↓
Identity verified
```

## Authorization

> What are you allowed to access?

Example:

```text
Ahmed authenticated
        ↓
Member of IT group
        ↓
Allowed to access IT share
```

Remember:

```text
Authentication = Who are you?
Authorization = What can you access?
```

---

# 25. Permissions and Groups

Suppose:

```text
D:\Company\Finance
```

You want Finance employees to access it.

Instead of giving permissions individually:

```text
Ahmed → access
Sara → access
Mohamed → access
```

Create:

```text
Finance-Users
```

Then:

```text
Finance-Users
      ↓
Folder Permission
```

This is easier to manage.

---

# 26. Group Policy — Basic Knowledge

Although not explicitly mentioned by the interviewer, know the basic idea.

**Group Policy** allows administrators to centrally configure policies for users and computers.

Examples:

* Password policy
* Lock screen settings
* Security settings
* Software configuration
* Desktop restrictions

Microsoft's AD DS training includes Group Policy as a core administration topic.

---

# 27. Active Directory Basic Architecture

Remember this model:

```text
                    FOREST
                       |
              +--------+--------+
              |                 |
           DOMAIN A          DOMAIN B
              |
       +------+------+
       |             |
      OU            OU
       |             |
    Users         Computers
       |
     Groups
```

---

# PART II — CCNA SWITCHING

# 28. What Is a Network Switch?

A switch connects devices inside a LAN.

Example:

```text
PC1 ───┐
PC2 ───┤
PC3 ───┤ SWITCH
PC4 ───┘
```

A switch primarily forwards Ethernet frames based on MAC addresses.

---

# 29. MAC Address

A MAC address identifies a network interface at Layer 2.

Example:

```text
00:1A:2B:3C:4D:5E
```

Switches learn which MAC address is associated with which port.

Example MAC table:

```text
MAC Address          Port
--------------------------------
AA:AA:AA:AA:AA:AA    Fa0/1
BB:BB:BB:BB:BB:BB    Fa0/2
CC:CC:CC:CC:CC:CC    Fa0/3
```

---

# 30. How Does a Switch Learn MAC Addresses?

Suppose PC1 sends a frame.

The switch sees:

```text
Source MAC:
AA:AA:AA
```

arriving on:

```text
Fa0/1
```

The switch learns:

```text
AA:AA:AA → Fa0/1
```

This is called MAC address learning.

---

# 31. VLAN

VLAN = **Virtual Local Area Network**

A VLAN logically separates devices into different Layer 2 broadcast domains.

Example:

```text
                 SWITCH
                    |
        +-----------+-----------+
        |                       |
      VLAN 10                 VLAN 20
        |                       |
       IT                      HR
```

Even if the computers are connected to the same physical switch, VLANs logically separate them.

---

# 32. Why Use VLANs?

Benefits include:

* Segmentation
* Smaller broadcast domains
* Better organization
* Security isolation
* Easier network management

Example:

```text
VLAN 10 = IT
VLAN 20 = HR
VLAN 30 = Finance
```

---

# 33. VLAN Example

Suppose:

```text
PC1 → VLAN 10
PC2 → VLAN 10
PC3 → VLAN 20
PC4 → VLAN 20
```

PC1 and PC2:

```text
Same VLAN
```

PC3 and PC4:

```text
Same VLAN
```

PC1 and PC3:

```text
Different VLAN
```

Communication between different VLANs normally requires Layer 3 routing.

---

# 34. Access Port

An **access port** normally carries traffic for one VLAN.

Example:

```text
PC
 |
 |
Switch Fa0/1
 |
VLAN 10
```

Typical use:

* PCs
* Printers
* End-user devices

### Interview answer

> An access port is a switch port assigned to a single VLAN and is typically used to connect end devices.

---

# 35. Trunk Port

A **trunk** carries traffic for multiple VLANs over one physical link.

Example:

```text
Switch A
   |
   | Trunk
   |
Switch B
```

The trunk can carry:

```text
VLAN 10
VLAN 20
VLAN 30
```

Conceptually:

```text
          Trunk
SW1 ================= SW2
      VLAN 10
      VLAN 20
      VLAN 30
```

---

# 36. Access vs Trunk

| Access                          | Trunk                 |
| ------------------------------- | --------------------- |
| Usually one VLAN                | Multiple VLANs        |
| End devices                     | Switch-to-switch      |
| Frames associated with one VLAN | VLAN-tagged traffic   |
| PC/printer                      | Switch/AP/server/etc. |

### Easy memory

```text
ACCESS = one VLAN

TRUNK = many VLANs
```

---

# 37. VLAN Tagging

802.1Q is commonly used for VLAN tagging on trunk links.

Conceptually:

```text
Ethernet Frame
      +
VLAN Tag
      ↓
Switch knows VLAN
```

Example:

```text
Frame → VLAN 10
Frame → VLAN 20
Frame → VLAN 30
```

The tag identifies the VLAN when traffic travels across a trunk.

---

# 38. Native VLAN

On an 802.1Q trunk, the native VLAN is the VLAN whose traffic is transmitted untagged by default.

Interview-level knowledge:

> Native VLAN is the VLAN associated with untagged traffic on an 802.1Q trunk.

Don't overcomplicate this unless the interviewer asks deeper questions.

---

# 39. STP

STP = **Spanning Tree Protocol**

Its primary purpose is to prevent Layer 2 switching loops.

Imagine:

```text
SW1 -------- SW2
 |             |
 |             |
 +-------------+
```

There are multiple paths.

A Layer 2 loop can cause serious problems.

---

# 40. Why Are Layer 2 Loops Dangerous?

A switch can continuously forward/broadcast frames around a loop.

Potential results:

* Broadcast storms
* MAC table instability
* Duplicate frames
* Network congestion
* Network outage

STP prevents this by logically blocking redundant paths.

---

# 41. STP Basic Idea

Topology:

```text
       SW1
      /   \
     /     \
   SW2-----SW3
```

STP can place one redundant link into a blocking/discarding state.

Conceptually:

```text
       SW1
      /   \
     /     \
   SW2     SW3
     \     /
      \ X /
      blocked
```

The physical redundancy remains, but STP prevents a loop.

---

# 42. Root Bridge

STP elects a **Root Bridge**.

The root bridge becomes the reference point for the spanning-tree topology.

Basic election concept:

> The switch with the lowest Bridge ID becomes the root bridge.

Bridge ID involves:

```text
Priority
+
MAC address
```

If priorities are equal, the lower MAC address wins.

---

# 43. STP Port Roles — Basic

Traditional STP terminology includes:

### Root Port

The best path from a non-root switch toward the root bridge.

### Designated Port

The forwarding port selected for a network segment.

### Blocking / Non-forwarding

A redundant path that is not forwarding user traffic.

For a basic interview, understand the purpose rather than memorizing every STP state/timer.

---

# 44. STP Port States

Traditional 802.1D STP states:

```text
Blocking
   ↓
Listening
   ↓
Learning
   ↓
Forwarding
```

There is also:

```text
Disabled
```

RSTP later simplified the operational behavior.

---

# 45. RSTP

RSTP = Rapid Spanning Tree Protocol.

It provides faster convergence than traditional STP.

Common terminology:

```text
STP  → 802.1D
RSTP → 802.1w
```

If the interviewer only asks STP basics, don't spend too much time here.

---

# 46. EtherChannel

EtherChannel combines multiple physical links into one logical link.

Example:

Without EtherChannel:

```text
SW1 ===== SW2
      Link 1

SW1 ===== SW2
      Link 2
```

With EtherChannel:

```text
          EtherChannel
SW1 ================= SW2
       Link 1
       Link 2
       Link 3
```

The multiple physical links are treated logically as one bundle.

---

# 47. Why Use EtherChannel?

Advantages:

* Increased aggregate bandwidth
* Redundancy
* Better utilization of multiple physical links
* STP sees the bundle as a logical link

Example:

```text
4 × 1 Gbps links

Potential aggregate:
4 Gbps
```

The exact usable throughput depends on traffic distribution and implementation; it does not mean one individual flow necessarily gets 4 Gbps.

---

# 48. LACP

LACP = **Link Aggregation Control Protocol**

It dynamically negotiates link aggregation.

Common modes:

```text
active
passive
```

Basic concept:

```text
Active + Active
Active + Passive
```

can form an LACP EtherChannel.

---

# 49. PAgP

PAgP = Port Aggregation Protocol.

It is Cisco proprietary.

Common modes:

```text
desirable
auto
```

For modern networking knowledge, LACP is especially important because it is standards-based.

---

# 50. EtherChannel Requirements

For links to form a proper EtherChannel, important parameters generally need to match, such as:

* Speed
* Duplex
* VLAN/trunk configuration
* Trunk/access mode
* Allowed VLAN configuration
* Other relevant interface parameters

If one link has inconsistent configuration, the bundle may fail or behave unexpectedly.

---

# 51. STP + EtherChannel

Very important conceptual relationship.

Suppose:

```text
SW1
 |||
 ||| 3 physical links
 |||
SW2
```

Without EtherChannel, STP may treat the links as separate paths and block redundant links.

With EtherChannel:

```text
SW1
 ||
 ||  ← one logical EtherChannel
 ||
SW2
```

STP sees the EtherChannel as a logical connection.

---

# 52. VLAN + Trunk + STP + EtherChannel Together

This is the big picture.

```text
             SWITCH 1
          +-------------+
          |             |
          | VLAN 10     |
          | VLAN 20     |
          +-------------+
                 ||
                 ||
            EtherChannel
              Trunk
                 ||
                 ||
          +-------------+
          |             |
          | SWITCH 2    |
          |             |
          +-------------+
             |       |
          VLAN 10   VLAN 20
```

STP protects the Layer 2 topology from loops.

VLANs provide segmentation.

Trunks carry multiple VLANs.

EtherChannel combines multiple physical links.

---

# PART III — VERY IMPORTANT COMPARISONS

# 53. Domain vs DNS

### Domain

An Active Directory administrative/security structure.

### DNS

A name-resolution system.

```text
Domain:
company.local

DNS:
server01.company.local
        ↓
192.168.1.10
```

They are different technologies, but AD depends heavily on DNS.

---

# 54. DNS vs DHCP

```text
DHCP:
"I need network configuration."

DNS:
"I need the IP address of this hostname."
```

---

# 55. User vs Group

```text
User = individual identity

Group = collection of identities
```

Example:

```text
Ahmed
Sara
Mohamed
   ↓
IT-Group
```

---

# 56. Access Port vs Trunk Port

```text
Access:
one VLAN

Trunk:
multiple VLANs
```

---

# 57. VLAN vs Subnet

They are not exactly the same.

### VLAN

Layer 2 logical segmentation.

### IP subnet

Layer 3 logical network.

Example:

```text
VLAN 10
   ↓
192.168.10.0/24
```

They are commonly mapped together, but they are conceptually different.

---

# 58. Switch vs Router

## Switch

Primarily connects devices within LANs and forwards frames using MAC addresses.

## Router

Connects different IP networks and forwards packets using IP routing.

Example:

```text
PC1
 |
Switch
 |
Router
 |
Internet
```

---

# 59. MAC vs IP

### MAC

Layer 2 address.

Used for local Ethernet frame delivery.

### IP

Layer 3 address.

Used for logical network communication/routing.

Simple:

```text
MAC → local Layer 2 delivery

IP → Layer 3 addressing/routing
```

---

# PART IV — TROUBLESHOOTING

# 60. Scenario: User Cannot Log Into Domain

Possible causes:

```text
1. Network problem
2. DNS problem
3. Domain Controller unavailable
4. Incorrect username/password
5. Account disabled
6. Account locked
7. Time synchronization problem
8. Computer not properly joined to domain
```

Basic troubleshooting:

```text
Check network
   ↓
ipconfig
   ↓
Check DNS
   ↓
ping / nslookup
   ↓
Check domain controller connectivity
   ↓
Check user account
   ↓
Check time synchronization
```

---

# 61. Scenario: Computer Has No IP

Run:

```cmd
ipconfig
```

If you see an APIPA address such as:

```text
169.254.x.x
```

the computer may not have received a DHCP lease.

Check:

```text
DHCP server
DHCP scope
Network cable
Switch port
VLAN
DHCP relay
NIC
```

---

# 62. Scenario: User Can Ping IP but Not Hostname

Example:

```text
ping 192.168.1.10
```

works.

But:

```text
ping server01
```

fails.

Likely area:

```text
DNS
```

Check:

```cmd
ipconfig /all
nslookup server01
```

---

# 63. Scenario: User Cannot Access Internet

Check in order:

```text
1. Physical connection
2. IP address
3. Subnet mask
4. Default gateway
5. DNS
6. Routing
```

Example:

```cmd
ipconfig
ping 192.168.1.1
ping 8.8.8.8
nslookup google.com
```

Interpretation:

```text
Gateway fails
→ local network problem

8.8.8.8 works but google.com fails
→ DNS problem
```

---

# 64. Scenario: VLAN Users Cannot Communicate

Check:

```text
1. Are both ports in the correct VLAN?
2. Does the VLAN exist?
3. Is the trunk configured?
4. Is the VLAN allowed on the trunk?
5. Is inter-VLAN routing required?
6. Is the gateway correct?
```

---

# 65. Scenario: VLAN Works on One Switch but Not Another

Possible problem:

```text
Trunk
```

Check:

* Is the link actually a trunk?
* Is the VLAN allowed?
* Is the VLAN created on the required switches?
* Is native VLAN configuration consistent?
* Are there configuration mismatches?

---

# 66. Scenario: EtherChannel Does Not Form

Check:

```text
Speed
Duplex
Access/trunk mode
Allowed VLANs
Native VLAN
LACP/PAgP mode
Channel-group configuration
```

The member interfaces need compatible configurations.

---

# 67. Scenario: Network Has a Switching Loop

Symptoms may include:

* Broadcast storm
* High CPU
* MAC address flapping
* Network instability
* Duplicate traffic

Think:

```text
STP
```

---

# 68. Useful Cisco Commands

## Show interfaces

```text
show interfaces
```

## Show interface status

```text
show interfaces status
```

## Show VLANs

```text
show vlan brief
```

## Show trunk

```text
show interfaces trunk
```

## Show MAC table

```text
show mac address-table
```

## Show spanning tree

```text
show spanning-tree
```

## Show EtherChannel

```text
show etherchannel summary
```

## Show running configuration

```text
show running-config
```

## Show IP interfaces

```text
show ip interface brief
```

---

# 69. Useful Windows Commands

## IP configuration

```cmd
ipconfig
```

Detailed:

```cmd
ipconfig /all
```

Release DHCP:

```cmd
ipconfig /release
```

Renew DHCP:

```cmd
ipconfig /renew
```

Clear DNS cache:

```cmd
ipconfig /flushdns
```

---

# 70. Ping

```cmd
ping 192.168.1.1
```

Tests basic IP connectivity.

Important:

> Ping failure does not always prove that a host is completely unreachable because ICMP may be blocked.

---

# 71. nslookup

```cmd
nslookup server01.company.local
```

Used to test DNS resolution.

Example:

```text
server01.company.local
       ↓
192.168.1.10
```

---

# 72. tracert

Windows:

```cmd
tracert 8.8.8.8
```

Shows the path toward a destination.

---

# 73. ipconfig /all

Extremely useful.

It can show:

```text
IPv4 Address
Subnet Mask
Default Gateway
DNS Servers
DHCP Enabled
MAC/Physical Address
```

---

# PART V — INTERVIEW Q&A

# 74. Active Directory Questions

## Q1. What is Active Directory?

**Answer:**

> Active Directory Domain Services is Microsoft's directory service used to centrally manage users, computers, groups, authentication, and access to network resources.

---

## Q2. What is a domain?

**Answer:**

> A domain is a logical administrative and security boundary in Active Directory containing objects such as users, computers, and groups.

---

## Q3. What is a Domain Controller?

**Answer:**

> A Domain Controller is a Windows Server running AD DS. It provides services such as authentication, directory access, and domain management.

---

## Q4. What is the difference between Active Directory and a Domain Controller?

**Answer:**

> Active Directory is the directory service and its data/services, while a Domain Controller is the server that hosts AD DS and provides those domain services.

---

## Q5. What is an OU?

**Answer:**

> An Organizational Unit is a container inside an Active Directory domain used to organize objects and support administration, delegation, and Group Policy.

---

## Q6. What is a forest?

**Answer:**

> A forest is the top-level Active Directory logical structure that can contain one or more domains and shares common schema and configuration.

---

## Q7. What is the difference between a domain and a workgroup?

**Answer:**

> In a workgroup, computers are managed independently using local accounts. In a domain, users and computers can be centrally managed through Active Directory.

---

## Q8. What is domain joining?

**Answer:**

> Domain joining means configuring a computer to become a member of an Active Directory domain so that it can use centralized authentication and management.

---

# 75. DNS Questions

## Q9. What is DNS?

**Answer:**

> DNS translates domain and hostnames into IP addresses and helps clients locate network services.

---

## Q10. Why is DNS important for Active Directory?

**Answer:**

> Active Directory relies on DNS for service discovery and for clients to locate domain controllers and other domain services.

---

## Q11. What is an A record?

**Answer:**

> An A record maps a hostname to an IPv4 address.

Example:

```text
server01 → 192.168.1.10
```

---

## Q12. What is a PTR record?

**Answer:**

> A PTR record is used for reverse DNS resolution, mapping an IP address to a hostname.

---

## Q13. What is an SRV record?

**Answer:**

> An SRV record identifies the location of services, and Active Directory uses SRV records to help clients discover domain services such as domain controllers.

---

## Q14. What is forward DNS?

**Answer:**

> Forward lookup resolves a hostname to an IP address.

---

## Q15. What is reverse DNS?

**Answer:**

> Reverse lookup resolves an IP address to a hostname.

---

# 76. DHCP Questions

## Q16. What is DHCP?

**Answer:**

> DHCP automatically provides clients with network configuration such as IP address, subnet mask, default gateway, and DNS server.

---

## Q17. Explain DORA.

**Answer:**

> DORA stands for Discover, Offer, Request, and Acknowledgment. It describes the basic DHCP process through which a client obtains an IP configuration.

---

## Q18. What happens if DHCP fails?

**Answer:**

> The client may fail to obtain a normal IP configuration. On Windows, it may assign itself an APIPA address in the 169.254.0.0/16 range.

---

## Q19. What is a DHCP lease?

**Answer:**

> A DHCP lease is the period for which a client is allowed to use an assigned IP configuration.

---

# 77. Users and Groups Questions

## Q20. Why use groups?

**Answer:**

> Groups make permission management easier because administrators can assign permissions to a group instead of configuring every user individually.

---

## Q21. What is a security group?

**Answer:**

> A security group is used to manage permissions and access to resources.

---

## Q22. What is a distribution group?

**Answer:**

> A distribution group is primarily used for communication, such as email distribution, rather than assigning security permissions.

---

## Q23. Can one user belong to multiple groups?

**Answer:**

> Yes. A user can be a member of multiple groups and receive permissions associated with those groups.

---

# 78. Switching Questions

## Q24. What is a switch?

**Answer:**

> A switch is a Layer 2 networking device that connects devices within a LAN and forwards Ethernet frames based on MAC addresses.

---

## Q25. How does a switch learn MAC addresses?

**Answer:**

> The switch examines the source MAC address of incoming frames and records the MAC address along with the port where it was received.

---

## Q26. What is a VLAN?

**Answer:**

> A VLAN is a logical Layer 2 segmentation mechanism that creates separate broadcast domains on a switched network.

---

## Q27. Why use VLANs?

**Answer:**

> VLANs provide logical segmentation, reduce broadcast domains, improve organization, and can help isolate different groups of devices.

---

## Q28. What is an access port?

**Answer:**

> An access port normally belongs to one VLAN and is typically used to connect an end device such as a PC or printer.

---

## Q29. What is a trunk port?

**Answer:**

> A trunk port carries traffic for multiple VLANs, commonly between switches.

---

## Q30. Access vs trunk?

**Answer:**

> Access is normally one VLAN; trunk carries multiple VLANs.

---

# 79. STP Questions

## Q31. What is STP?

**Answer:**

> Spanning Tree Protocol prevents Layer 2 switching loops by creating a loop-free logical topology while maintaining redundant physical paths.

---

## Q32. Why are Layer 2 loops dangerous?

**Answer:**

> They can cause broadcast storms, MAC table instability, duplicate frames, and severe network congestion.

---

## Q33. What is the Root Bridge?

**Answer:**

> The Root Bridge is the switch selected by STP as the reference point for calculating the spanning-tree topology.

---

## Q34. How is the Root Bridge selected?

**Answer:**

> The switch with the lowest Bridge ID becomes the Root Bridge. Bridge ID is based on STP priority and MAC address.

---

## Q35. What is a Root Port?

**Answer:**

> On a non-root switch, the Root Port is the port providing the best path toward the Root Bridge.

---

# 80. EtherChannel Questions

## Q36. What is EtherChannel?

**Answer:**

> EtherChannel combines multiple physical Ethernet links into one logical link to provide higher aggregate bandwidth and redundancy.

---

## Q37. Why use EtherChannel?

**Answer:**

> It allows multiple physical links to operate as one logical connection, improving aggregate bandwidth and providing redundancy.

---

## Q38. What is LACP?

**Answer:**

> LACP is the Link Aggregation Control Protocol used to negotiate and manage link aggregation.

---

## Q39. What are LACP modes?

**Answer:**

```text
Active
Passive
```

Active actively negotiates LACP; passive waits for LACP negotiation.

---

## Q40. What is PAgP?

**Answer:**

> PAgP is Cisco's proprietary protocol for negotiating EtherChannel.

---

# PART VI — SCENARIO QUESTIONS

# 81. Scenario: "A user cannot log in to the domain. What do you check?"

Good answer:

> First I would check basic network connectivity, then verify the client's IP configuration and DNS settings. Since Active Directory depends on DNS, I would check whether the client can resolve the domain and locate a domain controller. Then I would check the user's account status, password, lockout status, and finally domain connectivity and time synchronization.

Possible commands:

```cmd
ipconfig /all
ping <gateway>
nslookup <domain>
ping <domain-controller>
```

---

# 82. Scenario: "The PC has 169.254.x.x. What does it mean?"

Answer:

> It usually indicates that the client did not obtain an IP address from DHCP and assigned itself an APIPA address.

Then investigate:

```text
NIC
 ↓
Switch port
 ↓
VLAN
 ↓
DHCP server
 ↓
DHCP scope
 ↓
DHCP relay if applicable
```

---

# 83. Scenario: "The user can ping 8.8.8.8 but cannot open google.com."

Answer:

> I would suspect DNS because IP connectivity works but hostname resolution is failing.

Check:

```cmd
nslookup google.com
ipconfig /all
```

---

# 84. Scenario: "Two PCs are on the same switch but cannot communicate."

Check:

```text
Are both connected?
      ↓
Correct VLAN?
      ↓
Correct IP/subnet?
      ↓
Ports operational?
      ↓
Any ACL/security issue?
```

If they are in different VLANs:

```text
Inter-VLAN routing
```

may be required.

---

# 85. Scenario: "Users in VLAN 10 can communicate, but VLAN 10 cannot communicate with VLAN 20."

Answer:

> Since VLANs are separate Layer 2 broadcast domains, communication between them requires Layer 3 routing. I would check whether an inter-VLAN routing mechanism exists and whether the hosts have the correct default gateway.

---

# 86. Scenario: "VLAN 20 works on Switch 1 but not Switch 2."

Answer:

> I would check the link between the switches and verify that it is configured as a trunk, that VLAN 20 exists where required, and that VLAN 20 is allowed on the trunk.

Commands:

```text
show vlan brief
show interfaces trunk
```

---

# 87. Scenario: "You connect two switches with two cables. What can happen?"

Answer:

> The redundant links can create a Layer 2 loop. STP is used to prevent the loop by placing redundant paths into a non-forwarding state. Alternatively, the links can potentially be bundled using EtherChannel if configured correctly.

---

# 88. Scenario: "Why not just disable the second cable?"

Answer:

> The second link provides redundancy. STP allows the redundant path to remain available while preventing a Layer 2 loop. If the primary path fails, STP can reconverge and use the redundant path.

---

# 89. Scenario: "What is the difference between STP and EtherChannel?"

Answer:

> STP prevents Layer 2 loops by controlling which paths forward traffic. EtherChannel combines multiple physical links into one logical link, allowing the links to be used together as a bundle.

Simple:

```text
STP
→ prevents loops

EtherChannel
→ combines links
```

---

# PART VII — RAPID-FIRE QUESTIONS

These are questions where you should answer immediately.

### Active Directory

**What is AD?**

> Centralized directory service for Windows environments.

**What is a DC?**

> Server running AD DS.

**What is a domain?**

> Logical administrative/security boundary.

**What is an OU?**

> Container used to organize AD objects and apply administration/policies.

**What is a user?**

> An identity/account.

**What is a group?**

> Collection of users/computers used for management and permissions.

**What is DNS?**

> Name resolution.

**What is DHCP?**

> Automatic IP configuration.

**DORA?**

> Discover, Offer, Request, Acknowledgment.

---

### Switching

**What is VLAN?**

> Logical Layer 2 segmentation.

**Access port?**

> Normally one VLAN.

**Trunk?**

> Multiple VLANs.

**STP?**

> Prevents Layer 2 loops.

**Root Bridge?**

> STP reference switch.

**EtherChannel?**

> Multiple physical links combined into one logical link.

**LACP?**

> Link Aggregation Control Protocol.

**MAC address?**

> Layer 2 hardware/interface address.

**IP address?**

> Layer 3 logical address.

---

# PART VIII — "EXPLAIN THIS TO ME" QUESTIONS

Interviewers may test whether you actually understand the concept rather than memorized a definition.

## Explain a domain in simple words.

> Imagine a company with hundreds of computers. Instead of managing each computer separately, a domain allows the organization to centrally manage users, computers, authentication, and access.

---

## Explain DNS in simple words.

> DNS is like a phone book for network names. Instead of remembering an IP address, I can use a hostname and DNS finds the corresponding IP address.

---

## Explain DHCP in simple words.

> DHCP automatically gives a device the network information it needs, such as an IP address, subnet mask, gateway, and DNS server.

---

## Explain VLAN in simple words.

> A VLAN lets me logically divide one physical switch network into separate Layer 2 networks.

---

## Explain trunk in simple words.

> A trunk is a link that carries traffic from multiple VLANs, commonly between switches.

---

## Explain STP in simple words.

> STP prevents switching loops when there are redundant connections between switches.

---

## Explain EtherChannel in simple words.

> EtherChannel combines multiple physical links so they operate as one logical connection.

---

# PART IX — COMMAND CHEAT SHEET

## Windows

```cmd
ipconfig
ipconfig /all
ipconfig /release
ipconfig /renew
ipconfig /flushdns

ping <IP>
ping <hostname>

nslookup <hostname>

tracert <IP>
```

---

## Cisco

```text
show running-config

show interfaces

show interfaces status

show interfaces trunk

show vlan brief

show mac address-table

show spanning-tree

show etherchannel summary

show ip interface brief
```

---

# PART X — MEMORY MAP

Memorize this:

```text
WINDOWS SERVER
│
├── Active Directory
│   ├── Forest
│   ├── Domain
│   ├── Domain Controller
│   ├── OU
│   ├── Users
│   └── Groups
│
├── DNS
│   ├── A
│   ├── AAAA
│   ├── CNAME
│   ├── MX
│   ├── PTR
│   └── SRV
│
└── DHCP
    └── DORA
        ├── Discover
        ├── Offer
        ├── Request
        └── ACK
```

```text
SWITCHING
│
├── MAC Address
│
├── VLAN
│
├── Access Port
│
├── Trunk
│
├── STP
│   └── Root Bridge
│
└── EtherChannel
    ├── LACP
    └── PAgP
```

---

# PART XI — THE MOST IMPORTANT RELATIONSHIPS

## Relationship 1

```text
DHCP
 ↓
IP configuration
```

## Relationship 2

```text
DNS
 ↓
Name resolution
```

## Relationship 3

```text
DNS
 ↓
Active Directory
 ↓
Domain Controller discovery
```

## Relationship 4

```text
User
 ↓
Group
 ↓
Permission
 ↓
Resource
```

## Relationship 5

```text
VLAN
 ↓
Layer 2 segmentation
```

## Relationship 6

```text
Access Port
 ↓
One VLAN
```

## Relationship 7

```text
Trunk
 ↓
Multiple VLANs
```

## Relationship 8

```text
STP
 ↓
Prevent Layer 2 loops
```

## Relationship 9

```text
EtherChannel
 ↓
Multiple physical links
 ↓
One logical link
```

---

# PART XII — TOP 25 QUESTIONS TO MASTER FIRST

If you have very limited time, master these first:

1. What is Active Directory?
2. What is a Domain Controller?
3. What is a domain?
4. Domain vs workgroup?
5. What is an OU?
6. What is a user?
7. What is a group?
8. Security group vs distribution group?
9. What is DNS?
10. Why does AD need DNS?
11. What is DHCP?
12. Explain DORA.
13. DNS vs DHCP?
14. What is a switch?
15. What is a MAC address?
16. What is a VLAN?
17. Why use VLANs?
18. Access vs trunk?
19. What is STP?
20. Why do Layer 2 loops happen?
21. What is the Root Bridge?
22. What is EtherChannel?
23. What is LACP?
24. STP vs EtherChannel?
25. How would you troubleshoot a network/user connectivity problem?

---

# PART XIII — FINAL INTERVIEW MENTAL MODEL

Don't memorize 100 disconnected definitions.

Think about one company:

```text
                    INTERNET
                       |
                    ROUTER
                       |
                  CORE/SWITCH
                       |
              +--------+--------+
              |                 |
           VLAN 10           VLAN 20
             IT                HR
              |                 |
           Access             Access
           Ports              Ports
              |                 |
              +-------+---------+
                      |
                    TRUNK
                      |
                  SWITCH
                      |
                Windows Server
                      |
        +-------------+-------------+
        |             |             |
       AD             DNS          DHCP
        |
   +----+----+
   |         |
 Users     Groups
   |         |
   +----+----+
        |
   Permissions
```

Now think about what happens when Ahmed sits at his PC:

```text
1. PC connects to switch
        ↓
2. Switch port places PC in its VLAN
        ↓
3. DHCP gives PC an IP configuration
        ↓
4. PC receives DNS server information
        ↓
5. DNS helps resolve company/domain services
        ↓
6. PC locates a Domain Controller
        ↓
7. User authenticates
        ↓
8. AD provides identity/group information
        ↓
9. Groups determine access
        ↓
10. Network infrastructure provides connectivity
```

If you understand this flow, many interview questions become much easier.

---

# LAST-MINUTE CHEAT SHEET

```text
AD
= Centralized identity/directory management

DC
= Server running AD DS

DOMAIN
= Logical administrative/security boundary

OU
= Container for organization/delegation/policies

USER
= Identity

GROUP
= Collection of identities for management/permissions

DNS
= Name → IP / service discovery

DHCP
= Automatic network configuration

DORA
= Discover → Offer → Request → ACK

VLAN
= Layer 2 segmentation

ACCESS
= One VLAN

TRUNK
= Multiple VLANs

STP
= Prevent Layer 2 loops

ROOT BRIDGE
= STP reference switch

ETHERCHANNEL
= Multiple physical links → one logical link

LACP
= Standards-based link aggregation protocol

MAC
= Layer 2 address

IP
= Layer 3 address

SWITCH
= Primarily Layer 2 forwarding

ROUTER
= Layer 3 forwarding between networks
```

# Interview Strategy

For almost every question, use this structure:

```text
1. Definition
2. Purpose
3. Simple example
4. Troubleshooting/use case if relevant
```

Example:

**Interviewer:** What is DNS?

Weak:

> DNS translates names to IP addresses.

Better:

> DNS is the Domain Name System. It resolves hostnames to IP addresses and helps clients locate network services. In an Active Directory environment, DNS is especially important because clients use it to locate domain controllers and domain services. For example, a client can resolve `server01.company.local` to its IP address.

That style demonstrates **understanding rather than memorization**.

---

# Priority Order for Revision

If your interview is soon, revise in this exact order:

```text
                    HIGH PRIORITY
                         ↓

1. Active Directory
2. Domain / Domain Controller
3. DNS
4. DHCP + DORA
5. Users + Groups
6. VLAN
7. Access vs Trunk
8. STP
9. EtherChannel
10. Troubleshooting scenarios

                    ↓

              MEDIUM PRIORITY

11. OU
12. Forest
13. DNS records
14. Authentication vs Authorization
15. LACP/PAgP
16. STP Root Bridge / Port Roles

                    ↓

              LOWER PRIORITY

17. Advanced AD architecture
18. FSMO
19. Advanced Group Policy
20. Advanced STP variants
21. Advanced routing
```

The interviewer explicitly said **"خليك في الـ basics"**, so don't let the larger MCSA/CCNA syllabi distract you. Your target is to be able to **explain the fundamentals, connect them together, and troubleshoot simple scenarios**.
