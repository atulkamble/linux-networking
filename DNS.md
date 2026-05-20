# Linux Network & DNS Commands Cheat Sheet

## 1. Check IP Address

### Show IP Address

```bash
ip addr
```

Short:

```bash
ip a
```

### Show Only IPv4

```bash
ip -4 addr
```

### Show Interface Details

```bash
ip link
```

---

# 2. Check Network Connectivity

### Ping Google

```bash
ping google.com
```

### Ping Specific IP

```bash
ping 8.8.8.8
```

### Limited Ping Count

```bash
ping -c 4 google.com
```

---

# 3. DNS Lookup Commands

## nslookup

### Check DNS Resolution

```bash
nslookup google.com
```

### Query Specific DNS Server

```bash
nslookup google.com 8.8.8.8
```

---

## dig

### Install Dig (Ubuntu/Debian)

```bash
sudo apt install dnsutils -y
```

### Install Dig (Amazon Linux/RHEL)

```bash
sudo dnf install bind-utils -y
```

### DNS Lookup

```bash
dig google.com
```

### Short Output

```bash
dig google.com +short
```

### MX Record

```bash
dig google.com MX
```

### NS Record

```bash
dig google.com NS
```

### Reverse Lookup

```bash
dig -x 8.8.8.8
```

---

## host Command

### Install

```bash
sudo apt install bind9-host -y
```

### Lookup

```bash
host google.com
```

### Reverse Lookup

```bash
host 8.8.8.8
```

---

# 4. Check DNS Server Configured

## Linux

```bash
cat /etc/resolv.conf
```

Example:

```bash
nameserver 8.8.8.8
nameserver 1.1.1.1
```

---

# 5. Trace Network Path

## traceroute

### Install

Ubuntu/Debian:

```bash
sudo apt install traceroute -y
```

Amazon Linux/RHEL:

```bash
sudo dnf install traceroute -y
```

### Run

```bash
traceroute google.com
```

---

# 6. Check Open Ports

## netstat

### Install

```bash
sudo apt install net-tools -y
```

### Show Listening Ports

```bash
netstat -tulnp
```

---

## ss Command (Modern Alternative)

```bash
ss -tulnp
```

---

# 7. Check Routing Table

```bash
ip route
```

OR

```bash
route -n
```

---

# 8. Test Port Connectivity

## telnet

```bash
telnet google.com 80
```

## nc (Netcat)

```bash
nc -zv google.com 443
```

---

# 9. Download Test

## curl

```bash
curl google.com
```

### Check Headers

```bash
curl -I https://google.com
```

---

## wget

```bash
wget https://google.com
```

---

# 10. Check Hostname

```bash
hostname
```

### FQDN

```bash
hostname -f
```

---

# Important Ports to Remember

| Service | Port |
| ------- | ---- |
| SSH     | 22   |
| HTTP    | 80   |
| HTTPS   | 443  |
| DNS     | 53   |
| FTP     | 21   |
| SMTP    | 25   |
| RDP     | 3389 |

---

# Points to Remember

* DNS converts Domain Name → IP Address
* `ping` checks connectivity
* `nslookup`, `dig`, `host` check DNS resolution
* `traceroute` checks network path
* `ss` and `netstat` check listening ports
* `/etc/resolv.conf` stores DNS server details
* `curl` and `wget` test web connectivity
* `ip addr` replaces old `ifconfig`

---

# Quick Interview Questions

## Difference Between ping and nslookup

| ping                | nslookup               |
| ------------------- | ---------------------- |
| Tests connectivity  | Tests DNS resolution   |
| Uses ICMP           | Uses DNS protocol      |
| Checks reachability | Checks name resolution |

---

## Difference Between dig and nslookup

| dig                           | nslookup          |
| ----------------------------- | ----------------- |
| Detailed output               | Simple output     |
| Preferred for troubleshooting | Basic DNS queries |
| Supports advanced options     | Limited options   |

---

# Most Used Real-Time Commands

```bash
ip a
ping google.com
nslookup google.com
dig google.com +short
cat /etc/resolv.conf
ss -tulnp
curl -I https://google.com
traceroute google.com
```
