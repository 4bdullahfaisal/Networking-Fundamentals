# CCNA — DNS & DHCP

---

## DNS (Domain Name System)

DNS translates human-readable domain names (google.com) to IP addresses (142.250.190.46).

**Analogy:** DNS is like a phonebook for the internet.

---

## How DNS Works

| Step | What happens |
|------|--------------|
| 1 | You type `google.com` in browser |
| 2 | Computer checks local DNS cache |
| 3 | If not found, queries DNS resolver (ISP or 8.8.8.8) |
| 4 | Resolver queries Root DNS server |
| 5 | Root directs to TLD server (.com) |
| 6 | TLD directs to Authoritative DNS server (Google's) |
| 7 | Authoritative server returns IP address |
| 8 | Browser connects to that IP |

---

## Types of DNS Servers

| Type | What it does |
|------|--------------|
| DNS Resolver | Receives query from client, does the lookup |
| Root Server | Top of hierarchy, directs to TLD servers |
| TLD Server | Manages .com, .org, .net, etc. |
| Authoritative Server | Has actual DNS records for a domain |

---

## DNS Record Types (DevOps Must Know)

| Record | What it does | Example |
|--------|--------------|---------|
| A | Domain → IPv4 | google.com → 142.250.190.46 |
| AAAA | Domain → IPv6 | google.com → 2001:4860:4860::8888 |
| CNAME | Domain → another domain | www.example.com → example.com |
| MX | Mail exchange | Mail → mail.google.com |
| TXT | Text information | SPF, DKIM, verification |
| NS | Name server | ns1.google.com |
| PTR | IP → domain (reverse lookup) | 46.190.250.142 → google.com |

---

## Common DNS Tools (Linux)

```bash
# Query DNS records
nslookup google.com
nslookup google.com 8.8.8.8

# Dig (more detailed)
dig google.com
dig google.com A
dig google.com CNAME
dig -x 8.8.8.8  # Reverse lookup

# Host command
host google.com

# Show local DNS cache
systemd-resolve --statistics

# Clear local DNS cache
sudo systemd-resolve --flush-caches
```

---

## DHCP (Dynamic Host Configuration Protocol)

DHCP automatically assigns IP addresses to devices on a network.

**Analogy:** DHCP is like a hotel front desk — you arrive, they give you a room number (IP address).

---

## How DHCP Works (DORA Process)

| Step | Name | What happens |
|------|------|--------------|
| 1 | Discover | Client broadcasts "I need an IP" |
| 2 | Offer | DHCP server offers an IP address |
| 3 | Request | Client requests the offered IP |
| 4 | Acknowledge | Server confirms the assignment |

---

## DHCP Lease Components

| Component | Meaning |
|-----------|---------|
| IP Address | The assigned IP |
| Subnet Mask | Network size |
| Default Gateway | Router IP (to reach other networks) |
| DNS Server | DNS resolver IP |
| Lease Time | How long IP is valid |

---

## DHCP vs Static IP

| Feature | DHCP | Static IP |
|---------|------|-----------|
| Configuration | Automatic | Manual |
| IP assignment | Server assigns | Admin configures |
| Changing IP | Can change | Fixed |
| Best for | Clients, desktops, phones | Servers, routers |
| Management | Centralized | Per device |
| In AWS | Default for all subnets | Elastic IP for EC2 |

---

## DNS vs DHCP — Comparison

| Feature | DNS | DHCP |
|---------|-----|------|
| Purpose | Name → IP resolution | Automatic IP assignment |
| Port | 53 (TCP/UDP) | 67 (server), 68 (client) |
| Direction | Client queries server | Server offers to client |
| Configuration | Manual or automatic | Automatic |
| DevOps relevance | Web apps, service discovery | VPC networking, EC2 IP |

---

## Linux DHCP Commands

```bash
# Release DHCP lease
sudo dhclient -r eth0

# Renew DHCP lease
sudo dhclient eth0

# Check DHCP lease info
cat /var/lib/dhcp/dhclient.leases

# View current IP (assigned by DHCP)
ip a show eth0

# Restart network with DHCP
sudo systemctl restart NetworkManager
```
---

## Quick Revision Table

| Term | Definition |
|------|------------|
| DNS | Translates domain names to IP addresses |
| A Record | Domain → IPv4 |
| CNAME | Domain → another domain |
| nslookup/dig | DNS query tools |
| DHCP | Automatically assigns IP addresses |
| DORA | Discover, Offer, Request, Acknowledge |
| Lease Time | Duration of IP assignment |
| AWS DHCP Options Set | Custom DNS configuration for VPC |

---
