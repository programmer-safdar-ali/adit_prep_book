# Chapter 2: Core Networking Fundamentals

---

## Chapter Overview

- **Domain**: Networking and Communications
- **Estimated Study Time**: 5-6 hours
- **Prerequisites**: Chapter 1 (Introduction to IT for Public Service), Basic computer literacy
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Define** the OSI and TCP/IP models and **explain** each layer's function and associated protocols (B)
2. **Calculate** IPv4 subnet masks, network addresses, and usable host ranges for network design scenarios (I)
3. **Analyze** network traffic patterns to **troubleshoot** connectivity issues and identify protocol behavior (A)
4. **Design** a multi-site enterprise network architecture that meets organizational security and performance requirements (E)
5. **Identify** common network devices and **describe** their roles in enterprise infrastructure (B)
6. **Implement** VLAN segmentation and inter-VLAN routing configurations (I)
7. **Differentiate** between routing protocols and **evaluate** their suitability for different network scenarios (A)

---

## Introduction

Networking forms the backbone of modern IT infrastructure and is essential knowledge for any Assistant Director IT position. In today's interconnected government and enterprise environments, understanding how data flows between systems, how networks are designed and secured, and how to troubleshoot connectivity issues is fundamental to effective IT leadership.

As an Assistant Director IT, you will be responsible for overseeing network infrastructure, evaluating technology proposals from vendors, coordinating with network administrators, and making strategic decisions about network architecture. This chapter provides the foundational knowledge required to fulfill these responsibilities effectively.

This chapter builds upon the basic IT concepts introduced in Chapter 1 and establishes the networking fundamentals that will be referenced throughout subsequent chapters on security (Chapter 3), cloud computing (Chapter 9), and cybersecurity (Chapter 10). By mastering these concepts, you will be better equipped to understand complex IT systems and lead technology initiatives in your organization.

---

## Section 2.1: Network Models and Architecture (B)

Understanding network models is fundamental to grasping how data communication works. The two primary models used to conceptualize network communications are the OSI (Open Systems Interconnection) model and the TCP/IP model.

### 2.1.1 The OSI Reference Model

The OSI model, developed by the International Organization for Standardization (ISO), provides a conceptual framework for understanding network communications. It divides network communication into seven distinct layers, each with specific responsibilities.

**The Seven Layers of the OSI Model:**

| Layer | Name | Function | Example Protocols/Devices |
|-------|------|----------|--------------------------|
| 7 | Application | User interface and network services | HTTP, FTP, SMTP, DNS |
| 6 | Presentation | Data formatting, encryption, compression | SSL/TLS, JPEG, ASCII |
| 5 | Session | Session management and control | NetBIOS, RPC |
| 4 | Transport | End-to-end delivery, error recovery | TCP, UDP |
| 3 | Network | Logical addressing and routing | IP, ICMP, Routers |
| 2 | Data Link | Physical addressing, framing | Ethernet, MAC, Switches |
| 1 | Physical | Bit transmission over media | Cables, Hubs, NICs |

Each layer communicates only with adjacent layers, creating a modular design that allows changes at one layer without affecting others.

### Practical Example 2.1: Understanding Data Encapsulation

**Scenario**: When you access a government web portal, your browser initiates an HTTP request. Here's how data travels through the OSI layers:

1. **Application Layer**: Your browser generates an HTTP GET request for the webpage
2. **Presentation Layer**: The data is formatted and may be encrypted (HTTPS)
3. **Session Layer**: A session is established with the web server
4. **Transport Layer**: TCP segments the data and adds port numbers (source and destination port 443 for HTTPS)
5. **Network Layer**: IP adds source and destination IP addresses, creating packets
6. **Data Link Layer**: Ethernet framing adds MAC addresses, creating frames
7. **Physical Layer**: Frames are converted to electrical/optical signals for transmission

At the receiving end, this process reverses (de-encapsulation).

### 2.1.2 The TCP/IP Model

