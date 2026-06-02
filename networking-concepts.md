# CCNA — VLANs, Trunks, STP, Network Security & Troubleshooting

---

## VLAN (Virtual Local Area Network)

**VLAN** = divides a physical network into multiple logical networks.

### Why VLANs?
- Security (isolate traffic)
- Reduce broadcast traffic
- Organize devices by function
- Better performance

### Analogy:
A physical building divided into separate rooms — each room is a VLAN. People in different rooms can't hear each other's conversations.

### VLAN Ranges:
| Range | Type | Use |
|-------|------|-----|
| 1 | Default VLAN | Cannot be deleted |
| 2-1001 | Normal VLANs | User traffic |
| 1002-1005 | Reserved | Token Ring/FDDI |
| 1006-4094 | Extended VLANs | Large networks |

---

## Trunk Ports

**Trunk** = a port that carries traffic for **multiple VLANs** (unlike access ports which carry one VLAN).

### Access Port vs Trunk Port:

| Feature | Access Port | Trunk Port |
|---------|-------------|------------|
| VLANs carried | 1 VLAN | Multiple VLANs |
| Tagging | No tag | Adds 802.1Q tag |
| Use case | End devices (PC, server) | Switch to switch, switch to router |

### Tagging Protocol: **802.1Q (dot1q)**
- Adds VLAN ID to each Ethernet frame
- Standard for VLAN tagging across different vendors

### Native VLAN:
- Untagged traffic on trunk port
- Default is VLAN 1

---

## STP (Spanning Tree Protocol)

**STP** = prevents network loops in redundant network designs.

### Why STP?
- Without STP, loops cause broadcast storms
- Broadcast storms crash networks
- STP blocks redundant ports until needed

### How STP Works:
1. Elects a **Root Bridge** (lowest bridge ID)
2. Each switch determines **Root Port** (best path to root)
3. **Designated Ports** forward traffic
4. **Alternate Ports** are blocked (no forwarding)

### STP Port States:

| State | Forward Traffic? | Learn MAC? | Time |
|-------|-----------------|------------|------|
| Blocking | No | No | 20 sec |
| Listening | No | No | 15 sec |
| Learning | No | Yes | 15 sec |
| Forwarding | Yes | Yes | Steady state |
| Disabled | No | No | Admin down |

### STP Types:
| Protocol | Standard | Speed |
|----------|----------|-------|
| STP (802.1D) | Original | Slow (50 sec convergence) |
| RSTP (802.1w) | Rapid | Fast (few seconds) |
| MSTP (802.1s) | Multiple instances | Fast |

---

## Network Security Basics

### Security Layers:

| Layer | Security Method | In DevOps |
|-------|-----------------|-----------|
| Physical | Locks, cameras, biometrics | Data center security (AWS handles) |
| Network | Firewall, ACL, VPN | Security Groups, NACLs |
| Transport | TLS, IPsec | HTTPS, VPN |
| Application | Authentication, authorization | IAM, Cognito |

### Common Security Methods:

| Method | What it does | In DevOps |
|--------|--------------|-----------|
| Firewall | Filters traffic based on rules | Security Groups, NACLs |
| ACL (Access Control List) | Rules for allowed/denied traffic | Network ACLs in AWS |
| Port Security | Limits MAC addresses on a port | Rare in cloud |
| DHCP Snooping | Prevents rogue DHCP servers | Rare in cloud |
| Dynamic ARP Inspection | Prevents ARP spoofing | Rare in cloud |
| VPN (IPsec) | Encrypted tunnel over internet | AWS VPN, Direct Connect |
| TLS/SSL | Encrypts application data | HTTPS (port 443) |

### Firewall Types:

| Type | Stateless/Stateful | Example |
|------|-------------------|---------|
| Packet filtering | Stateless | Standard ACLs |
| Stateful inspection | Stateful | AWS Security Groups |
| Next-Gen Firewall | Stateful + Application | AWS Network Firewall |

### AWS Security Layers:

| Layer | AWS Service | Stateful/Stateless |
|-------|-------------|-------------------|
| Instance firewall | Security Groups | Stateful |
| Subnet firewall | Network ACLs | Stateless |
| DDoS protection | AWS Shield | Automatic |
| Web app firewall | AWS WAF | Application layer |
| Encryption in transit | TLS, VPN | - |
| Encryption at rest | EBS, S3 encryption | - |

### Security Best Practices:

1. **Least privilege** — only allow necessary traffic
2. **Defense in depth** — multiple security layers
3. **Log everything** — CloudTrail, VPC Flow Logs
4. **Regular audits** — review security groups, NACLs
5. **Use HTTPS** — encrypt web traffic
6. **Disable root SSH** — use key pairs

---

## Network Troubleshooting

### Troubleshooting Methodology:

| Step | Action |
|------|--------|
| 1 | Identify the problem |
| 2 | Establish theory of cause |
| 3 | Test theory |
| 4 | Establish action plan |
| 5 | Implement solution |
| 6 | Verify full functionality |
| 7 | Document findings |
