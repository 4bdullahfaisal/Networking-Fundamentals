# CCNA — VPNs (Virtual Private Networks) 
---

## What is a VPN?

VPN = Virtual Private Network — creates a secure, encrypted connection over a less secure network (like the internet).

**Analogy:** VPN is like a private tunnel through a public city — no one can see what's inside your tunnel.

---

## Why Use a VPN?

| Reason | Explanation |
|--------|-------------|
| Security | Encrypts data between two points |
| Privacy | Hides your IP address |
| Remote Access | Connect to office/cloud network from anywhere |
| Bypass restrictions | Access region-locked content |

---

## Types of VPNs

| Type | What it does | Use Case |
|------|--------------|----------|
| Site-to-Site VPN | Connects entire networks (office → cloud) | AWS VPN to on-premises data center |
| Remote Access VPN | Connects single device to a network | Employee working from home |
| Client VPN | Software on laptop/phone | OpenVPN, WireGuard |
| SSL VPN | Uses web browser (HTTPS) | No client software needed |

---

## VPN Protocols

| Protocol | Port | Speed | Security | Use Case |
|----------|------|-------|----------|----------|
| IPsec | UDP 500, 4500 | Fast | High | Site-to-Site VPN |
| OpenVPN | UDP 1194 | Moderate | High | Remote access |
| WireGuard | UDP 51820 | Very Fast | High | Modern VPN |
| L2TP/IPsec | UDP 1701 | Moderate | Moderate | Legacy |
| PPTP | TCP 1723 | Fast | Low | Deprecated (insecure) |
| SSL/TLS | TCP 443 | Moderate | High | Browser-based VPN |

---

### Architecture Example:
```
On-Premises Data Center
        │
        │ (IPsec VPN)
        ▼
AWS Site-to-Site VPN
        │
        ▼
AWS VPC (10.0.0.0/16)
```

---

## VPN vs Proxy vs TOR

| Feature | VPN | Proxy | TOR |
|---------|-----|-------|-----|
| Encryption | Full traffic | Application only | Multi-layer |
| Speed | Fast | Fast | Slow |
| Anonymity | Moderate | Low | High |
| Use case | Security + privacy | Content bypass | Extreme anonymity |

---

## VPN Terminology

| Term | Definition |
|------|------------|
| Tunnel | Encrypted connection between two points |
| Encapsulation | Wrapping original packet inside another packet |
| Split Tunneling | Only certain traffic goes through VPN |
| Full Tunnel | All traffic goes through VPN |
| VPN Gateway | Device/software that terminates VPN connections |
| IKE (Internet Key Exchange) | Protocol for setting up IPsec tunnels |
| Pre-shared Key (PSK) | Shared password for VPN authentication |

---

## Basic VPN Commands (Linux)

```bash
# Check VPN connections
ipsec status
systemctl status ipsec

# OpenVPN connection (client)
sudo openvpn --config client.ovpn

# WireGuard
sudo wg show
sudo wg-quick up wg0

# Check VPN interface
ip a show tun0
ip a show wg0

# Routing through VPN
ip route show table all | grep tun0
```

---
