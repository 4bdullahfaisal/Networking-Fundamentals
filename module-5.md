# CCNA — Routing
---

## What is Routing?

**Routing** = the process of moving data packets from one network to another.

**Analogy:** Routing is like a GPS for data — it decides which path to take to reach the destination.

---

## Router vs Switch

| Device | Function | In DevOps |
|--------|----------|-----------|
| Switch | Moves data within the same network (LAN) | Connects servers inside a subnet |
| Router | Moves data between different networks | Connects subnets to each other or to internet |

---

## Routing Table

Every router has a **routing table** — a list of rules that tell it where to send traffic.

**Example routing table:**

| Destination | Next Hop | Interface |
|-------------|----------|-----------|
| 10.0.0.0/24 | directly connected | eth0 |
| 192.168.1.0/24 | 10.0.0.1 | eth0 |
| 0.0.0.0/0 (default) | 203.0.113.1 | eth1 |

**Default route (`0.0.0.0/0`)** = "if no other rule matches, send traffic here" (usually to internet gateway)

---

## Types of Routing

| Type | How it works | Pros | Cons |
|------|--------------|------|------|
| Static Routing | Manually configured by admin | Simple, secure, no overhead | Doesn't adapt to failures |
| Dynamic Routing | Routers automatically learn routes | Adapts to network changes | Complex, more overhead |

---

## Static Routing

Admins manually add routes to routing tables.

**Example (Linux command):**

```bash
# Add static route to 192.168.5.0 network via gateway 10.0.0.1
ip route add 192.168.5.0/24 via 10.0.0.1

# Add default gateway
ip route add default via 10.0.0.1
```

### When to use static routing:
- Small networks
- Simple setups (home, small office)
- Stub networks (only one way in/out)
- **AWS route tables** (you manually add routes!)

---

## Dynamic Routing

Routers automatically learn routes from each other using **routing protocols**.

### Common Dynamic Routing Protocols:

| Protocol | What it does | Where used |
|----------|--------------|------------|
| RIP | Old, simple, limited to 15 hops | Legacy networks |
| OSPF | Fast, scalable, industry standard | Enterprise networks, data centers |
| EIGRP | Cisco proprietary | Cisco-only networks |
| BGP | Internet routing | Between ISPs, cloud providers |

### When to use dynamic routing:
- Large networks
- Networks with redundant paths
- Networks that change frequently
- **AWS Direct Connect** (uses BGP)

---

## Private vs Public Routing

| Type | Where it routes | In DevOps |
|------|----------------|-----------|
| Private Routing | Inside your VPC, between subnets | Route tables in AWS VPC |
| Public Routing | To/from the internet | Internet Gateway, NAT Gateway |

---

## Default Route (0.0.0.0/0)

The **default route** is a catch-all route for any traffic that doesn't match a more specific route.

| Destination | Target | Meaning |
|-------------|--------|---------|
| 0.0.0.0/0 | Internet Gateway | Send all internet traffic to IGW |
| 0.0.0.0/0 | NAT Gateway | Send internet traffic via NAT (private subnet) |
| 0.0.0.0/0 | Virtual Private Gateway | Send to VPN or Direct Connect |

**In AWS:** Without a default route to IGW, a subnet cannot reach the internet.

---

## Static vs Dynamic Routing — Comparison

| Feature | Static Routing | Dynamic Routing |
|---------|----------------|-----------------|
| Setup | Manual | Automatic |
| Adapts to failures | No | Yes |
| Network overhead | None | Some (protocol messages) |
| Security | More secure | Less secure |
| Scalability | Poor (large networks) | Excellent |
| Use case | Small networks, VPC route tables | Large networks, data centers, BGP |

---


## Linux Routing Commands

```bash
# Show routing table
ip route
route -n

# Add static route
ip route add 192.168.5.0/24 via 10.0.0.1

# Add default gateway
ip route add default via 10.0.0.1

# Delete route
ip route del 192.168.5.0/24

# Show ARP table
ip neigh
```

---

## Quick Reference

| Term | Definition |
|------|------------|
| Routing | Moving data between networks |
| Routing table | Set of rules for where to send traffic |
| Default route (0.0.0.0/0) | Catch-all route for unknown destinations |
| Static routing | Manual routes (used in AWS VPC) |
| Dynamic routing | Automatic routes using protocols (OSPF, BGP) |
| Internet Gateway | Connects VPC to internet |
| NAT Gateway | Allows private subnets to access internet |
| Local route | Route that keeps traffic inside VPC |

---

