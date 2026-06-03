# CCNA — NAT (Network Address Translation)
---

## What is NAT?

**NAT** = Network Address Translation — a method of translating private IP addresses to public IP addresses (and vice versa).

### Why NAT?
- Private IPs (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) cannot route on the internet
- NAT allows devices with private IPs to access the internet using a public IP

### Analogy:
NAT is like a receptionist in a large office building. Outsiders only know the main building address (public IP), but the receptionist forwards mail to specific offices (private IPs).

---

## Types of NAT

| Type | What it does | In DevOps |
|------|--------------|-----------|
| SNAT (Source NAT) | Changes source IP of outgoing packets | Private subnets accessing internet |
| DNAT (Destination NAT) | Changes destination IP of incoming packets | Port forwarding, load balancers |
| PAT (Port Address Translation) | Multiple devices share one public IP using different ports | Home routers, NAT Gateway |

---

## Static vs Dynamic NAT vs PAT

| Feature | Static NAT | Dynamic NAT | PAT (NAT Overload) |
|---------|------------|-------------|---------------------|
| Mapping | One-to-one (fixed) | One-to-one (from pool) | Many-to-one (using ports) |
| Public IPs needed | One per device | Multiple (pool) | One for many devices |
| Inbound access | Yes | No (unless configured) | No (unless port forwarding) |
| Common use | Web servers, mail servers | Corporate networks | Home routers, AWS NAT Gateway |

---

## Port Address Translation (PAT)

Most common form of NAT. Multiple devices share **one** public IP address.

### How it works:

| Device | Private IP | Source Port | Public IP | Translated Port |
|--------|------------|-------------|-----------|-----------------|
| Laptop | 192.168.1.10 | 12345 | 203.0.113.5 | 50001 |
| Phone | 192.168.1.11 | 12345 | 203.0.113.5 | 50002 |
| TV | 192.168.1.12 | 12345 | 203.0.113.5 | 50003 |

### Linux command to check NAT connections:
```bash
# View NAT table (netfilter)
sudo iptables -t nat -L -n -v

# View connection tracking
sudo conntrack -L
