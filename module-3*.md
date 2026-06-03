# CCNA - Firewalls & Security Groups
---

## What is a Firewall?

A firewall monitors and filters incoming/outgoing network traffic based on security rules.

**Analogy:** Firewall is like a security guard at a building entrance — checks who comes in and out.

---

## Types of Firewalls

| Type | What it does | Where used |
|------|--------------|------------|
| Packet Filtering | Inspects headers (IP, port, protocol) | Routers, basic firewalls |
| Stateful Inspection | Tracks connection state | Enterprise firewalls |
| Application Layer | Inspects actual data (HTTP, FTP, etc.) | Next-gen firewalls (NGFW) |
| Proxy Firewall | Intermediary between client and server | Security gateways |

---

## Firewall Rules Components

| Component | What it means | Example |
|-----------|---------------|---------|
| Source IP | Where traffic comes from | 192.168.1.0/24 |
| Destination IP | Where traffic goes to | 10.0.0.5 |
| Port | Which service | 22 (SSH), 80 (HTTP), 443 (HTTPS) |
| Protocol | TCP, UDP, ICMP | TCP |
| Action | Allow or Deny | ACCEPT, DROP, REJECT |

---

## Firewall Rule Actions

| Action | What it does |
|--------|--------------|
| ACCEPT | Allows traffic through |
| DROP | Silently discards traffic (no response) |
| REJECT | Discards and sends error response |

---

## Types of Firewalls by Location

| Type | Location | Purpose |
|------|----------|---------|
| Network Firewall | Between networks | Protects entire network |
| Host-based Firewall | On individual devices | Protects single device |
| Perimeter Firewall | Network edge | Internal vs internet |
| Internal Firewall | Between network segments | Segments internal traffic |

---

## Firewall Zones

Zones are predefined sets of rules for different trust levels.

| Zone | Trust Level | Typical Use |
|------|-------------|-------------|
| trusted | Highest | Internal servers |
| home | High | Home network |
| work | Medium | Office network |
| public | Low | Public Wi-Fi |
| dmz | Medium | Web servers |
| block | None | Blocked traffic |
| drop | None | Dropped traffic |

---

## Common Firewall Ports to Know

| Port | Service | Direction | Protocol |
|------|---------|-----------|----------|
| 22 | SSH | Inbound | TCP |
| 80 | HTTP | Inbound | TCP |
| 443 | HTTPS | Inbound | TCP |
| 25 | SMTP | Outbound | TCP |
| 53 | DNS | Outbound | UDP/TCP |
| 123 | NTP | Outbound | UDP |
| 3306 | MySQL | Inbound | TCP |
| 5432 | PostgreSQL | Inbound | TCP |

---

## Firewall Rule Order

Firewall rules are processed in order — first match wins.

| Order | Rule | Action |
|-------|------|--------|
| 1 | Allow SSH from office IP (10.0.0.5) | ACCEPT |
| 2 | Allow HTTP from anywhere | ACCEPT |
| 3 | Drop everything else | DROP |

### Best Practice:
- Specific rules first
- General rules later
- Default deny at the end

---

## Security Groups (Network Concept)

Security Groups are firewall rules applied to a group of devices.

| Feature | Explanation |
|---------|-------------|
| Stateful | If inbound allowed, response auto-allowed |
| Stateless | Inbound and outbound rules evaluated separately |
| Default deny | All traffic blocked unless explicitly allowed |

### Security Group Rule Example

| Direction | Source | Port | Action |
|-----------|--------|------|--------|
| Inbound | 192.168.1.0/24 | 22 (TCP) | ALLOW |
| Inbound | 0.0.0.0/0 | 80 (TCP) | ALLOW |
| Inbound | 0.0.0.0/0 | 443 (TCP) | ALLOW |
| Outbound | 0.0.0.0/0 | All | ALLOW |

---

## Firewall vs Router vs Switch (Security Role)

| Device | Security Role |
|--------|---------------|
| Router | Basic ACLs (packet filtering) |
| Firewall | Advanced filtering, stateful inspection |
| Switch | VLAN segmentation (port isolation) |

---

## Firewall Commands (Linux Quick Reference)

```bash
# Allow HTTP (port 80)
sudo firewall-cmd --add-service=http --permanent

# Allow SSH (port 22)
sudo firewall-cmd --add-service=ssh --permanent

# Allow custom port
sudo firewall-cmd --add-port=8080/tcp --permanent

# Reload to apply
sudo firewall-cmd --reload
