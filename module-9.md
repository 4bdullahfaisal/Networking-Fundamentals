# CCNA — Network Troubleshooting Tools

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

---

## Ping (ICMP Echo)

PING (Packet Internet Groper) 
Tests if a host is reachable and measures round-trip time.

```bash
# Basic ping
ping google.com
ping 8.8.8.8

# Ping with count (4 packets)
ping -c 4 google.com

# Ping with interval (0.5 seconds)
ping -i 0.5 google.com

# Ping with packet size
ping -s 1000 google.com
```

### What ping tells you:

| Output | Meaning |
|--------|---------|
| Reply from | Host is reachable |
| Request timeout | Host not responding |
| Destination unreachable | Network problem |
| TTL expired | Routing loop or too many hops |

---

## Traceroute (Path Discovery)

Shows every hop packets take to reach a destination.

```bash
# Basic traceroute
traceroute google.com

# With IP address (skip DNS lookup)
traceroute -n google.com

# Set max hops
traceroute -m 15 google.com

# Use TCP instead of ICMP (firewall friendly)
traceroute -T google.com

# Windows version
tracert google.com
```

### Understanding traceroute output:

| Symbol | Meaning |
|--------|---------|
| `* * *` | No response (firewall or timeout) |
| `ms` | Round trip time in milliseconds |
| `!H` | Host unreachable |
| `!N` | Network unreachable |
| `!P` | Protocol unreachable |

---

## Netstat / ss (Network Statistics)

Shows network connections, routing tables, and listening ports.

### netstat commands:

```bash
# All listening ports
netstat -tulpn

# All active connections
netstat -an

# Show routing table
netstat -rn

# Show interface statistics
netstat -i

# Show PID and program name
netstat -tulpn | grep LISTEN

# Continuous mode (every 5 seconds)
netstat -c

```

### netstat options:

| Option | Meaning |
|--------|---------|
| `-t` | TCP |
| `-u` | UDP |
| `-l` | Listening ports |
| `-p` | Show process PID/name |
| `-n` | Numeric (no DNS) |
| `-a` | All connections |
| `-r` | Routing table |
| `-i` | Interfaces |
| `-s` | Statistics |
| `-c` | Continuous |

---

### ss commands (modern replacement for netstat):

```bash
# All listening ports
ss -tulpn

# All TCP connections
ss -tan

# All UDP connections
ss -uan

# Show processes
ss -tulpn | grep ssh

# Show connections to specific port
ss -tan | grep :80
```

### ss vs netstat:

| Feature | netstat | ss |
|---------|---------|-----|
| Speed | Slower | Faster |
| Installed by default | Older systems | Modern Linux |
| More details | Less | More |

---
## ip (iproute2 tools)

Modern replacement for ifconfig and route.

```bash
# Show IP addresses
ip a
ip addr show

# Show interfaces
ip link show

# Show routing table
ip route show

# Show ARP cache
ip neigh show

# Add IP address
ip addr add 192.168.1.10/24 dev eth0

# Remove IP address
ip addr del 192.168.1.10/24 dev eth0

# Enable interface
ip link set eth0 up

# Disable interface
ip link set eth0 down

# Add static route
ip route add 192.168.5.0/24 via 192.168.1.1

# Delete static route
ip route del 192.168.5.0/24
```

---

## Telnet (Test Port Connectivity)

Tests if a specific port is open and reachable.

```bash
# Test SSH port (22)
telnet google.com 22

# Test HTTP port (80)
telnet google.com 80

# Test HTTPS port (443)
telnet google.com 443

# Test MySQL port (3306)
telnet 10.0.0.5 3306
```

### After connecting to port:

| Port | What you can type |
|------|-------------------|
| 80 | `GET / HTTP/1.1` + `Host: example.com` + `Enter` + `Enter` |
| 22 | Will show SSH banner |
| 25 | `EHLO test.com` (SMTP) |

---

## Netcat (nc) — Swiss Army Knife

A versatile tool for network testing.

