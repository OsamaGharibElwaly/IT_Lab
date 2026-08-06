
> A structured 20-video curriculum broken into 8 executable Python modules for learning, review, and hands-on practice.

---

## Table of Contents

| Module | Videos Covered | Topics |
|--------|---------------|--------|
| [Module 1: IT Foundations](#module-1-it-foundations) | 1-3 | Welcome, Intro to IT, Programs & Hardware |
| [Module 2: Hardware & Mobile](#module-2-hardware--mobile) | 4-5 | Build a Computer, Mobile IT Support |
| [Module 3: Operating Systems](#module-3-operating-systems) | 6-7 | OS Composition, Installation & Management |
| [Module 4: Internet & Software](#module-4-internet--software) | 8-9 | Internet Deep Dive, Software Lifecycle |
| [Module 5: Professional Skills](#module-5-professional-skills) | 10-13 | Customer Service, Troubleshooting, Career Insights |
| [Module 6: Networking Fundamentals](#module-6-networking-fundamentals) | 14, 20 | Computer Communication, Network Layer Components |
| [Module 7: Storage & Identity](#module-7-storage--identity) | 16, 18 | Disks & Filesystems, Users & Groups |
| [Module 8: Networking Services](#module-8-networking-services) | 17, 19 | Best Practices, DNS Deep Dive |

---

## Module 1: IT Foundations
**Videos:** 1, 2, 3

### Lesson 1.1 - Welcome to IT Support

**Key Concepts:**
- IT Support as the backbone of modern organizations
- The Google IT Support Certificate pathway
- Career opportunities: Help Desk -> System Admin -> Network Engineer -> IT Manager

**Vocabulary:**
| Term | Definition |
|------|------------|
| **IT Support** | Technical assistance provided to end-users experiencing computer, software, or network issues |
| **Help Desk** | First line of support; handles initial triage and ticket resolution |
| **Escalation** | Process of forwarding unresolved issues to higher-tier support |
| **SLA** | Service Level Agreement; defines response and resolution time expectations |

**Grammar Focus:** Professional communication tone - polite, clear, and solution-oriented.

**Dialogue Example:**
> **User:** "My computer won't turn on."
> **IT Support:** "I understand how frustrating that can be. Let's troubleshoot together. First, can you confirm the power cable is securely connected?"

**Code Sample - Ticket System Simulation:**
```python
# module1_ticket_system.py
class ITTicket:
    def __init__(self, ticket_id, user, issue, priority="Medium"):
        self.ticket_id = ticket_id
        self.user = user
        self.issue = issue
        self.priority = priority
        self.status = "Open"
        self.resolution = None
    
    def escalate(self, reason):
        self.priority = "High"
        return f"Ticket #{self.ticket_id} escalated: {reason}"
    
    def resolve(self, solution):
        self.status = "Resolved"
        self.resolution = solution
        return f"Ticket #{self.ticket_id} resolved: {solution}"

# Example usage
ticket = ITTicket(101, "Alice", "Cannot access email", "High")
print(ticket.escalate("Requires admin privileges"))
print(ticket.resolve("Reset password and cleared cache"))
```

---

### Lesson 1.2 - Intro to IT

**Key Concepts:**
- Definition of Information Technology
- The IT ecosystem: hardware, software, networks, data, people
- Binary system (0s and 1s) as the foundation of computing
- Bits, bytes, and data representation

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Bit** | Smallest unit of data; binary digit (0 or 1) |
| **Byte** | 8 bits; basic unit of memory/storage |
| **Binary** | Base-2 number system used by computers |
| **ASCII** | Character encoding standard mapping numbers to letters |

**Code Sample - Binary Converter:**
```python
# module1_binary_converter.py
def text_to_binary(text):
    return ' '.join(format(ord(char), '08b') for char in text)

def binary_to_text(binary_str):
    bytes_list = binary_str.split()
    return ''.join(chr(int(byte, 2)) for byte in bytes_list)

# Example
message = "IT"
binary = text_to_binary(message)
print(f"'{message}' in binary: {binary}")
print(f"Back to text: {binary_to_text(binary)}")
```

---

### Lesson 1.3 - Modern Computer Programs & Hardware

**Key Concepts:**
- CPU, RAM, Storage, Motherboard, GPU
- Von Neumann architecture
- Input -> Process -> Output -> Storage cycle
- Programs vs. processes vs. services

**Vocabulary:**
| Term | Definition |
|------|------------|
| **CPU** | Central Processing Unit; the "brain" executing instructions |
| **RAM** | Random Access Memory; volatile, fast temporary storage |
| **Motherboard** | Main circuit board connecting all components |
| **GPU** | Graphics Processing Unit; handles rendering and parallel computation |
| **BIOS/UEFI** | Firmware initializing hardware during boot |

**Code Sample - System Info Simulator:**
```python
# module1_system_info.py
class Computer:
    def __init__(self, cpu, ram_gb, storage_gb, gpu=None):
        self.cpu = cpu
        self.ram_gb = ram_gb
        self.storage_gb = storage_gb
        self.gpu = gpu
        self.powered_on = False
    
    def boot(self):
        self.powered_on = True
        return f"Booting {self.cpu} with {self.ram_gb}GB RAM... BIOS loaded. OS starting."
    
    def get_specs(self):
        specs = f"CPU: {self.cpu}\nRAM: {self.ram_gb}GB\nStorage: {self.storage_gb}GB"
        if self.gpu:
            specs += f"\nGPU: {self.gpu}"
        return specs

pc = Computer("Intel i7-12700K", 16, 512, "NVIDIA RTX 3060")
print(pc.boot())
print("\n--- System Specs ---")
print(pc.get_specs())
```

---

## Module 2: Hardware & Mobile
**Videos:** 4, 5

### Lesson 2.1 - Build a Computer in 20 Minutes

**Key Concepts:**
- Step-by-step PC assembly
- Component compatibility (socket types, form factors, wattage)
- Thermal management and cable management
- POST (Power-On Self Test) and beep codes

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Form Factor** | Physical size standard (ATX, Micro-ATX, Mini-ITX) |
| **Thermal Paste** | Compound improving heat transfer between CPU and cooler |
| **POST** | Power-On Self Test; hardware diagnostic on boot |
| **PSU** | Power Supply Unit; converts AC to DC for components |

**Build Checklist:**
1. Install CPU onto motherboard (align triangle markers)
2. Apply thermal paste and mount CPU cooler
3. Install RAM into DIMM slots (check notch alignment)
4. Mount motherboard into case with standoffs
5. Install storage drives (SSD/HDD)
6. Connect PSU cables (24-pin motherboard, 8-pin CPU, SATA power)
7. Install GPU into PCIe x16 slot
8. Connect front panel headers (power, reset, LEDs)
9. Power on and verify POST success

**Code Sample - Build Validator:**
```python
# module2_build_validator.py
class PCBuilder:
    REQUIRED_COMPONENTS = ["cpu", "motherboard", "ram", "storage", "psu", "case"]
    
    def __init__(self):
        self.components = {}
    
    def add_component(self, name, spec):
        self.components[name] = spec
        return f"Added {name}: {spec}"
    
    def validate_build(self):
        missing = [c for c in self.REQUIRED_COMPONENTS if c not in self.components]
        if missing:
            return f"Missing: {', '.join(missing)}"
        return "Build validated! Ready for assembly."
    
    def estimate_wattage(self):
        wattage = {"cpu": 65, "gpu": 170, "ram": 5, "storage": 10, "motherboard": 50}
        total = sum(wattage.get(k, 0) for k in self.components)
        return f"Estimated power draw: ~{total}W (recommend {int(total * 1.3)}W PSU)"

builder = PCBuilder()
builder.add_component("cpu", "AMD Ryzen 5 5600X")
builder.add_component("motherboard", "B550 ATX")
builder.add_component("ram", "16GB DDR4")
builder.add_component("storage", "1TB NVMe SSD")
builder.add_component("psu", "650W 80+ Gold")
builder.add_component("case", "Mid Tower ATX")
builder.add_component("gpu", "RTX 3060")
print(builder.validate_build())
print(builder.estimate_wattage())
```

---

### Lesson 2.2 - IT Support for Mobile Devices

**Key Concepts:**
- Mobile OS: Android vs. iOS architecture
- MDM (Mobile Device Management)
- Common mobile issues: battery, connectivity, app crashes
- BYOD (Bring Your Own Device) policies

**Vocabulary:**
| Term | Definition |
|------|------------|
| **MDM** | Mobile Device Management; enterprise control of mobile devices |
| **APK/IPA** | Android/iOS application package formats |
| **Rooting/Jailbreaking** | Gaining superuser access to mobile OS |
| **BYOD** | Bring Your Own Device; personal device use for work |

**Code Sample - Mobile Device Manager:**
```python
# module2_mobile_manager.py
class MobileDevice:
    def __init__(self, device_id, os_type, owner, enrolled=False):
        self.device_id = device_id
        self.os_type = os_type  # "Android" or "iOS"
        self.owner = owner
        self.enrolled = enrolled
        self.policies = []
        self.apps = []
    
    def enroll(self, mdm_server):
        self.enrolled = True
        return f"Device {self.device_id} enrolled to {mdm_server}"
    
    def apply_policy(self, policy):
        self.policies.append(policy)
        return f"Applied: {policy}"
    
    def remote_wipe(self):
        self.apps = []
        self.policies = []
        return f"Device {self.device_id} remotely wiped!"

# Example
device = MobileDevice("MD-8821", "iOS", "john.doe@company.com")
print(device.enroll("mdm.company.com"))
print(device.apply_policy("Require Passcode (6-digit)"))
print(device.apply_policy("Disable Camera in Secure Zones"))
print(device.remote_wipe())
```

---

## Module 3: Operating Systems
**Videos:** 6, 7

### Lesson 3.1 - Operating Systems: Composition and Management

**Key Concepts:**
- Kernel, Shell, File System, User Interface
- Process management, memory management, I/O management
- Multitasking, multithreading, multiprocessing
- System calls and APIs

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Kernel** | Core OS component managing hardware and software interactions |
| **Shell** | Command-line interface interpreting user commands |
| **Process** | Running instance of a program |
| **Daemon** | Background process running without user interaction |
| **Scheduler** | Algorithm deciding which process gets CPU time |

**Code Sample - OS Process Simulator:**
```python
# module3_os_simulator.py
from collections import deque

class Process:
    def __init__(self, pid, name, priority, burst_time):
        self.pid = pid
        self.name = name
        self.priority = priority
        self.burst_time = burst_time
        self.state = "Ready"
    
    def __repr__(self):
        return f"P{self.pid}({self.name}, prio={self.priority}, t={self.burst_time})"

class Scheduler:
    def __init__(self, algorithm="Round Robin"):
        self.algorithm = algorithm
        self.ready_queue = deque()
        self.clock = 0
    
    def add_process(self, process):
        self.ready_queue.append(process)
    
    def run_round_robin(self, quantum=2):
        results = []
        while self.ready_queue:
            proc = self.ready_queue.popleft()
            proc.state = "Running"
            exec_time = min(quantum, proc.burst_time)
            self.clock += exec_time
            proc.burst_time -= exec_time
            
            if proc.burst_time > 0:
                proc.state = "Ready"
                self.ready_queue.append(proc)
            else:
                proc.state = "Terminated"
            
            results.append(f"t={self.clock}: {proc.name} ran for {exec_time}s, state={proc.state}")
        return results

# Simulate
scheduler = Scheduler()
scheduler.add_process(Process(1, "Browser", 2, 5))
scheduler.add_process(Process(2, "Editor", 1, 3))
scheduler.add_process(Process(3, "Music", 3, 4))

for log in scheduler.run_round_robin(quantum=2):
    print(log)
```

---

### Lesson 3.2 - Operating Systems: Considerations and Installation

**Key Concepts:**
- Choosing an OS: Windows, macOS, Linux distributions
- Licensing, hardware compatibility, use-case fit
- Installation methods: USB boot, network boot, VM
- Partitioning schemes: MBR vs. GPT
- Dual-boot and virtualization

**Vocabulary:**
| Term | Definition |
|------|------------|
| **MBR** | Master Boot Record; legacy partitioning (max 2TB, 4 primary partitions) |
| **GPT** | GUID Partition Table; modern standard (128 partitions, >2TB support) |
| **UEFI** | Unified Extensible Firmware Interface; modern replacement for BIOS |
| **Live USB** | Bootable OS running from USB without installation |
| **Virtual Machine** | Emulated computer running inside host OS |

**Code Sample - OS Installation Planner:**
```python
# module3_os_installer.py
class OSInstaller:
    OS_OPTIONS = {
        "Windows 11": {"ram_min": 4, "storage_min": 64, "uefi": True, "license": "Proprietary"},
        "Ubuntu 22.04": {"ram_min": 2, "storage_min": 25, "uefi": True, "license": "GPL"},
        "macOS Ventura": {"ram_min": 4, "storage_min": 35, "uefi": True, "license": "Proprietary"},
        "Debian 12": {"ram_min": 1, "storage_min": 10, "uefi": True, "license": "GPL"}
    }
    
    def __init__(self, ram_gb, storage_gb, uefi_supported=True):
        self.ram_gb = ram_gb
        self.storage_gb = storage_gb
        self.uefi_supported = uefi_supported
    
    def check_compatibility(self, os_name):
        os_info = self.OS_OPTIONS.get(os_name)
        if not os_info:
            return f"Unknown OS: {os_name}"
        
        issues = []
        if self.ram_gb < os_info["ram_min"]:
            issues.append(f"RAM insufficient (need {os_info['ram_min']}GB, have {self.ram_gb}GB)")
        if self.storage_gb < os_info["storage_min"]:
            issues.append(f"Storage insufficient (need {os_info['storage_min']}GB, have {self.storage_gb}GB)")
        if os_info["uefi"] and not self.uefi_supported:
            issues.append("UEFI required but not supported")
        
        if issues:
            return f"{os_name}: {', '.join(issues)}"
        return f"{os_name} is compatible! License: {os_info['license']}"
    
    def list_compatible(self):
        return {os: self.check_compatibility(os) for os in self.OS_OPTIONS}

# Example
installer = OSInstaller(ram_gb=8, storage_gb=256)
for os_name, result in installer.list_compatible().items():
    print(result)
```

---

## Module 4: Internet & Software
**Videos:** 8, 9

### Lesson 4.1 - An In-Depth Look at the Internet

**Key Concepts:**
- Internet vs. World Wide Web
- TCP/IP protocol suite
- Packets, routing, and switching
- DNS, HTTP/HTTPS, IP addresses (IPv4 vs. IPv6)
- Latency, bandwidth, throughput

**Vocabulary:**
| Term | Definition |
|------|------------|
| **IP Address** | Unique identifier for devices on a network |
| **DNS** | Domain Name System; translates domain names to IP addresses |
| **Packet** | Unit of data transmitted over a network |
| **Router** | Device forwarding packets between networks |
| **Latency** | Time delay for data to travel from source to destination |
| **Bandwidth** | Maximum data transfer rate of a network connection |

**Code Sample - Network Packet Simulator:**
```python
# module4_network_simulator.py
import random

class Packet:
    def __init__(self, src_ip, dst_ip, payload, protocol="TCP"):
        self.src_ip = src_ip
        self.dst_ip = dst_ip
        self.payload = payload
        self.protocol = protocol
        self.ttl = 64  # Time To Live
        self.hops = 0
    
    def __repr__(self):
        return f"[{self.protocol}] {self.src_ip} -> {self.dst_ip} (TTL={self.ttl})"

class Router:
    def __init__(self, name, routing_table):
        self.name = name
        self.routing_table = routing_table  # {dest_network: next_hop}
    
    def forward(self, packet):
        packet.ttl -= 1
        packet.hops += 1
        if packet.ttl <= 0:
            return f"Packet dropped at {self.name}: TTL expired"
        
        dst_network = '.'.join(packet.dst_ip.split('.')[:3]) + '.0/24'
        next_hop = self.routing_table.get(dst_network, "Default Gateway")
        return f"{self.name}: Forwarding to {next_hop} | {packet}"

# Simulate a packet journey
packet = Packet("192.168.1.10", "10.0.0.50", "Hello Internet!")
router_a = Router("Router-A", {"10.0.0.0/24": "Router-B"})
router_b = Router("Router-B", {"10.0.0.0/24": "Direct Delivery"})

print(packet)
print(router_a.forward(packet))
print(router_b.forward(packet))
```

---

### Lesson 4.2 - Software: Installation, Removal, and Everything in Between

**Key Concepts:**
- Software lifecycle: acquisition -> installation -> configuration -> maintenance -> removal
- Package managers: apt, yum, winget, brew
- Registry (Windows) vs. config files (Linux/macOS)
- Dependencies and compatibility
- Licensing: proprietary, open-source, freeware, shareware

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Package Manager** | Tool automating software installation and dependency resolution |
| **Dependency** | External library or program required for software to run |
| **Registry** | Windows hierarchical database storing configuration settings |
| **Repository** | Centralized storage location for software packages |
| **Sandbox** | Isolated environment for testing software safely |

**Code Sample - Software Package Manager:**
```python
# module4_package_manager.py
class PackageManager:
    def __init__(self, os_type):
        self.os_type = os_type
        self.installed = {}
        self.repos = {
            "Ubuntu": ["main", "universe", "multiverse"],
            "Windows": ["winget", "chocolatey"],
            "macOS": ["homebrew", "macports"]
        }
    
    def install(self, package_name, version=None):
        if package_name in self.installed:
            return f"{package_name} already installed (v{self.installed[package_name]})"
        ver = version or "latest"
        self.installed[package_name] = ver
        return f"Installed {package_name} v{ver} via {self.os_type} repo"
    
    def remove(self, package_name, purge=False):
        if package_name not in self.installed:
            return f"{package_name} not found"
        del self.installed[package_name]
        mode = "purged" if purge else "removed"
        return f"{package_name} {mode}"
    
    def list_installed(self):
        return self.installed

# Example
pm = PackageManager("Ubuntu")
print(pm.install("python3", "3.10.12"))
print(pm.install("nginx"))
print(pm.install("python3"))  # Duplicate
print(pm.remove("nginx", purge=True))
print("Installed:", pm.list_installed())
```

---

## Module 5: Professional Skills
**Videos:** 10, 11, 12, 13

### Lesson 5.1 - IT Customer Service

**Key Concepts:**
- Active listening and empathy in technical support
- Ticket management and documentation
- De-escalation techniques
- Follow-up and feedback loops
- Professional communication (email, phone, chat, in-person)

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Active Listening** | Fully concentrating on, understanding, and responding to the speaker |
| **Empathy Statement** | Acknowledging the user's feelings before addressing the technical issue |
| **First Call Resolution (FCR)** | Resolving an issue during the initial contact |
| **Knowledge Base** | Centralized repository of solutions and documentation |

**Dialogue Framework:**
```
1. GREET: "Thank you for contacting IT Support."
2. ACKNOWLEDGE: "I understand this issue is impacting your work."
3. INVESTIGATE: "Let me ask a few questions to narrow this down."
4. RESOLVE: "Here's what we'll do to fix this..."
5. VERIFY: "Can you confirm the issue is resolved?"
6. CLOSE: "Is there anything else I can help with today?"
```

**Code Sample - Customer Interaction Logger:**
```python
# module5_customer_service.py
from datetime import datetime

class SupportInteraction:
    def __init__(self, ticket_id, customer_name, channel):
        self.ticket_id = ticket_id
        self.customer_name = customer_name
        self.channel = channel  # email, phone, chat, in-person
        self.log = []
        self.resolved = False
    
    def add_entry(self, speaker, message):
        timestamp = datetime.now().strftime("%H:%M:%S")
        self.log.append(f"[{timestamp}] {speaker}: {message}")
    
    def apply_empathy(self, issue):
        responses = {
            "slow": "I completely understand how frustrating a slow computer can be.",
            "crash": "I'm sorry to hear your application keeps crashing. Let's fix this together.",
            "locked": "Getting locked out is never convenient. I'll get you back in quickly."
        }
        return responses.get(issue.lower(), "I understand this is inconvenient.")
    
    def generate_report(self):
        header = f"=== Ticket #{self.ticket_id} | {self.customer_name} | {self.channel} ==="
        return "\n".join([header] + self.log)

# Example interaction
interaction = SupportInteraction(2047, "Sarah Chen", "chat")
interaction.add_entry("Agent", interaction.apply_empathy("crash"))
interaction.add_entry("Agent", "Can you tell me which application crashed?")
interaction.add_entry("Customer", "It's Excel. It freezes when I open large files.")
interaction.add_entry("Agent", "Let's try opening in Safe Mode. Press Ctrl while launching Excel.")
print(interaction.generate_report())
```

---

### Lesson 5.2 - Why Troubleshooting is Critical in IT

**Key Concepts:**
- Systematic troubleshooting methodology
- The CompTIA 6-step process: Identify -> Establish theory -> Test -> Plan -> Implement -> Verify -> Document
- Root cause analysis vs. symptom treatment
- Common troubleshooting tools: ping, ipconfig, Event Viewer, Task Manager

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Root Cause** | Underlying reason for a problem, not just the symptom |
| **Divide and Conquer** | Isolating problem halves to narrow down causes |
| **Top-Down Troubleshooting** | Starting from application layer moving to physical |
| **Bottom-Up Troubleshooting** | Starting from physical layer moving to application |

**Code Sample - Troubleshooting Decision Tree:**
```python
# module5_troubleshooting.py
class Troubleshooter:
    def __init__(self, issue_type):
        self.issue_type = issue_type
        self.steps_taken = []
        self.resolved = False
    
    def diagnose(self):
        trees = {
            "no_internet": [
                ("Check physical connections", "cable_ok"),
                ("Restart router", "router_restarted"),
                ("Run ipconfig /release && /renew", "ip_renewed"),
                ("Check DNS settings", "dns_ok"),
                ("Contact ISP", "isp_issue")
            ],
            "slow_computer": [
                ("Check Task Manager for high CPU/RAM", "resources_ok"),
                ("Run disk cleanup", "disk_cleaned"),
                ("Disable startup programs", "startup_optimized"),
                ("Check for malware", "malware_scan_done"),
                ("Upgrade RAM/SSD", "hardware_upgraded")
            ]
        }
        return trees.get(self.issue_type, [("Unknown issue", "escalate")])
    
    def run_diagnosis(self):
        steps = self.diagnose()
        print(f"Troubleshooting: {self.issue_type}")
        for i, (action, result_key) in enumerate(steps, 1):
            self.steps_taken.append(action)
            print(f"  Step {i}: {action} -> [{result_key}]")
        return self.steps_taken

# Example
ts = Troubleshooter("no_internet")
ts.run_diagnosis()
```

---

### Lesson 5.3 - One Surprising Fact About IT Professionals

**Key Concepts:**
- IT is fundamentally about helping people, not just technology
- Soft skills often outweigh technical skills in career advancement
- Continuous learning is the only constant in IT
- Imposter syndrome is common; documentation and community help

**Reflection Prompt:**
> "The best IT professionals aren't those who know every answer - they're the ones who know how to find the answer and communicate it clearly."

**Code Sample - Skill Tracker:**
```python
# module5_skill_tracker.py
class ITProfessional:
    SKILL_CATEGORIES = {
        "Technical": ["Networking", "OS Administration", "Scripting", "Security"],
        "Soft Skills": ["Communication", "Empathy", "Problem Solving", "Patience"],
        "Business": ["Project Management", "Documentation", "SLA Management"]
    }
    
    def __init__(self, name):
        self.name = name
        self.skills = {cat: {skill: 0 for skill in skills} 
                      for cat, skills in self.SKILL_CATEGORIES.items()}
    
    def rate_skill(self, category, skill, level):
        if category in self.skills and skill in self.skills[category]:
            self.skills[category][skill] = min(10, max(0, level))
            return f"{skill}: {level}/10"
        return "Invalid category or skill"
    
    def get_profile(self):
        profile = f"\n{self.name} - IT Professional Profile\n"
        for cat, skills in self.skills.items():
            profile += f"\n{cat}:\n"
            for skill, level in skills.items():
                bar = "#" * level + "-" * (10 - level)
                profile += f"  {skill:20} [{bar}] {level}/10\n"
        return profile

# Example
pro = ITProfessional("Alex Rivera")
pro.rate_skill("Technical", "Networking", 7)
pro.rate_skill("Technical", "Scripting", 5)
pro.rate_skill("Soft Skills", "Communication", 9)
pro.rate_skill("Soft Skills", "Empathy", 8)
print(pro.get_profile())
```

---

### Lesson 5.4 - Technology is an Equalizer

**Key Concepts:**
- No prior experience required for IT entry-level roles
- Transferable skills from any background (retail, teaching, hospitality)
- Free and low-cost learning resources
- Community support and mentorship
- Certifications as career accelerators

**Code Sample - Career Path Planner:**
```python
# module5_career_path.py
class ITCareerPath:
    PATHS = {
        "Help Desk": {
            "entry_certs": ["Google IT Support", "CompTIA A+"],
            "skills": ["Customer Service", "Troubleshooting", "OS Basics"],
            "next_roles": ["System Administrator", "Network Technician"],
            "salary_range": "$35k - $55k"
        },
        "System Admin": {
            "entry_certs": ["CompTIA Server+", "Microsoft Azure Fundamentals"],
            "skills": ["Active Directory", "Linux", "Virtualization"],
            "next_roles": ["Cloud Engineer", "DevOps Engineer"],
            "salary_range": "$55k - $85k"
        },
        "Network Engineer": {
            "entry_certs": ["CompTIA Network+", "Cisco CCNA"],
            "skills": ["Routing & Switching", "TCP/IP", "Network Security"],
            "next_roles": ["Network Architect", "Security Engineer"],
            "salary_range": "$65k - $100k"
        }
    }
    
    @classmethod
    def explore_path(cls, role):
        path = cls.PATHS.get(role)
        if not path:
            return f"Role '{role}' not found. Available: {list(cls.PATHS.keys())}"
        
        report = f"\nCareer Path: {role}\n"
        report += f"Salary Range: {path['salary_range']}\n"
        report += f"Entry Certs: {', '.join(path['entry_certs']}\n"
        report += f"Key Skills: {', '.join(path['skills'])}\n"
        report += f"Next Steps: {', '.join(path['next_roles'])}\n"
        return report

print(ITCareerPath.explore_path("Help Desk"))
print(ITCareerPath.explore_path("System Admin"))
```

---

## Module 6: Networking Fundamentals
**Videos:** 14, 20

### Lesson 6.1 - How Computers Communicate in a Network

**Key Concepts:**
- LAN, WAN, MAN, PAN topologies
- OSI Model (7 layers) and TCP/IP Model (4 layers)
- MAC addresses and ARP
- Switches vs. hubs vs. routers
- Subnetting and CIDR notation

**Vocabulary:**
| Term | Definition |
|------|------------|
| **LAN** | Local Area Network; covers small geographic area |
| **WAN** | Wide Area Network; spans large distances (e.g., the Internet) |
| **MAC Address** | Hardware address unique to each network interface |
| **ARP** | Address Resolution Protocol; maps IP to MAC addresses |
| **CIDR** | Classless Inter-Domain Routing; IP allocation method |
| **Subnet Mask** | Defines network and host portions of an IP address |

**OSI Model Quick Reference:**
```
Layer 7: Application  - HTTP, FTP, SMTP
Layer 6: Presentation - SSL/TLS, JPEG, ASCII
Layer 5: Session      - NetBIOS, RPC
Layer 4: Transport    - TCP, UDP
Layer 3: Network      - IP, ICMP, Routing
Layer 2: Data Link    - Ethernet, MAC, ARP
Layer 1: Physical     - Cables, Hubs, Signals
```

**Code Sample - Network Topology Simulator:**
```python
# module6_network_topology.py
class NetworkDevice:
    def __init__(self, name, device_type, mac_address):
        self.name = name
        self.device_type = device_type  # PC, Switch, Router
        self.mac_address = mac_address
        self.ports = {}
    
    def connect(self, port, other_device, other_port):
        self.ports[port] = (other_device, other_port)
        other_device.ports[other_port] = (self, port)
        return f"Connected {self.name}:{port} <-> {other_device.name}:{other_port}"
    
    def arp_request(self, target_ip):
        return f"[{self.name}] ARP: Who has {target_ip}? Tell {self.mac_address}"

class Network:
    def __init__(self):
        self.devices = []
    
    def add_device(self, device):
        self.devices.append(device)
    
    def trace_path(self, src, dst):
        return f"Path: {src.name} -> [Switch] -> [Router] -> [Switch] -> {dst.name}"

# Build a simple LAN
pc1 = NetworkDevice("PC-Alice", "PC", "AA:BB:CC:11:22:33")
pc2 = NetworkDevice("PC-Bob", "PC", "AA:BB:CC:44:55:66")
switch = NetworkDevice("Switch-1", "Switch", "00:11:22:33:44:55")
router = NetworkDevice("Router-1", "Router", "00:AA:BB:CC:DD:EE")

lan = Network()
lan.add_device(pc1)
lan.add_device(pc2)
lan.add_device(switch)
lan.add_device(router)

print(pc1.connect("eth0", switch, "port1"))
print(pc2.connect("eth0", switch, "port2"))
print(switch.connect("uplink", router, "lan0"))
print(pc1.arp_request("192.168.1.20"))
print(lan.trace_path(pc1, pc2))
```

---

### Lesson 6.2 - Understanding the Components of the Network Layer

**Key Concepts:**
- IP addressing: IPv4 (32-bit) vs. IPv6 (128-bit)
- Routing protocols: RIP, OSPF, BGP, EIGRP
- Default gateway and static vs. dynamic routing
- NAT (Network Address Translation)
- ICMP and ping/traceroute

**Vocabulary:**
| Term | Definition |
|------|------------|
| **IPv4** | 32-bit addressing (e.g., 192.168.1.1) - ~4.3 billion addresses |
| **IPv6** | 128-bit addressing (e.g., 2001:0db8::1) - virtually unlimited |
| **NAT** | Network Address Translation; maps private IPs to public IP |
| **BGP** | Border Gateway Protocol; routes between autonomous systems |
| **OSPF** | Open Shortest Path First; interior gateway protocol |
| **ICMP** | Internet Control Message Protocol; used by ping and traceroute |

**Code Sample - IP Address & Subnet Calculator:**
```python
# module6_ip_calculator.py
import ipaddress

class NetworkCalculator:
    def __init__(self, cidr):
        self.network = ipaddress.ip_network(cidr, strict=False)
    
    def get_info(self):
        return {
            "Network Address": str(self.network.network_address),
            "Broadcast Address": str(self.network.broadcast_address),
            "Subnet Mask": str(self.network.netmask),
            "Total Hosts": self.network.num_addresses - 2,
            "Usable Range": f"{self.network.network_address + 1} - {self.network.broadcast_address - 1}"
        }
    
    def is_host_in_network(self, ip):
        return ipaddress.ip_address(ip) in self.network
    
    @staticmethod
    def ipv6_expand(ipv6_addr):
        return str(ipaddress.ip_address(ipv6_addr).exploded)

# Example
calc = NetworkCalculator("192.168.1.0/24")
print("=== IPv4 Network Info ===")
for key, value in calc.get_info().items():
    print(f"{key}: {value}")

print(f"\nIs 192.168.1.50 in network? {calc.is_host_in_network('192.168.1.50')}")
print(f"Is 10.0.0.1 in network? {calc.is_host_in_network('10.0.0.1')}")
print(f"\nExpanded IPv6: {NetworkCalculator.ipv6_expand('2001:db8::1')}")
```

---

## Module 7: Storage & Identity
**Videos:** 16, 18

### Lesson 7.1 - Disks and Filesystem Types

**Key Concepts:**
- Storage types: HDD, SSD, NVMe, optical, flash
- Filesystems: NTFS, FAT32, exFAT, APFS, ext4, XFS, ZFS
- Partitioning, formatting, mounting
- RAID levels: 0, 1, 5, 6, 10
- Disk management tools

**Vocabulary:**
| Term | Definition |
|------|------------|
| **NTFS** | New Technology File System; Windows default (journaling, ACLs) |
| **ext4** | Fourth Extended Filesystem; Linux default |
| **APFS** | Apple File System; macOS default |
| **RAID** | Redundant Array of Independent Disks; combines multiple drives |
| **Journaling** | Logs changes before applying them; prevents corruption |
| **Mount Point** | Directory where a filesystem is attached in the OS |

**RAID Comparison:**
| Level | Description | Min Drives | Fault Tolerance | Use Case |
|-------|-------------|-----------|-----------------|----------|
| RAID 0 | Striping | 2 | None | Performance |
| RAID 1 | Mirroring | 2 | 1 drive | Redundancy |
| RAID 5 | Striping + Parity | 3 | 1 drive | Balanced |
| RAID 6 | Striping + Double Parity | 4 | 2 drives | High redundancy |
| RAID 10 | Mirror + Strip | 4 | 1 per mirror | Performance + Redundancy |

**Code Sample - RAID Calculator:**
```python
# module7_raid_calculator.py
class RAIDCalculator:
    RAID_CONFIGS = {
        0: {"description": "Striping", "min_drives": 2, "fault_tolerance": 0, "efficiency": 1.0},
        1: {"description": "Mirroring", "min_drives": 2, "fault_tolerance": 1, "efficiency": 0.5},
        5: {"description": "Striping + Parity", "min_drives": 3, "fault_tolerance": 1, "efficiency": "(n-1)/n"},
        6: {"description": "Striping + Double Parity", "min_drives": 4, "fault_tolerance": 2, "efficiency": "(n-2)/n"},
        10: {"description": "Mirror + Strip", "min_drives": 4, "fault_tolerance": "1 per mirror", "efficiency": 0.5}
    }
    
    @classmethod
    def calculate(cls, raid_level, drive_count, drive_size_gb):
        config = cls.RAID_CONFIGS.get(raid_level)
        if not config:
            return "Invalid RAID level"
        
        if drive_count < config["min_drives"]:
            return f"Need at least {config['min_drives']} drives for RAID {raid_level}"
        
        if raid_level == 0:
            usable = drive_count * drive_size_gb
        elif raid_level == 1:
            usable = drive_size_gb
        elif raid_level == 5:
            usable = (drive_count - 1) * drive_size_gb
        elif raid_level == 6:
            usable = (drive_count - 2) * drive_size_gb
        elif raid_level == 10:
            usable = (drive_count // 2) * drive_size_gb
        
        return f"""
RAID {raid_level} - {config['description']}
   Drives: {drive_count} x {drive_size_gb}GB
   Usable Space: {usable}GB
   Fault Tolerance: {config['fault_tolerance']} drive(s)
   Min Drives Required: {config['min_drives']}
        """.strip()

print(RAIDCalculator.calculate(5, 4, 1000))
print()
print(RAIDCalculator.calculate(10, 4, 2000))
```

---

### Lesson 7.2 - Users, Administrators, and Groups

**Key Concepts:**
- Authentication vs. authorization
- User accounts: standard, administrator, guest, service accounts
- Groups: local, domain, security, distribution
- Permissions: read, write, execute, modify, full control
- UAC (User Account Control) and sudo
- ACLs (Access Control Lists)

**Vocabulary:**
| Term | Definition |
|------|------------|
| **Authentication** | Verifying identity (who you are) |
| **Authorization** | Granting access rights (what you can do) |
| **UAC** | User Account Control; Windows privilege elevation prompt |
| **sudo** | Superuser do; Linux command for elevated privileges |
| **ACL** | Access Control List; defines permissions for users/groups |
| **Service Account** | Dedicated account for applications/processes |

**Permission Matrix (Linux):**
```
Owner | Group | Others
  rwx |  rwx  |  rwx
  421 |  421  |  421
  --- |  ---  |  ---
  7   |   7   |   7   = 777 (full access)
  7   |   5   |   5   = 755 (rwxr-xr-x)
  6   |   4   |   4   = 644 (rw-r--r--)
```

**Code Sample - Permission Manager:**
```python
# module7_permission_manager.py
class PermissionManager:
    PERMISSIONS = {"read": 4, "write": 2, "execute": 1}
    
    def __init__(self, file_name):
        self.file_name = file_name
        self.acl = {"owner": set(), "group": set(), "others": set()}
    
    def set_permissions(self, owner_perms, group_perms, others_perms):
        self.acl["owner"] = set(owner_perms)
        self.acl["group"] = set(group_perms)
        self.acl["others"] = set(others_perms)
        return self.get_numeric()
    
    def get_numeric(self):
        result = ""
        for entity in ["owner", "group", "others"]:
            score = sum(self.PERMISSIONS.get(p, 0) for p in self.acl[entity])
            result += str(score)
        return result
    
    def get_symbolic(self):
        symbols = ""
        for entity in ["owner", "group", "others"]:
            for perm in ["read", "write", "execute"]:
                symbols += perm[0].upper() if perm in self.acl[entity] else "-"
        return symbols
    
    def check_access(self, user, requested_perm):
        if user == "owner":
            return requested_perm in self.acl["owner"]
        elif user == "group":
            return requested_perm in self.acl["group"]
        return requested_perm in self.acl["others"]

# Example
pm = PermissionManager("report.pdf")
pm.set_permissions(["read", "write"], ["read"], ["read"])
print(f"File: {pm.file_name}")
print(f"Numeric: {pm.get_numeric()}")
print(f"Symbolic: {pm.get_symbolic()}")
print(f"Owner can write? {pm.check_access('owner', 'write')}")
print(f"Others can write? {pm.check_access('others', 'write')}")
```

---

## Module 8: Networking Services
**Videos:** 17, 19

### Lesson 8.1 - Networking Services: Best Practices and Technologies

**Key Concepts:**
- DHCP: automatic IP assignment
- DNS: domain name resolution
- NAT/PAT: address translation
- VPN: secure remote access
- Proxy servers and load balancers
- Firewalls and port security
- Network monitoring and logging

**Vocabulary:**
| Term | Definition |
|------|------------|
| **DHCP** | Dynamic Host Configuration Protocol; auto-assigns IP addresses |
| **NAT** | Network Address Translation; maps private to public IPs |
| **VPN** | Virtual Private Network; encrypted tunnel over public network |
| **Proxy** | Intermediary server forwarding client requests |
| **Load Balancer** | Distributes traffic across multiple servers |
| **Firewall** | Security system monitoring/filtering network traffic |

**Code Sample - DHCP Lease Simulator:**
```python
# module8_dhcp_simulator.py
class DHCPServer:
    def __init__(self, network, start_ip, end_ip, lease_time=3600):
        self.network = network
        self.pool = self._generate_pool(start_ip, end_ip)
        self.leases = {}  # mac -> {ip, expiry}
        self.lease_time = lease_time
    
    def _generate_pool(self, start, end):
        start_parts = list(map(int, start.split('.')))
        end_parts = list(map(int, end.split('.')))
        pool = []
        for i in range(start_parts[3], end_parts[3] + 1):
            pool.append(f"{start_parts[0]}.{start_parts[1]}.{start_parts[2]}.{i}")
        return pool
    
    def request_lease(self, mac_address):
        if mac_address in self.leases:
            lease = self.leases[mac_address]
            return f"RENEW: {mac_address} keeps {lease['ip']}"
        
        if not self.pool:
            return f"DECLINE: No IPs available for {mac_address}"
        
        ip = self.pool.pop(0)
        self.leases[mac_address] = {"ip": ip, "expiry": self.lease_time}
        return f"OFFER: {mac_address} -> {ip} (lease: {self.lease_time}s)"
    
    def release_lease(self, mac_address):
        if mac_address in self.leases:
            ip = self.leases[mac_address]["ip"]
            self.pool.append(ip)
            del self.leases[mac_address]
            return f"RELEASED: {ip} from {mac_address}"
        return f"No lease found for {mac_address}"
    
    def show_leases(self):
        return self.leases

# Simulate
dhcp = DHCPServer("192.168.1.0/24", "192.168.1.100", "192.168.1.110")
print(dhcp.request_lease("AA:BB:CC:11:22:33"))
print(dhcp.request_lease("AA:BB:CC:44:55:66"))
print(dhcp.request_lease("AA:BB:CC:11:22:33"))  # Renew
print("\nActive Leases:", dhcp.show_leases())
print(dhcp.release_lease("AA:BB:CC:11:22:33"))
print("\nActive Leases after release:", dhcp.show_leases())
```

---

### Lesson 8.2 - Networking Services: What is DNS?

**Key Concepts:**
- DNS hierarchy: Root -> TLD -> Domain -> Subdomain
- DNS record types: A, AAAA, CNAME, MX, TXT, NS, SOA
- DNS resolution process (recursive vs. iterative)
- Caching and TTL (Time To Live)
- DNSSEC for security
- Common DNS issues and troubleshooting

**Vocabulary:**
| Term | Definition |
|------|------------|
| **DNS** | Domain Name System; translates human-readable names to IP addresses |
| **TLD** | Top-Level Domain; .com, .org, .net, .edu |
| **A Record** | Maps domain to IPv4 address |
| **AAAA Record** | Maps domain to IPv6 address |
| **CNAME** | Canonical Name; alias pointing to another domain |
| **MX Record** | Mail Exchange; specifies mail servers |
| **TTL** | Time To Live; how long a DNS record is cached |
| **DNSSEC** | DNS Security Extensions; adds cryptographic validation |

**DNS Resolution Flow:**
```
User types: www.example.com
    |
Browser checks local cache
    |
OS resolver checks hosts file & cache
    |
Recursive DNS resolver (ISP/Google/Cloudflare)
    |
Root Server (.) -> TLD Server (.com)
    |
Authoritative Server (example.com)
    |
Returns IP: 93.184.216.34
```

**Code Sample - DNS Resolver Simulator:**
```python
# module8_dns_resolver.py
class DNSResolver:
    def __init__(self):
        self.root_servers = ["a.root-servers.net", "b.root-servers.net"]
        self.tld_servers = {
            ".com": "a.gtld-servers.net",
            ".org": "a0.org.afilias-nst.info",
            ".net": "a.gtld-servers.net"
        }
        self.authoritative_zones = {
            "example.com": {
                "A": "93.184.216.34",
                "AAAA": "2606:2800:220:1:248:1893:25c8:1946",
                "MX": "mail.example.com",
                "TXT": "v=spf1 include:_spf.example.com ~all",
                "CNAME": None,
                "TTL": 300
            },
            "google.com": {
                "A": "142.250.185.78",
                "AAAA": "2607:f8b0:4004:c06::64",
                "MX": "aspmx.l.google.com",
                "TXT": "v=spf1 include:_spf.google.com ~all",
                "CNAME": None,
                "TTL": 600
            }
        }
        self.cache = {}
    
    def resolve(self, domain, record_type="A"):
        print(f"\nResolving {domain} ({record_type})")
        
        cache_key = f"{domain}:{record_type}"
        if cache_key in self.cache:
            print(f"  Cache HIT: {self.cache[cache_key]}")
            return self.cache[cache_key]
        
        print(f"  Querying Root Server: {self.root_servers[0]}")
        
        tld = '.' + domain.split('.')[-1]
        tld_server = self.tld_servers.get(tld, "unknown")
        print(f"  Querying TLD Server ({tld}): {tld_server}")
        
        zone = self.authoritative_zones.get(domain)
        if not zone:
            print(f"  NXDOMAIN: {domain} not found")
            return None
        
        result = zone.get(record_type)
        if result:
            self.cache[cache_key] = result
            print(f"  Resolved: {domain} -> {result} (TTL: {zone['TTL']}s)")
        else:
            print(f"  No {record_type} record for {domain}")
        
        return result
    
    def show_cache(self):
        print("\nDNS Cache:")
        for key, value in self.cache.items():
            print(f"  {key} -> {value}")

# Example
resolver = DNSResolver()
resolver.resolve("example.com", "A")
resolver.resolve("example.com", "MX")
resolver.resolve("google.com", "A")
resolver.resolve("example.com", "A")  # Cache hit
resolver.show_cache()
```

---

## Appendix A: Glossary of All Terms

| Term | Definition | Module |
|------|------------|--------|
| ACL | Access Control List | 7 |
| A Record | DNS record mapping domain to IPv4 | 8 |
| ARP | Address Resolution Protocol | 6 |
| Authentication | Verifying user identity | 7 |
| Authorization | Granting access rights | 7 |
| Bandwidth | Maximum data transfer rate | 4 |
| BGP | Border Gateway Protocol | 6 |
| Binary | Base-2 number system | 1 |
| Bit | Smallest data unit (0 or 1) | 1 |
| Byte | 8 bits | 1 |
| CIDR | Classless Inter-Domain Routing | 6 |
| CNAME | Canonical Name (DNS alias) | 8 |
| CPU | Central Processing Unit | 1 |
| Daemon | Background process | 3 |
| DHCP | Dynamic Host Configuration Protocol | 8 |
| DNS | Domain Name System | 4, 8 |
| DNSSEC | DNS Security Extensions | 8 |
| FCR | First Call Resolution | 5 |
| Firewall | Network traffic filter | 8 |
| GPU | Graphics Processing Unit | 1 |
| GPT | GUID Partition Table | 3 |
| HTTP/HTTPS | HyperText Transfer Protocol | 4 |
| ICMP | Internet Control Message Protocol | 6 |
| IP Address | Network device identifier | 4, 6 |
| IPv4 | 32-bit IP addressing | 6 |
| IPv6 | 128-bit IP addressing | 6 |
| Kernel | Core OS component | 3 |
| LAN | Local Area Network | 6 |
| Latency | Network delay | 4 |
| Load Balancer | Traffic distributor | 8 |
| MAC Address | Hardware network address | 6 |
| MDM | Mobile Device Management | 2 |
| MBR | Master Boot Record | 3 |
| MX Record | Mail Exchange record | 8 |
| NAT | Network Address Translation | 6, 8 |
| NTFS | Windows filesystem | 7 |
| OSI Model | 7-layer networking model | 6 |
| OSPF | Open Shortest Path First | 6 |
| Packet | Network data unit | 4 |
| POST | Power-On Self Test | 2 |
| Process | Running program instance | 3 |
| Proxy | Intermediary server | 8 |
| RAID | Redundant Array of Independent Disks | 7 |
| RAM | Random Access Memory | 1 |
| Router | Packet-forwarding device | 4 |
| Shell | Command-line interface | 3 |
| SLA | Service Level Agreement | 1 |
| Subnet Mask | IP network/host divider | 6 |
| sudo | Linux superuser command | 7 |
| TCP/IP | Core internet protocol suite | 4 |
| TTL | Time To Live | 8 |
| UAC | User Account Control | 7 |
| UEFI | Unified Extensible Firmware Interface | 2, 3 |
| VPN | Virtual Private Network | 8 |
| WAN | Wide Area Network | 6 |

---

## Appendix B: 8 Python Execution Files

Each module above corresponds to a runnable Python file:

| File | Module | Topics |
|------|--------|--------|
| `module1_ticket_system.py` | 1 | Ticket class, binary converter, system info |
| `module2_build_validator.py` | 2 | PC build validation, mobile device management |
| `module3_os_simulator.py` | 3 | Process scheduler, OS installer compatibility |
| `module4_network_simulator.py` | 4 | Packet routing, package manager |
| `module5_customer_service.py` | 5 | Interaction logger, troubleshooting tree, skill tracker |
| `module6_network_topology.py` | 6 | Network topology, IP calculator |
| `module7_raid_calculator.py` | 7 | RAID calculator, permission manager |
| `module8_dhcp_simulator.py` | 8 | DHCP lease simulator, DNS resolver |

**Run any module:**
```bash
python module1_ticket_system.py
python module6_network_topology.py
```

---

## Appendix C: Exercises

### Exercise 1: Binary Challenge
Convert your name to binary and back using the `text_to_binary()` function.

### Exercise 2: Build Your Dream PC
Use the `PCBuilder` class to configure a workstation with at least 32GB RAM and RTX 4070.

### Exercise 3: OSI Model Quiz
Match these protocols to their OSI layers: HTTP, TCP, IP, Ethernet, SSL.

### Exercise 4: Subnetting Practice
Given `10.0.0.0/16`, how many subnets of `/24` can you create? How many hosts per subnet?

### Exercise 5: Permission Scenarios
A file has permissions `755`. Can a group member write to it? What about others?

### Exercise 6: DNS Troubleshooting
A user can't reach `www.example.com`. Walk through the DNS resolution steps to diagnose.

### Exercise 7: RAID Planning
Design a storage array for 10TB usable space with 2-drive fault tolerance. Which RAID level and how many drives?

### Exercise 8: Customer Service Roleplay
Write a dialogue handling a user whose email won't send. Use the 6-step framework.

---

## Appendix D: References

1. **Google IT Support Certificate** - Coursera / Google Career Certificates
2. **CompTIA A+ Certification** - Core 1 (220-1101) & Core 2 (220-1102)
3. **CompTIA Network+** - N10-008
4. **TCP/IP Illustrated** - W. Richard Stevens
5. **The Linux Command Line** - William Shotts
6. **Windows Internals** - Mark Russinovich
7. **RFC 1035** - Domain Names Implementation and Specification
8. **RFC 791** - Internet Protocol (IPv4)
9. **RFC 2460** - Internet Protocol, Version 6 (IPv6)
10. **Google Cloud Networking Documentation** - cloud.google.com/docs

---

*Generated for the Google IT Support Certificate curriculum. Each module is self-contained and runnable as a standalone Python script.*
