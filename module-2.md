# CCNA - Application Layer Protocols (HTTP, HTTPS, FTP, SSH )  - Ports - Firewalls and Security Groups 

---

## HTTP (Hypertext Transfer Protocol)

HTTP is the foundation of data communication on the web.

| Feature | Details |
|---------|---------|
| Port | 80 |
| Protocol | TCP |
| Security | None (plain text) |
| Use case | Regular websites (not secure) |

### HTTP Methods

| Method | What it does | Example |
|--------|--------------|---------|
| GET | Retrieve data | Visiting a webpage |
| POST | Submit data | Form submission |
| PUT | Update/replace resource | API update |
| DELETE | Remove resource | Delete an entry |
| PATCH | Partial update | Modify part of resource |

---

## HTTPS (HTTP Secure)

HTTPS = HTTP + SSL/TLS encryption.

| Feature | Details |
|---------|---------|
| Port | 443 |
| Protocol | TCP |
| Security | Encrypted (SSL/TLS) |
| Use case | Banking, login pages, APIs, production apps |

### How HTTPS Works

| Step | What happens |
|------|--------------|
| 1 | Client requests HTTPS connection |
| 2 | Server sends SSL/TLS certificate |
| 3 | Client verifies certificate |
| 4 | Session keys are exchanged |
| 5 | Encrypted communication begins |

---

## FTP (File Transfer Protocol)

FTP transfers files between client and server.

| Feature | Details |
|---------|---------|
| Ports | 20 (data), 21 (control) |
| Protocol | TCP |
| Security | None (plain text credentials) |
| Use case | Uploading website files (legacy) |

### FTP Modes

| Mode | How it works | Use case |
|------|--------------|----------|
| Active | Server connects to client | Old networks |
| Passive | Client connects to server | Modern networks (firewall friendly) |

### Secure FTP Alternatives

| Protocol | Port | Security | Use case |
|----------|------|----------|----------|
| SFTP (SSH File Transfer) | 22 | SSH encrypted | Most common for secure transfers |
| FTPS (FTP over SSL) | 990 | SSL/TLS | Legacy secure FTP |
| SCP | 22 | SSH encrypted | Quick file copies |

---

## SSH (Secure Shell)

SSH provides secure remote access to servers.

| Feature | Details |
|---------|---------|
| Port | 22 |
| Protocol | TCP |
| Security | Strong encryption |
| Use case | Remote server administration, Git, file transfers |

### Common SSH Commands

```bash
# Connect to remote server
ssh user@hostname

# Copy file via SCP
scp local.txt user@hostname:/remote/path/

# Copy directory
scp -r folder/ user@hostname:/remote/path/

# Generate SSH key pair
ssh-keygen -t rsa -b 4096

# Copy public key to server
ssh-copy-id user@hostname
```

---

## Protocol Comparison Table

| Protocol | Port | Security | Transport | Use Case |
|----------|------|----------|-----------|----------|
| HTTP | 80 | None | TCP | Regular web |
| HTTPS | 443 | SSL/TLS | TCP | Secure web |
| FTP | 20,21 | None | TCP | File transfer (old) |
| SFTP | 22 | SSH | TCP | Secure file transfer |
| SCP | 22 | SSH | TCP | Quick secure copy |
| SSH | 22 | Strong | TCP | Remote access |

---

## DevOps Relevance

| Protocol | Where you use it in DevOps |
|----------|---------------------------|
| HTTP/HTTPS | Web apps, API endpoints, load balancers |
| SSH | Access EC2 instances, Git push, Ansible |
| SFTP/SCP | Transfer logs, configs, artifacts |

---

## Linux Commands for Testing

```bash
# Test HTTP connection
curl http://example.com
curl -I http://example.com

# Test HTTPS connection
curl https://example.com
curl -I https://example.com

# Check SSL certificate
openssl s_client -connect google.com:443 -servername google.com

# Test SSH connection
ssh -v user@hostname

# Test FTP connection
ftp hostname
```

---

# - Port Numbers

A port is like a door number on a server. Different services listen on different ports.

### Well-Known Ports (0-1023) — Must Know for DevOps

| Port | Protocol | Service | DevOps Use |
|------|----------|---------|-------------|
| 22 | TCP | SSH | Remote server access |
| 80 | TCP | HTTP | Unencrypted web traffic |
| 443 | TCP | HTTPS | Encrypted web traffic |
| 53 | TCP/UDP | DNS | Domain name resolution |
| 25 | TCP | SMTP | Email sending |
| 3306 | TCP | MySQL | Database connection |
| 5432 | TCP | PostgreSQL | Database connection |
| 27017 | TCP | MongoDB | Database connection |
| 8080 | TCP | Alternative HTTP | Proxy, testing |
| 8443 | TCP | Alternative HTTPS | Secure proxy |

### DevOps Scenario Examples

| Scenario | Protocol | Port |
|----------|----------|------|
| SSH into a server | TCP | 22 |
| Open a website | TCP | 80 or 443 |
| App connects to MySQL | TCP | 3306 |
| Ping a server | ICMP | N/A |
| DNS query | UDP | 53 |

---

# - Firewalls & Security Groups
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