The TCP/IP model, also known as the Internet Protocol Suite, is the practical model used on the Internet and most modern networks. It consolidates the OSI model into four layers:

| TCP/IP Layer | Corresponding OSI Layers | Primary Protocols |
|--------------|-------------------------|-------------------|
| Application | Application, Presentation, Session | HTTP, DNS, SMTP, FTP |
| Transport | Transport | TCP, UDP |
| Internet | Network | IP, ICMP, ARP |
| Network Access | Data Link, Physical | Ethernet, Wi-Fi |

### 2.1.3 Comparing OSI and TCP/IP Models

While the OSI model provides an excellent conceptual framework for learning, the TCP/IP model reflects real-world implementation. Key differences include:

- **OSI**: Seven layers, theoretical, developed by ISO
- **TCP/IP**: Four layers, practical, developed by DoD

Understanding both models is essential for the ADIT examination and practical network administration.

### Practical Example 2.2: Identifying Protocol Layers

**Scenario**: A network administrator needs to troubleshoot a user's email issue.

- If the user cannot resolve the mail server's hostname → **DNS issue (Application/Internet Layer)**
- If DNS works but connection times out → **TCP issue (Transport Layer)**
- If TCP connects but authentication fails → **Application Layer (SMTP)**
- If the user cannot reach any network resources → **Check Physical Layer (cables, NICs)**

This layered approach to troubleshooting helps isolate problems efficiently.

---

## Section 2.2: IP Addressing and Subnetting (I)

IP addressing is the foundation of network communication. Every device on an IP network requires a unique address to send and receive data. This section covers IPv4 addressing, subnet masks, and subnetting calculations.

### 2.2.1 IPv4 Address Structure

An IPv4 address is a 32-bit number represented in dotted decimal notation (four octets separated by periods).

**Example**: 192.168.1.100

Each octet ranges from 0 to 255, giving approximately 4.3 billion unique addresses (2^32).

### 2.2.2 IP Address Classes

Traditional IP addressing used five classes:

| Class | First Octet Range | Default Subnet Mask | Networks | Hosts per Network |
|-------|-------------------|---------------------|----------|-------------------|
| A | 1-126 | 255.0.0.0 (/8) | 126 | 16,777,214 |
| B | 128-191 | 255.255.0.0 (/16) | 16,384 | 65,534 |
| C | 192-223 | 255.255.255.0 (/24) | 2,097,152 | 254 |
| D | 224-239 | Multicast | N/A | N/A |
| E | 240-255 | Reserved | N/A | N/A |

**Note**: Class D is used for multicast communications, and Class E is reserved for experimental purposes.

### 2.2.3 Private IP Address Ranges

RFC 1918 defines private IP address ranges that are not routable on the public Internet:

| Class | Private Range | CIDR Notation |
|-------|---------------|---------------|
| A | 10.0.0.0 - 10.255.255.255 | 10.0.0.0/8 |
| B | 172.16.0.0 - 172.31.255.255 | 172.16.0.0/12 |
| C | 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 |

### 2.2.4 Subnet Masks and CIDR Notation

A subnet mask determines which portion of an IP address represents the network and which represents the host. CIDR (Classless Inter-Domain Routing) notation uses a slash followed by the number of network bits.

**Examples**:
- 255.255.255.0 = /24 (24 network bits, 8 host bits)
- 255.255.255.192 = /26 (26 network bits, 6 host bits)

### 2.2.5 Subnetting Calculations

**Step-by-step subnetting process**:

1. **Determine the number of subnets needed**
2. **Calculate subnet bits**: 2^n ≥ required subnets
3. **Calculate new subnet mask**: Add subnet bits to original mask
4. **Calculate hosts per subnet**: 2^(host bits) - 2

### Practical Example 2.3: Subnetting a Class C Network

**Scenario**: Your organization has been assigned 192.168.10.0/24 and needs to create 4 equal subnets for different departments.

**Solution**:

