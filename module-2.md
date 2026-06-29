# CCNA — Application Layer Protocols (HTTP, HTTPS, FTP, SSH )  - Ports

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

# Port Numbers

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