```bash
# Test port connectivity
nc -zv google.com 80

# Listen on a port (server mode)
nc -l 1234

# Connect to listening port (client mode)
nc localhost 1234

# Transfer file
nc -l 1234 > received.txt  # Receiver
nc 192.168.1.10 1234 < send.txt  # Sender

# Port scan (range)
nc -zv 192.168.1.1 20-100

# Banner grab
echo "HEAD / HTTP/1.0\n\n" | nc google.com 80
```

### nc options:

| Option | Meaning |
|--------|---------|
| `-z` | Zero I/O (just test connection) |
| `-v` | Verbose output |
| `-l` | Listen mode |
| `-u` | UDP instead of TCP |

---

## tcpdump (Packet Capture)

Captures and analyzes network packets.

```bash
# Capture all packets on interface
sudo tcpdump -i eth0

# Capture only HTTP packets (port 80)
sudo tcpdump -i eth0 port 80

# Capture SSH packets to/from specific IP
sudo tcpdump -i eth0 host 192.168.1.100 and port 22

# Capture and limit to 10 packets
sudo tcpdump -i eth0 -c 10

# Save to file
sudo tcpdump -i eth0 -w capture.pcap

# Read from file
tcpdump -r capture.pcap

# Show packets in ASCII (good for HTTP)
sudo tcpdump -A -i eth0 port 80

# Show timestamps
sudo tcpdump -i eth0 -tttt
```

---

## Other Useful Tools

### mtr (My TraceRoute)

Combines ping and traceroute (real-time).

```bash
# Install mtr
sudo dnf install mtr -y

# Run mtr
mtr google.com

# Report mode (send 10 packets)
mtr -r -c 10 google.com
```

### nslookup / dig (DNS Testing)

```bash
# Query DNS
nslookup google.com
dig google.com
dig google.com A
dig -x 8.8.8.8

# Use specific DNS server
dig @8.8.8.8 google.com
```

### curl (HTTP Testing)

```bash
# Test web endpoint
curl -v https://api.example.com/health

# Check only headers
curl -I https://example.com

# Follow redirects
curl -L https://example.com

# Timeout after 5 seconds
curl --connect-timeout 5 https://example.com
```

---

## Troubleshooting Scenarios

### Scenario 1: Cannot reach website

| Step | Command | What to check |
|------|---------|---------------|
| 1 | `ping google.com` | Basic connectivity |
| 2 | `traceroute google.com` | Where path breaks |
| 3 | `dig google.com` | DNS resolution |
| 4 | `curl -v https://google.com` | HTTP response |

### Scenario 2: SSH connection failing

| Step | Command | What to check |
|------|---------|---------------|
| 1 | `ping 10.0.0.5` | Host reachable |
| 2 | `telnet 10.0.0.5 22` | SSH port open |
| 3 | `ssh -v user@10.0.0.5` | Verbose SSH output |

### Scenario 3: Slow connection

| Step | Command | What to check |
|------|---------|---------------|
| 1 | `ping -c 10 google.com` | Packet loss / latency |
| 2 | `traceroute google.com` | Slow hop |
| 3 | `mtr google.com` | Real-time analysis |

---

## Port Reference for Troubleshooting

| Service | Port | Protocol | Test command |
|---------|------|----------|--------------|
| SSH | 22 | TCP | `telnet host 22` |
| HTTP | 80 | TCP | `curl http://host` |
| HTTPS | 443 | TCP | `curl https://host` |
| DNS | 53 | UDP | `dig @host google.com` |
| MySQL | 3306 | TCP | `telnet host 3306` |
| PostgreSQL | 5432 | TCP | `telnet host 5432` |

---

## Commands Summary

```bash
# Connectivity
ping -c 4 google.com
traceroute google.com
mtr google.com

# Port testing
telnet google.com 80
nc -zv google.com 443
ss -tulpn | grep LISTEN

# DNS
dig google.com
nslookup google.com

# HTTP testing
curl -v https://api.example.com
curl -I https://example.com

# Packet capture
sudo tcpdump -i eth0 -c 10
sudo tcpdump -i eth0 port 80 -A
```