1. **Subnets needed**: 4
2. **Subnet bits required**: 2^2 = 4 ✓
3. **New subnet mask**: /24 + 2 = /26 (255.255.255.192)
4. **Hosts per subnet**: 2^6 - 2 = 62 usable hosts

**Resulting Subnets**:

| Subnet | Network Address | First Host | Last Host | Broadcast |
|--------|-----------------|------------|-----------|-----------|
| 1 | 192.168.10.0 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 |
| 2 | 192.168.10.64 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| 3 | 192.168.10.128 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 |
| 4 | 192.168.10.192 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 |

### Practical Example 2.4: Calculating Hosts for a Given CIDR

**Scenario**: How many usable host addresses are available in a /27 network?

**Solution**:
- Total bits = 32
- Network bits = 27
- Host bits = 32 - 27 = 5
- Total addresses = 2^5 = 32
- Usable hosts = 32 - 2 = 30 (minus network and broadcast addresses)

### 2.2.6 IPv6 Overview

IPv6 uses 128-bit addresses, providing approximately 3.4×10^38 unique addresses. IPv6 addresses are written in hexadecimal, separated by colons.

**Example**: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

Key IPv6 features:
- No need for NAT
- Built-in IPsec support
- Simplified header format
- Auto-configuration (SLAAC)

---

## Section 2.3: Network Devices and Topologies (I)

Understanding network devices and their interconnection patterns (topologies) is essential for designing and managing enterprise networks.

### 2.3.1 Common Network Devices

**Hub** (Layer 1):
- Broadcasts all traffic to all ports
- No intelligence; creates collision domains
- Obsolete in modern networks

**Switch** (Layer 2):
- Forwards frames based on MAC addresses
- Reduces collision domains (each port is a collision domain)
- Maintains MAC address table
- Supports VLANs

**Router** (Layer 3):
- Forwards packets based on IP addresses
- Connects different networks
- Maintains routing tables
- Provides NAT and firewall capabilities

**Multilayer Switch** (Layer 3):
- Combines switch and router functionality
- Performs routing at hardware speeds
- Common in enterprise data centers

**Firewall** (Layer 3-7):
- Controls network traffic based on security policies
- Stateful packet inspection
- Application layer filtering
- Intrusion prevention

### Practical Example 2.5: Selecting the Right Device

**Scenario**: A small government office needs to connect 50 workstations, provide internet access, and segment the network for security.

**Solution**:
- **48-port managed switch**: Connect all workstations, enable VLANs
- **Router/Firewall**: Connect to ISP, provide NAT, enforce security policies
- **Optional Layer 3 switch**: If inter-VLAN routing performance is critical

### 2.3.2 Network Topologies

**Bus Topology**:
- Single backbone cable
- Simple but unreliable
- Single point of failure

**Star Topology**:
- Central device (switch/hub)
- Most common in LANs
- Easy troubleshooting

**Ring Topology**:
- Data flows in one direction
- Token-passing mechanism
- Used in some industrial networks

**Mesh Topology**:
- Every device connects to every other
- Full mesh: Maximum redundancy, expensive
- Partial mesh: Balance of redundancy and cost

**Hybrid Topology**:
- Combination of multiple topologies
- Common in enterprise networks

### Practical Example 2.6: Enterprise Topology Design

**Scenario**: Design a network for a multi-floor office building with 500 users.

**Recommended Approach**:
- **Star topology** on each floor (access layer switches)
- **Partial mesh** between floors (distribution layer)
- **Redundant core** for data center connectivity
- **Result**: Hierarchical three-tier architecture (Access, Distribution, Core)

### 2.3.3 VLANs (Virtual Local Area Networks)

VLANs logically segment a physical network into multiple broadcast domains. Benefits include:

- **Security**: Isolate sensitive systems
- **Performance**: Reduce broadcast traffic
- **Flexibility**: Group users by function, not location

### Practical Example 2.7: VLAN Segmentation

