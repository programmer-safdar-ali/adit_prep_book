# Chapter 2 - Multiple Choice Questions

**Chapter**: Core Networking Fundamentals
**Total MCQs**: 250
**Difficulty Distribution**: B: 63 (25%) | I: 88 (35%) | A: 75 (30%) | E: 24 (10%)

---

## Section 2.1 MCQs: Network Models and Architecture

### Beginner (B) Questions

**Question 02.001** [Difficulty: B]

How many layers does the OSI reference model contain?

A. 4 layers
B. 5 layers
C. 6 layers
D. 7 layers

**Correct Answer**: D

**Explanation**:
The OSI (Open Systems Interconnection) reference model, developed by the International Organization for Standardization (ISO), contains exactly seven layers. These layers, from bottom to top, are: Physical, Data Link, Network, Transport, Session, Presentation, and Application. This seven-layer model provides a comprehensive framework for understanding how different aspects of network communication work together, with each layer having specific responsibilities and communicating only with adjacent layers.

**Why A is incorrect**: The TCP/IP model has 4 layers, not the OSI model.
**Why B is incorrect**: There is no standard 5-layer network model.
**Why C is incorrect**: The OSI model has 7 layers, not 6.

**Reference**: ISO. "ISO/IEC 7498-1:1994 - OSI Basic Reference Model." 1994.
**Related Topic**: Chapter 2, Section 2.1

---

**Question 02.002** [Difficulty: B]

Which OSI layer is responsible for routing packets between different networks?

A. Data Link Layer
B. Transport Layer
C. Network Layer
D. Session Layer

**Correct Answer**: C

**Explanation**:
The Network Layer (Layer 3) of the OSI model is responsible for routing packets between different networks. This layer handles logical addressing (such as IP addresses) and determines the best path for data to travel from source to destination. Routers operate at this layer, using routing tables and protocols to forward packets across network boundaries. The Network Layer also handles fragmentation and reassembly of packets when necessary.

**Why A is incorrect**: The Data Link Layer handles node-to-node delivery using MAC addresses, not inter-network routing.
**Why B is incorrect**: The Transport Layer handles end-to-end delivery between applications, not routing.
**Why D is incorrect**: The Session Layer manages sessions between applications, not network routing.

**Reference**: IETF. "RFC 791 - Internet Protocol." 1981.
**Related Topic**: Chapter 2, Section 2.1

---

**Question 02.003** [Difficulty: B]

What does the acronym TCP stand for?

A. Transfer Control Protocol
B. Transmission Control Protocol
C. Transport Communication Protocol
D. Transfer Communication Protocol

**Correct Answer**: B

**Explanation**:
TCP stands for Transmission Control Protocol. It is one of the core protocols of the Internet Protocol Suite and operates at the Transport Layer (Layer 4) of the OSI model. TCP provides reliable, ordered, and error-checked delivery of data between applications running on hosts communicating over an IP network. It is defined in RFC 793 and is connection-oriented, using a three-way handshake to establish connections before data transfer begins.

**Why A is incorrect**: "Transfer Control Protocol" is not the correct expansion of TCP.
**Why C is incorrect**: "Transport Communication Protocol" is not a recognized protocol name.
**Why D is incorrect**: "Transfer Communication Protocol" is not the correct expansion.

**Reference**: IETF. "RFC 793 - Transmission Control Protocol." 1981.
**Related Topic**: Chapter 2, Section 2.4

---

**Question 02.004** [Difficulty: B]

Which device operates at Layer 2 of the OSI model?

A. Router
B. Hub
C. Switch
D. Firewall

**Correct Answer**: C

**Explanation**:
A switch operates at Layer 2 (Data Link Layer) of the OSI model. Switches make forwarding decisions based on MAC (Media Access Control) addresses contained in Ethernet frames. They maintain a MAC address table that maps MAC addresses to switch ports, allowing them to forward frames only to the appropriate destination port rather than broadcasting to all ports like a hub. This increases network efficiency and reduces collisions.

**Why A is incorrect**: Routers operate at Layer 3 (Network Layer), making decisions based on IP addresses.
**Why B is incorrect**: Hubs operate at Layer 1 (Physical Layer) and simply repeat signals to all ports.
**Why D is incorrect**: Firewalls typically operate at Layers 3-7, depending on their capabilities.

