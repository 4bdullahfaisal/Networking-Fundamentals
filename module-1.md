# CCNA — Network Essentials
---
## What is a Network?

A **network** = two or more devices connected together to share data.

**Examples:**
- Your laptop connected to Wi-Fi
- Servers in a data center
- Cloud VPC (Virtual Private Cloud)

---

## Network Topologies

Topology = how devices are physically or logically connected.

| Topology | How it looks | Pros | Cons |
|----------|--------------|------|------|
| Bus | One cable, all devices connected | Cheap | If cable breaks, whole network down |
| Star | Devices connected to central switch | Easy to troubleshoot | Switch failure = network down |
| Ring | Devices in a circle | Predictable | One break breaks the ring |
| Mesh | Every device connected to every other | Very reliable | Expensive |
| Hybrid | Combination of topologies | Flexible | Complex to manage |

**Most common in DevOps/Cloud:** Star and Hybrid

---

## Network Devices (Routers & Switches)

| Device | What it does | DevOps relevance |
|--------|--------------|------------------|
| Switch | Connects devices within the same network (LAN) | Connects servers in a data center |
| Router | Connects different networks together | AWS VPC uses route tables (like routers) |
| Firewall | Filters traffic based on rules | Security groups, NACLs |
| Load Balancer | Distributes traffic across servers | AWS ALB, NLB |

**Simple way to remember:**
- **Switch** = connects devices inside your house
- **Router** = connects your house to the outside world

---

## Cable Types

| Cable Type | Used for | Speed | Example |
|------------|----------|-------|---------|
| Coaxial | Old TV/internet | Slow | Cable modem |
| Twisted Pair (Ethernet) | Office/home networks | 100 Mbps - 10 Gbps | Cat5e, Cat6 |
| Fiber Optic | Long distance, high speed | 1 Gbps - 100 Gbps | Data centers |
| Console Cable | Configure routers/switches | Slow | Initial device setup |

**In DevOps:** You'll rarely touch physical cables, but know Ethernet (standard for servers) and Fiber (high-speed).

---

## Key Networking Terms

| Term | Meaning |
|------|---------|
| LAN | Local Area Network (your office/home) |
| WAN | Wide Area Network (internet, connects LANs) |
| Bandwidth | Maximum data transfer rate |
| Latency | Delay in data transfer |
| Collision Domain | Where two devices can interfere |
| Broadcast Domain | Where a broadcast message reaches |

---

## Characteristics of a Network

A good network has 4 main characteristics:

| Characteristic | Meaning | DevOps Example |
|----------------|---------|----------------|
| Fault Tolerance | Network keeps working even if something fails | AWS Availability Zones (AZs) |
| Scalability | Can grow without breaking | Adding more servers to a VPC subnet |
| Quality of Service (QoS) | Prioritizes important traffic | Giving priority to SSH over file downloads |
| Security | Protects data from unauthorized access | Firewalls, encryption, VPNs, IAM |

**Memory trick:** FSQS (Fault Tolerance, Scalability, QoS, Security)

---

## OSI Model (7 Layers)

OSI = Open Systems Interconnection

| Layer | Name | What it does | DevOps Example |
|-------|------|--------------|----------------|
| 7 | Application | User interacts with app | HTTP, HTTPS, SSH, DNS |
| 6 | Presentation | Data format, encryption | SSL/TLS, JPEG |
| 5 | Session | Manages connection between apps | API sessions |
| 4 | Transport | Reliable data delivery | TCP, UDP |
| 3 | Network | Routing between networks | IP addressing, route tables |
| 2 | Data Link | Communication between adjacent devices | MAC addresses, switches |
| 1 | Physical | Raw bits over cable | Ethernet, fiber optics |

### Memory Trick (Bottom to Top):
**P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way
- Physical, Data Link, Network, Transport, Session, Presentation, Application

### DevOps Focus Layers:
- Layer 7: Configure web servers (Nginx/Apache), APIs
- Layer 4: Open ports (TCP 22 for SSH, TCP 443 for HTTPS)
- Layer 3: Assign IPs, configure VPC route tables

---

## TCP/IP Protocol Suite

TCP/IP is the actual protocol used on the internet.

| Layer | TCP/IP Model | Protocols | DevOps Relevance |
|-------|--------------|-----------|------------------|
| 4 | Application | HTTP, HTTPS, SSH, DNS, SMTP | Web servers, APIs |
| 3 | Transport | TCP, UDP | Ports, reliability |
| 2 | Internet | IP (IPv4, IPv6), ICMP | IP addresses, routing |
| 1 | Network Access | Ethernet, Wi-Fi | Physical cables |

---

## TCP vs UDP

| Feature | TCP | UDP |
|---------|-----|-----|
| Connection | Requires handshake (3-way) | No connection |
| Reliability | Guaranteed delivery | Best effort |
| Order | Preserves order | No order guarantee |
| Speed | Slower | Faster |
| Use cases | SSH, HTTP, HTTPS, databases | DNS, streaming, VoIP |

**Analogy:**
- TCP = Certified mail (you get confirmation)
- UDP = Regular mail (you hope it arrives)

### TCP 3-Way Handshake
1. Client → Server: SYN (I want to connect)
2. Server → Client: SYN-ACK (OK, let's connect)
3. Client → Server: ACK (Connected!)

---
