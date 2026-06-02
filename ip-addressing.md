# CCNA Day 2 — IP Addressing, Subnetting & IPV6

---

## IPv4 Addressing

An **IP address** is a unique identifier for a device on a network.

### IPv4 Address Structure

IPv4 addresses are **32 bits** long, written as **4 decimal numbers** (0-255) separated by dots.

**Example:** `192.168.1.10`

| Format | Example |
|--------|---------|
| Binary | `11000000.10101000.00000001.00001010` |
| Decimal | `192.168.1.10` |

### Two Parts of an IP Address

| Part | Purpose | Example (192.168.1.10) |
|------|---------|------------------------|
| Network Part | Identifies the network | `192.168.1` |
| Host Part | Identifies the specific device | `.10` |

The **Subnet Mask** tells you where the network part ends.

---

## Subnet Mask

A subnet mask defines which part of the IP is network vs host.

| CIDR | Subnet Mask | Network Bits | Host Bits | Total IPs |
|------|-------------|--------------|-----------|-----------|
| /8 | 255.0.0.0 | 8 | 24 | 16,777,216 |
| /16 | 255.255.0.0 | 16 | 16 | 65,536 |
| /24 | 255.255.255.0 | 24 | 8 | 256 |
| /25 | 255.255.255.128 | 25 | 7 | 128 |
| /26 | 255.255.255.192 | 26 | 6 | 64 |
| /27 | 255.255.255.224 | 27 | 5 | 32 |
| /28 | 255.255.255.240 | 28 | 4 | 16 |
| /29 | 255.255.255.248 | 29 | 3 | 8 |
| /30 | 255.255.255.252 | 30 | 2 | 4 |

**Most common in DevOps:** `/24` (256 IPs), `/16` (65,536 IPs)

---

## IP Address Classes (Traditional)

| Class | Start Range | Subnet Mask | Use |
|-------|-------------|-------------|-----|
| A | 1-126 | 255.0.0.0 (/8) | Large organizations |
| B | 128-191 | 255.255.0.0 (/16) | Medium organizations |
| C | 192-223 | 255.255.255.0 (/24) | Small networks |
| D | 224-239 | N/A | Multicast |
| E | 240-255 | N/A | Experimental |

**Note:** Classes are old — modern networking uses CIDR.

---

## Public vs Private IP Addresses

### Private IP Addresses (Not routable on internet)

| Range | CIDR | How many IPs | Use |
|-------|------|--------------|-----|
| 10.0.0.0 - 10.255.255.255 | 10.0.0.0/8 | 16,777,216 | Large internal networks |
| 172.16.0.0 - 172.31.255.255 | 172.16.0.0/12 | 1,048,576 | Medium internal networks |
| 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 | 65,536 | Home/small office |

### Public IP Addresses
- Everything else
- Routable on the internet
- Must be unique globally

### Special Addresses

| Address | Purpose |
|---------|---------|
| 127.0.0.1 | Localhost (your own computer) |
| 0.0.0.0 | All interfaces (listen on all IPs) |
| 255.255.255.255 | Broadcast (send to everyone on network) |

---

## Subnetting Basics

**Subnetting** = dividing a large network into smaller networks.

**Why subnet?**
- Reduce network traffic
- Improve security
- Efficient use of IP addresses

### Binary Quick Reference

| Decimal | Binary |
|---------|--------|
| 128 | 10000000 |
| 192 | 11000000 |
| 224 | 11100000 |
| 240 | 11110000 |
| 248 | 11111000 |
| 252 | 11111100 |
| 254 | 11111110 |
| 255 | 11111111 |

### Subnet Masks in Binary

| CIDR | Subnet Mask | Binary |
|------|-------------|--------|
| /24 | 255.255.255.0 | 11111111.11111111.11111111.00000000 |
| /25 | 255.255.255.128 | 11111111.11111111.11111111.10000000 |
| /26 | 255.255.255.192 | 11111111.11111111.11111111.11000000 |
| /27 | 255.255.255.224 | 11111111.11111111.11111111.11100000 |
| /28 | 255.255.255.240 | 11111111.11111111.11111111.11110000 |

### How Many Hosts Per Subnet?

Formula: `2^(Host bits) - 2`

**Subtract 2 for:**
- Network address (all host bits = 0)
- Broadcast address (all host bits = 1)

| CIDR | Host Bits | Formula | Usable Hosts | Common Use |
|------|-----------|---------|--------------|-------------|
| /24 | 8 | 2^8 - 2 | 254 | Small office, public subnet |
| /25 | 7 | 2^7 - 2 | 126 | Half subnet |
| /26 | 6 | 2^6 - 2 | 62 | Quarter subnet |
| /27 | 5 | 2^5 - 2 | 30 | Small subnet |
| /28 | 4 | 2^4 - 2 | 14 | Very small subnet |
| /29 | 3 | 2^3 - 2 | 6 | AWS NAT Gateway |
| /30 | 2 | 2^2 - 2 | 2 | Point-to-point links |

### Network vs Broadcast Addresses

**Example:** `192.168.1.0/24`

| Address Type | Value | Use |
|--------------|-------|-----|
| Network Address | 192.168.1.0 | Identifies the subnet (cannot assign) |
| First usable | 192.168.1.1 | Assign to first device |
| Last usable | 192.168.1.254 | Assign to last device |
| Broadcast Address | 192.168.1.255 | Send to all devices (cannot assign) |

---

## IPv6 Basics

### Why IPv6?

| Feature | IPv4 | IPv6 |
|---------|------|------|
| Address size | 32 bits | 128 bits |
| Address format | Decimal | Hexadecimal |
| Number of addresses | 4.3 billion | 340 undecillion |
| Subnet notation | /24, /16, /8 | /64, /48, /32 |
| NAT | Commonly used | Not needed |
| Security | Optional | Built-in |
| Broadcast | Yes | No (uses multicast) |

### IPv6 Address Format

128 bits written as **8 groups of 4 hexadecimal digits**.

**Example:** `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

**Shortening rules:**
1. Leading zeros can be omitted
2. Consecutive zeros replaced with `::` (only once)

| Original | Shortened |
|----------|-----------|
| `2001:0db8:0000:0000:0000:0000:0000:0001` | `2001:db8::1` |
| `fe80:0000:0000:0000:0000:0000:0000:0001` | `fe80::1` |

### IPv6 Address Types

| Type | Starts With | Purpose | Example |
|------|-------------|---------|---------|
| Global Unicast | 2000::/3 | Public internet address | `2001:db8::1` |
| Link-Local | fe80::/10 | Automatic, within same subnet | `fe80::1` |
| Unique Local | fc00::/7 | Private (like IPv4 private) | `fd00::1` |
| Multicast | ff00::/8 | One-to-many communication | `ff02::1` |
| Loopback | ::1 | Localhost (like 127.0.0.1) | `::1` |

---