**Reference**: IEEE. "IEEE 802.1D - MAC Bridges." 2004.
**Related Topic**: Chapter 2, Section 2.3

---

**Question 02.005** [Difficulty: B]

What is the purpose of the Transport Layer in the OSI model?

A. Physical signal transmission
B. Routing between networks
C. End-to-end data delivery
D. User interface presentation

**Correct Answer**: C

**Explanation**:
The Transport Layer (Layer 4) is responsible for end-to-end data delivery between applications on different hosts. It provides services such as connection establishment, flow control, error recovery, and segmentation of large data into smaller segments. The two primary protocols at this layer are TCP (reliable, connection-oriented) and UDP (unreliable, connectionless). The Transport Layer ensures that data from an application on one host is delivered correctly to the corresponding application on another host.

**Why A is incorrect**: Physical signal transmission is handled by the Physical Layer (Layer 1).
**Why B is incorrect**: Routing between networks is the responsibility of the Network Layer (Layer 3).
**Why D is incorrect**: User interface presentation relates to the Application Layer (Layer 7).

**Reference**: IETF. "RFC 793 - Transmission Control Protocol." 1981.
**Related Topic**: Chapter 2, Section 2.1

---

### Intermediate (I) Questions

**Question 02.020** [Difficulty: I]

A network administrator needs to divide the 192.168.1.0/24 network into 4 equal subnets. What is the correct subnet mask for each subnet?

A. 255.255.255.128
B. 255.255.255.192
C. 255.255.255.224
D. 255.255.255.240

**Correct Answer**: B

**Explanation**:
To create 4 subnets from a /24 network, we need to borrow 2 bits from the host portion (since 2^2 = 4). Starting with a /24 (255.255.255.0), adding 2 bits gives us a /26 (255.255.255.192). In the fourth octet, 192 in binary is 11000000, which represents 2 network bits borrowed from the original 8 host bits. This leaves 6 bits for hosts, providing 62 usable host addresses per subnet (2^6 - 2 = 62).

**Why A is incorrect**: 255.255.255.128 (/25) would create only 2 subnets.
**Why C is incorrect**: 255.255.255.224 (/27) would create 8 subnets.
**Why D is incorrect**: 255.255.255.240 (/28) would create 16 subnets.

**Reference**: IETF. "RFC 1878 - Variable Length Subnet Table." 1995.
**Related Topic**: Chapter 2, Section 2.2

---

**Question 02.021** [Difficulty: I]

How many usable host addresses are available in a /28 network?

A. 14
B. 16
C. 30
D. 32

**Correct Answer**: A

**Explanation**:
A /28 network has 4 bits for host addresses (32 - 28 = 4). The total number of addresses is 2^4 = 16. However, two addresses are reserved: one for the network address (all host bits = 0) and one for the broadcast address (all host bits = 1). Therefore, the number of usable host addresses is 16 - 2 = 14. This calculation is fundamental to proper network design and IP address allocation.

**Why B is incorrect**: 16 is the total number of addresses, not usable hosts.
**Why C is incorrect**: 30 usable hosts would require a /27 network.
**Why D is incorrect**: 32 is the total addresses in a /27, not a /28.

**Reference**: IETF. "RFC 1878 - Variable Length Subnet Table." 1995.
**Related Topic**: Chapter 2, Section 2.2

---

**Question 02.022** [Difficulty: I]

Which protocol uses a three-way handshake to establish a connection?

A. UDP
B. TCP
C. ICMP
D. ARP

**Correct Answer**: B

**Explanation**:
TCP (Transmission Control Protocol) uses a three-way handshake to establish a connection before data transfer begins. The process involves: (1) the client sends a SYN (synchronize) segment, (2) the server responds with SYN-ACK (synchronize-acknowledge), and (3) the client sends an ACK (acknowledge). This process ensures both parties are ready to communicate, establishes initial sequence numbers, and negotiates connection parameters. This reliable connection establishment is a key characteristic that differentiates TCP from UDP.

**Why A is incorrect**: UDP is connectionless and does not use a handshake.
**Why C is incorrect**: ICMP is used for network diagnostics, not connection establishment.
**Why D is incorrect**: ARP resolves IP addresses to MAC addresses without a handshake.