**Scenario**: A government agency needs to separate HR, Finance, and IT departments on the same physical network.

**Solution**:
| VLAN ID | Name | Subnet | Purpose |
|---------|------|--------|---------|
| 10 | HR | 10.1.10.0/24 | Human Resources |
| 20 | Finance | 10.1.20.0/24 | Finance Department |
| 30 | IT | 10.1.30.0/24 | IT Operations |
| 100 | Management | 10.1.100.0/24 | Network Management |

Inter-VLAN routing is performed by a Layer 3 switch or router.

---

## Section 2.4: Network Protocols (A)

Network protocols define the rules for communication between devices. This section covers essential protocols at various layers.

### 2.4.1 Transport Layer Protocols

**TCP (Transmission Control Protocol)**:
- Connection-oriented (three-way handshake)
- Reliable delivery (acknowledgments, retransmission)
- Flow control and congestion control
- Used for: HTTP, FTP, SMTP, SSH

**Three-Way Handshake**:
1. Client → Server: SYN
2. Server → Client: SYN-ACK
3. Client → Server: ACK

**UDP (User Datagram Protocol)**:
- Connectionless
- Best-effort delivery (no guarantees)
- Low overhead, faster
- Used for: DNS, DHCP, VoIP, streaming

### Practical Example 2.8: Choosing TCP vs UDP

**Scenario**: Which protocol would you recommend for each application?

| Application | Recommended Protocol | Reason |
|-------------|---------------------|--------|
| File transfer | TCP | Reliability required |
| Video conferencing | UDP | Real-time, tolerates loss |
| Web browsing | TCP | Reliable page delivery |
| DNS queries | UDP | Quick lookups |
| Database replication | TCP | Data integrity critical |

### 2.4.2 Application Layer Protocols

**DNS (Domain Name System)** - Port 53:
- Resolves domain names to IP addresses
- Hierarchical distributed database
- Uses UDP for queries, TCP for zone transfers

**DHCP (Dynamic Host Configuration Protocol)** - Ports 67/68:
- Automatically assigns IP addresses
- DORA process: Discover, Offer, Request, Acknowledge
- Lease-based allocation

**HTTP/HTTPS** - Ports 80/443:
- Web communication protocol
- HTTPS adds TLS encryption
- Stateless protocol

### Practical Example 2.9: DHCP Troubleshooting

**Scenario**: A user reports "APIPA address" (169.254.x.x) on their workstation.

**Analysis**:
- APIPA indicates DHCP failure
- Client could not reach DHCP server

**Troubleshooting Steps**:
1. Check physical connectivity (cable, switch port)
2. Verify DHCP server is operational
3. Check VLAN configuration (DHCP relay if needed)
4. Review DHCP scope for available addresses

### 2.4.3 Routing Protocols

**Static Routing**:
- Manually configured routes
- Simple, no overhead
- Suitable for small networks

**Dynamic Routing Protocols**:

| Protocol | Type | Algorithm | Metric | Use Case |
|----------|------|-----------|--------|----------|
| RIP | Distance Vector | Bellman-Ford | Hop count | Small networks |
| OSPF | Link State | Dijkstra | Cost (bandwidth) | Enterprise |
| EIGRP | Hybrid | DUAL | Composite | Cisco networks |
| BGP | Path Vector | Path attributes | AS path | Internet routing |

### Practical Example 2.10: Routing Protocol Selection

**Scenario**: A government organization with 50 remote sites needs a routing protocol.

**Analysis**:
- RIP: Not suitable (15 hop limit, slow convergence)
- OSPF: Good choice (scalable, fast convergence, open standard)
- EIGRP: Good if all Cisco equipment
- BGP: Overkill for internal routing

**Recommendation**: OSPF for scalability and vendor independence.

### 2.4.4 Network Address Translation (NAT)

NAT translates private IP addresses to public IP addresses, enabling internet connectivity while conserving IPv4 addresses.

**Types of NAT**:
- **Static NAT**: One-to-one mapping
- **Dynamic NAT**: Pool of public addresses
- **PAT (Port Address Translation)**: Many-to-one using port numbers

---

## Section 2.5: Enterprise Network Design (E)

Designing enterprise networks requires understanding organizational requirements, scalability, security, and high availability.

### 2.5.1 Three-Tier Architecture

The traditional enterprise network design uses three layers:

**Core Layer**:
- High-speed backbone
- Minimal processing, maximum throughput
- Redundant links

**Distribution Layer**:
- Policy enforcement
- Inter-VLAN routing
- QoS implementation
- Aggregation point

**Access Layer**:
- End-user connectivity
- Port security
- VLAN assignment

### 2.5.2 Spine-Leaf Architecture

Modern data centers often use spine-leaf topology:

- **Spine switches**: High-capacity interconnection
- **Leaf switches**: Connect to servers/endpoints
- Every leaf connects to every spine
- Predictable latency, easy scaling

### Practical Example 2.11: Network Design for a New Office

**Scenario**: Design a network for a 200-user government office with the following requirements:
- High availability
- Security segmentation
- VoIP support
- Guest Wi-Fi

**Proposed Design**:

1. **Core**: Redundant Layer 3 switches with HSRP/VRRP
2. **Distribution**: Layer 3 switches for routing between VLANs
3. **Access**: 48-port PoE switches for phones and workstations
4. **Firewall**: Next-generation firewall at internet edge
5. **Wi-Fi**: Enterprise wireless controllers with separate SSID for guests
6. **VLANs**:
   - VLAN 10: Users
   - VLAN 20: VoIP
   - VLAN 30: Servers
   - VLAN 40: Guest Wi-Fi
   - VLAN 100: Management

### 2.5.3 High Availability Considerations

**Link Redundancy**:
- EtherChannel/LACP: Bundle multiple links
- Spanning Tree Protocol: Prevent loops, provide failover

**Device Redundancy**:
- HSRP/VRRP: Virtual gateway redundancy
- Stack configurations: Switch stacking for resilience

**Path Redundancy**:
- Multiple ISP connections
- BGP for automatic failover

### Practical Example 2.12: WAN Design for Multi-Site Organization

**Scenario**: Connect 10 branch offices to headquarters with the following requirements:
- Secure communication
- Failover capability
- Voice quality for IP telephony

**Proposed Solution**:
- **Primary**: MPLS VPN from carrier
- **Backup**: IPsec VPN over Internet
- **Routing**: OSPF over both paths
- **QoS**: Priority queuing for voice traffic
- **SD-WAN**: Consider for dynamic path selection

---

## Hands-on Labs

### Lab 2.1: IPv4 Subnetting Exercise

See [labs/lab-02-01-subnetting.md](labs/lab-02-01-subnetting.md) for complete lab instructions.

**Objective**: Calculate subnet masks, network addresses, and host ranges for various scenarios.

### Lab 2.2: VLAN Configuration

See [labs/lab-02-02-vlans.md](labs/lab-02-02-vlans.md) for complete lab instructions.

**Objective**: Create and configure VLANs, assign ports, and verify connectivity.

### Lab 2.3: Packet Analysis with Wireshark

See [labs/lab-02-03-wireshark.md](labs/lab-02-03-wireshark.md) for complete lab instructions.

**Objective**: Capture and analyze network traffic to identify protocols and troubleshoot issues.

### Lab 2.4: Basic Router Configuration

See [labs/lab-02-04-router-config.md](labs/lab-02-04-router-config.md) for complete lab instructions.

**Objective**: Configure basic router settings including interfaces, routing, and NAT.

### Lab 2.5: Network Troubleshooting

See [labs/lab-02-05-troubleshooting.md](labs/lab-02-05-troubleshooting.md) for complete lab instructions.

**Objective**: Apply systematic troubleshooting methodology to diagnose connectivity issues.

---

## Chapter Summary

Key points covered in this chapter:

- The OSI model provides a seven-layer conceptual framework for understanding network communications, while the TCP/IP model offers a four-layer practical implementation.
- IPv4 addresses are 32-bit numbers organized into classes, with private address ranges defined by RFC 1918 for internal network use.
- Subnetting divides networks into smaller segments, improving security and performance; CIDR notation simplifies subnet mask representation.
- Network devices operate at different OSI layers: hubs (Layer 1), switches (Layer 2), routers (Layer 3), and firewalls (Layers 3-7).
- VLANs provide logical network segmentation without physical rewiring, enhancing security and reducing broadcast domains.
- TCP provides reliable, connection-oriented communication, while UDP offers faster, connectionless delivery for time-sensitive applications.
- Routing protocols (RIP, OSPF, EIGRP, BGP) automate path selection; OSPF is commonly used in enterprise environments.
- Enterprise networks typically use a three-tier architecture (Core, Distribution, Access) for scalability and manageability.
- High availability requires redundancy at multiple levels: links, devices, and paths.

---

## Key Takeaways

1. **The OSI and TCP/IP models are complementary**: Use OSI for learning and troubleshooting methodology; TCP/IP reflects actual protocol implementation on networks.

2. **Subnetting is a critical skill**: The ability to calculate subnet masks, network addresses, and host ranges is essential for network design and frequently tested on IT examinations.

3. **Layer 2 vs Layer 3 decisions impact network design**: Switches (Layer 2) segment collision domains; routers (Layer 3) segment broadcast domains and enable inter-network communication.

4. **Protocol selection depends on application requirements**: TCP for reliability, UDP for speed; understanding this trade-off helps in troubleshooting and design.

5. **Enterprise network design balances performance, security, and availability**: A well-designed network uses hierarchical architecture, proper segmentation, and redundancy to meet organizational needs.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Explain how data encapsulation works as a packet travels from a web browser to a web server**. Include the role of each OSI layer and the headers/trailers added at each step. (B/I)

2. **Given a network address of 10.20.0.0/16, design a subnetting scheme** that provides separate subnets for 5 departments, each requiring at least 1,000 hosts. Show your calculations and list the resulting subnets. (I/A)

3. **Compare and contrast OSPF and BGP routing protocols**. When would you use each, and what are the key advantages and disadvantages of each approach? (A)

4. **As an Assistant Director IT, you are tasked with designing a network for a new government building** with 300 users across 4 floors, including requirements for VoIP, security cameras, and guest Wi-Fi. Describe your proposed architecture, including device selection and VLAN design. (E)

5. **A user reports they can access internal websites but not external websites**. Describe your troubleshooting approach using the OSI model, listing specific commands and checks at each layer. (A/E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 63 Beginner (B) questions (25%)
- 88 Intermediate (I) questions (35%)
- 75 Advanced (A) questions (30%)
- 24 Expert (E) questions (10%)

Total: 250 MCQs

---

## References

- IETF. "RFC 791 - Internet Protocol." 1981. https://tools.ietf.org/html/rfc791
- IETF. "RFC 793 - Transmission Control Protocol." 1981. https://tools.ietf.org/html/rfc793
- IETF. "RFC 1918 - Address Allocation for Private Internets." 1996. https://tools.ietf.org/html/rfc1918
- IETF. "RFC 2328 - OSPF Version 2." 1998. https://tools.ietf.org/html/rfc2328
- ISO. "ISO/IEC 7498-1:1994 - OSI Basic Reference Model." 1994.
- Cisco. "Enterprise Campus 3.0 Architecture." 2025. https://www.cisco.com/c/en/us/solutions/enterprise-networks/enterprise-campus-architecture.html
- IEEE. "IEEE 802.1Q - Virtual LANs." 2022.
- Tanenbaum, Andrew S. "Computer Networks." 6th Edition. 2021.
- Kurose, James F. and Ross, Keith W. "Computer Networking: A Top-Down Approach." 8th Edition. 2020.

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