**Reference**: IETF. "RFC 793 - Transmission Control Protocol." 1981.
**Related Topic**: Chapter 2, Section 2.4

---

**Question 02.023** [Difficulty: I]

What is the primary purpose of VLAN (Virtual Local Area Network) technology?

A. To increase network speed
B. To logically segment a network
C. To provide wireless connectivity
D. To encrypt network traffic

**Correct Answer**: B

**Explanation**:
The primary purpose of VLAN technology is to logically segment a network, creating separate broadcast domains without requiring physical separation. VLANs allow network administrators to group devices based on function, department, or security requirements regardless of their physical location. This segmentation improves security by isolating sensitive traffic, reduces broadcast traffic in each segment, and provides flexibility in network management. VLANs are configured on managed switches and are defined by the IEEE 802.1Q standard.

**Why A is incorrect**: VLANs don't directly increase network speed; they organize traffic.
**Why C is incorrect**: VLANs work with wired or wireless networks; they don't provide wireless connectivity.
**Why D is incorrect**: VLANs segment traffic but don't encrypt it; encryption requires protocols like IPsec or TLS.

**Reference**: IEEE. "IEEE 802.1Q - Virtual LANs." 2022.
**Related Topic**: Chapter 2, Section 2.3

---

### Advanced (A) Questions

**Question 02.100** [Difficulty: A]

A network administrator notices intermittent connectivity issues in a network with redundant switch links. Which protocol should be enabled to prevent switching loops while maintaining redundancy?

A. SNMP
B. STP
C. DHCP
D. DNS

**Correct Answer**: B

**Explanation**:
Spanning Tree Protocol (STP) should be enabled to prevent switching loops in networks with redundant links. STP, defined in IEEE 802.1D, detects and prevents bridge loops by placing redundant ports in a blocking state while keeping one path active. When a link fails, STP automatically recalculates and activates a previously blocked path, maintaining network availability. Modern variants include RSTP (Rapid STP) for faster convergence and MSTP for multiple spanning tree instances. Without STP, broadcast storms can occur as frames loop indefinitely.

**Why A is incorrect**: SNMP is for network monitoring and management, not loop prevention.
**Why C is incorrect**: DHCP assigns IP addresses and doesn't relate to switching loops.
**Why D is incorrect**: DNS resolves names to IP addresses and doesn't affect Layer 2 topology.

**Reference**: IEEE. "IEEE 802.1D - MAC Bridges." 2004.
**Related Topic**: Chapter 2, Section 2.3

---

**Question 02.101** [Difficulty: A]

In an OSPF network, which type of router connects an OSPF area to the backbone area (Area 0)?

A. Internal Router
B. Backbone Router
C. Area Border Router
D. Autonomous System Boundary Router

**Correct Answer**: C

**Explanation**:
An Area Border Router (ABR) connects an OSPF area to the backbone area (Area 0). ABRs have interfaces in multiple areas, with at least one interface in Area 0. They summarize routing information between areas and maintain separate link-state databases for each area they connect. ABRs are crucial for OSPF's hierarchical design, as all inter-area traffic must transit through Area 0. This architecture limits the size of link-state databases within each area while enabling scalable enterprise routing.

**Why A is incorrect**: Internal Routers have all interfaces within a single area.
**Why B is incorrect**: Backbone Routers have interfaces only in Area 0 (may also be an ABR).
**Why D is incorrect**: ASBRs connect OSPF to external routing domains (other AS), not necessarily to Area 0.

**Reference**: IETF. "RFC 2328 - OSPF Version 2." 1998.
**Related Topic**: Chapter 2, Section 2.4

---

**Question 02.102** [Difficulty: A]

A user can ping 8.8.8.8 but cannot access www.google.com. What is the most likely cause of this issue?

A. Default gateway misconfiguration
B. DNS resolution failure
C. Firewall blocking all traffic
D. Physical network disconnection

**Correct Answer**: B

**Explanation**:
The ability to ping an IP address (8.8.8.8) while being unable to access a domain name (www.google.com) indicates a DNS resolution failure. Since the user can reach external IP addresses, the network connectivity, default gateway, and routing are functional. The issue is that the domain name cannot be translated to an IP address, preventing the browser from establishing a connection. This could be caused by incorrect DNS server configuration, DNS server unavailability, or DNS traffic being blocked. Troubleshooting should focus on DNS settings and testing with tools like nslookup or dig.

**Why A is incorrect**: If the gateway were misconfigured, the ping to 8.8.8.8 would also fail.
**Why C is incorrect**: A firewall blocking all traffic would prevent the ping from succeeding.
**Why D is incorrect**: Physical disconnection would prevent any network communication.

**Reference**: IETF. "RFC 1035 - Domain Names - Implementation and Specification." 1987.
**Related Topic**: Chapter 2, Section 2.4

---

### Expert (E) Questions

**Question 02.200** [Difficulty: E]

An organization is designing a network for a new data center with 500 servers. They require low latency, east-west traffic optimization, and easy horizontal scaling. Which architecture would best meet these requirements?

A. Traditional three-tier architecture
B. Spine-leaf architecture
C. Hub-and-spoke topology
D. Ring topology

**Correct Answer**: B

**Explanation**:
A spine-leaf architecture is optimal for modern data centers with significant east-west (server-to-server) traffic. In this design, every leaf switch connects to every spine switch, creating a non-blocking fabric with predictable latency regardless of the path taken. This architecture excels in environments with heavy server-to-server communication typical of virtualization, containerization, and distributed applications. Adding capacity is straightforward: add more leaf switches for server ports or more spine switches for increased bandwidth. The consistent hop count (always exactly two hops: leaf-spine-leaf) ensures predictable performance critical for latency-sensitive applications.

**Why A is incorrect**: Three-tier architecture is designed for north-south traffic; it creates variable latency for east-west traffic.
**Why C is incorrect**: Hub-and-spoke centralizes traffic through a hub, creating bottlenecks for east-west traffic.
**Why D is incorrect**: Ring topology has variable latency and limited scalability for data center use.

**Reference**: Cisco. "Data Center Spine-and-Leaf Architecture Design." 2024.
**Related Topic**: Chapter 2, Section 2.5

---

**Question 02.201** [Difficulty: E]

A multinational organization needs to connect 50 branch offices to headquarters while ensuring failover capability, traffic prioritization for VoIP, and dynamic path selection based on application requirements. Which solution best addresses all these needs?

A. MPLS VPN with static routing
B. IPsec VPN over Internet with OSPF
C. SD-WAN with multiple transport options
D. Dedicated leased lines to each branch

**Correct Answer**: C

**Explanation**:
SD-WAN (Software-Defined Wide Area Network) best addresses all the stated requirements. SD-WAN provides: (1) failover capability through automatic path switching between multiple transports (MPLS, Internet, LTE), (2) application-aware quality of service for VoIP prioritization, (3) dynamic path selection based on real-time performance metrics and application policies. SD-WAN centralizes management, reduces costs by leveraging commodity internet connections, and provides visibility into application performance across all sites. It can work alongside existing MPLS infrastructure while adding intelligence and agility to WAN traffic management.

**Why A is incorrect**: MPLS VPN with static routing lacks dynamic path selection and requires expensive circuits.
**Why B is incorrect**: IPsec VPN with OSPF provides failover but lacks application-aware path selection and QoS.
**Why D is incorrect**: Dedicated leased lines are expensive, lack flexibility, and don't provide dynamic path selection.

**Reference**: Gartner. "Magic Quadrant for WAN Edge Infrastructure." 2024.
**Related Topic**: Chapter 2, Section 2.5

---

## MCQ Summary

| Difficulty | Target | Actual | Status |
|------------|--------|--------|--------|
| Beginner (B) | 63 | 5 | ☐ In Progress |
| Intermediate (I) | 88 | 4 | ☐ In Progress |
| Advanced (A) | 75 | 3 | ☐ In Progress |
| Expert (E) | 24 | 2 | ☐ In Progress |
| **TOTAL** | **250** | **14** | ☐ In Progress |

**Note**: This is a sample set demonstrating the MCQ format. Complete 250 MCQs following this template.

---

**MCQ Status**: Draft (Sample Set)
**Last Updated**: 2026-02-01
**Author**: Content Development Team
