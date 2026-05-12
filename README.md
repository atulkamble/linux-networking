# 🌐 IPv4 Addressing

---

## 📘 Introduction to IPv4 Addressing and Structure

IPv4 (Internet Protocol Version 4) is the most widely used protocol for communication between devices on a network.

### 📌 Features of IPv4

* Uses 32-bit addressing
* Written in dotted decimal format
* Identifies devices uniquely
* Enables communication between systems

### 📌 IPv4 Example

```bash id="1omymh"
192.168.1.10
```

---

## 📘 IPv4 Address Structure

IPv4 contains 4 octets.

| Decimal | Binary   |
| ------- | -------- |
| 192     | 11000000 |
| 168     | 10101000 |
| 1       | 00000001 |
| 10      | 00001010 |

---

## 📘 IPv4 Address Classes

| Class | Range     | Default Subnet Mask | Usage           |
| ----- | --------- | ------------------- | --------------- |
| A     | 1 – 126   | 255.0.0.0           | Large Networks  |
| B     | 128 – 191 | 255.255.0.0         | Medium Networks |
| C     | 192 – 223 | 255.255.255.0       | Small Networks  |
| D     | 224 – 239 | N/A                 | Multicast       |
| E     | 240 – 255 | N/A                 | Experimental    |

---

## 📘 Reserved IPv4 Addresses

| Address         | Purpose       |
| --------------- | ------------- |
| 127.0.0.1       | Loopback      |
| 0.0.0.0         | Default Route |
| 255.255.255.255 | Broadcast     |
| 169.254.x.x     | APIPA         |

---

## 📘 Public vs Private IP Addressing

### 🌍 Public IP Address

* Accessible over internet
* Assigned by ISP
* Globally unique

Example:

```bash id="2kccqg"
8.8.8.8
```

---

### 🏠 Private IP Address

Used inside local/private networks.

| Range                         | Class |
| ----------------------------- | ----- |
| 10.0.0.0 – 10.255.255.255     | A     |
| 172.16.0.0 – 172.31.255.255   | B     |
| 192.168.0.0 – 192.168.255.255 | C     |

---

## 📘 Static IP vs Dynamic IP

| Type       | Description            |
| ---------- | ---------------------- |
| Static IP  | Fixed IP Address       |
| Dynamic IP | Automatically Assigned |

### 📌 DHCP

```bash id="ytd70r"
DHCP = Dynamic Host Configuration Protocol
```

---

## 📘 Network ID and Host ID Concept

Every IP address contains:

* Network Portion
* Host Portion

### 📌 Example

```bash id="af7c8x"
192.168.1.25/24
```

| Component  | Value       |
| ---------- | ----------- |
| Network ID | 192.168.1.0 |
| Host ID    | 25          |

---

## 📘 Subnet Mask and CIDR Notation

### 📌 Common Subnet Masks

| CIDR | Subnet Mask     |
| ---- | --------------- |
| /8   | 255.0.0.0       |
| /16  | 255.255.0.0     |
| /24  | 255.255.255.0   |
| /25  | 255.255.255.128 |
| /26  | 255.255.255.192 |
| /27  | 255.255.255.224 |
| /28  | 255.255.255.240 |

---

### 📌 CIDR Example

```bash id="l3zy8f"
192.168.1.0/24
```

Meaning:

* 24 bits Network
* 8 bits Hosts

---

## 📘 Broadcast Address

Broadcast sends packets to all hosts within a network.

### 📌 Example

Network:

```bash id="gnt9z8"
192.168.1.0/24
```

Broadcast:

```bash id="j0e1pf"
192.168.1.255
```

---

## 📘 Loopback Address

Used for internal testing.

### 📌 Example

```bash id="7b8k0t"
127.0.0.1
```

### 📌 Test Localhost

```bash id="tqz22w"
ping 127.0.0.1
```

---

# 🌐 Mastering IPv4 & IPv6 Addressing

---

## 📘 Introduction to Subnetting Principles

Subnetting divides one large network into smaller networks.

### 📌 Advantages of Subnetting

* Better security
* Improved performance
* Reduced broadcast traffic
* Efficient IP utilization

---

## 📘 Binary Basics for Subnetting

| Decimal | Binary   |
| ------- | -------- |
| 128     | 10000000 |
| 192     | 11000000 |
| 224     | 11100000 |
| 240     | 11110000 |
| 248     | 11111000 |
| 252     | 11111100 |

---

## 📘 Subnetting Techniques

### 📌 FLSM

Fixed Length Subnet Mask

* All subnets are equal size

---

### 📌 VLSM

Variable Length Subnet Mask

* Different subnet sizes
* Better IP utilization

---

## 📘 Calculating Number of Subnets and Hosts

### 📌 Formula for Subnets

2^n

Where:

* `n` = borrowed bits

---

### 📌 Formula for Hosts

2^h - 2

Where:

* `h` = host bits

---

## 📘 Practical Subnetting Scenarios

### 📌 Scenario 1

Requirement:

```bash id="l2yyq7"
Need 50 hosts
```

Solution:

```bash id="m2p5lc"
/26
```

Usable Hosts:

```bash id="7k3w67"
62
```

---

### 📌 Scenario 2

Requirement:

```bash id="ujw9bz"
Need 200 hosts
```

Solution:

```bash id="3lnzyq"
/24
```

Usable Hosts:

```bash id="szf4kg"
254
```

---

## 📘 Subnetting Cheat Sheet

| CIDR | Usable Hosts |
| ---- | ------------ |
| /24  | 254          |
| /25  | 126          |
| /26  | 62           |
| /27  | 30           |
| /28  | 14           |
| /29  | 6            |
| /30  | 2            |

---

# 🌐 IPv6 Addressing

---

## 📘 Overview of IPv6 and Its Need

IPv6 was introduced because IPv4 addresses are exhausted.

### 📌 Advantages of IPv6

* 128-bit addressing
* Larger address space
* Better routing
* Built-in security
* Auto configuration

---

## 📘 IPv6 Address Structure and Representation

### 📌 IPv6 Example

```bash id="3tw8yb"
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

---

### 📌 Shortened IPv6

```bash id="utxz1f"
2001:db8:85a3::8a2e:370:7334
```

---

## 📘 Types of IPv6 Addresses

| Type      | Description    |
| --------- | -------------- |
| Unicast   | One-to-One     |
| Multicast | One-to-Many    |
| Anycast   | Nearest Device |

---

## 📘 IPv6 Address Categories

| Category       | Example   |
| -------------- | --------- |
| Global Unicast | 2000::/3  |
| Link Local     | FE80::/10 |
| Loopback       | ::1       |
| Multicast      | FF00::/8  |

---

## 📘 IPv6 Address Generation using EUI-64

EUI-64 automatically creates IPv6 interface IDs using MAC addresses.

### 📌 Benefits

* Automatic configuration
* Simplifies administration

---

## 📘 IPv4 vs IPv6 Key Differences

| Feature        | IPv4      | IPv6           |
| -------------- | --------- | -------------- |
| Address Size   | 32-bit    | 128-bit        |
| Address Format | Decimal   | Hexadecimal    |
| NAT            | Required  | Not Required   |
| Security       | Optional  | Built-in IPSec |
| Broadcast      | Supported | Removed        |

---

## 📘 IPv4 to IPv6 Transition Concepts

### 📌 Dual Stack

IPv4 and IPv6 run together.

---

### 📌 Tunneling

IPv6 traffic travels through IPv4 networks.

---

### 📌 NAT64

Allows IPv6 systems to communicate with IPv4 systems.

---

# 🔐 Networking Basics and Security

---

## 📘 Network Configuration and Interface Management

### 📌 Show Network Interfaces

```bash id="s7q7gw"
ip addr show
```

---

### 📌 Show Interface Status

```bash id="e3m5i0"
ip link show
```

---

### 📌 Restart Network Services

#### Ubuntu

```bash id="wafcij"
sudo systemctl restart networking
```

#### RHEL / CentOS

```bash id="fajwdc"
sudo systemctl restart NetworkManager
```

---

## 📘 Network Troubleshooting Commands

### 📡 ping

```bash id="0jqeg2"
ping google.com
```

---

### 📡 traceroute

```bash id="pmp2nh"
traceroute google.com
```

Install:

```bash id="gzt4up"
sudo yum install traceroute -y
```

---

### 📡 tracepath

```bash id="9g95xb"
tracepath google.com
```

---

## 📘 IP and Interface Inspection Commands

### 📌 ip command

```bash id="k5u5h0"
ip addr
ip route
ip link
```

---

### 📌 ifconfig

```bash id="wy6gq6"
ifconfig
```

Install:

```bash id="6psm4w"
sudo yum install net-tools -y
```

---

## 📘 DNS and Connectivity Testing

### 📌 nslookup

```bash id="z76s6h"
nslookup google.com
```

---

### 📌 dig

```bash id="g4i1l0"
dig google.com
```

Install:

```bash id="t2xqzv"
sudo yum install bind-utils -y
```

---

### 📌 host

```bash id="2a6feh"
host google.com
```

---

## 📘 Port and Process Monitoring

### 📌 netstat

```bash id="9e1q1q"
netstat -tulnp
```

---

### 📌 ss

```bash id="qyptkk"
ss -tulnp
```

---

### 📌 lsof

```bash id="93f0n0"
sudo lsof -i :80
```

---

# 🔥 Firewall Configuration and Management

---

## 📘 firewalld Commands

### Check Status

```bash id="0h8f9n"
sudo systemctl status firewalld
```

---

### Start firewalld

```bash id="bg2v0z"
sudo systemctl start firewalld
```

---

### Enable firewalld

```bash id="n8m2k0"
sudo systemctl enable firewalld
```

---

### Open HTTP Port

```bash id="cyy9a7"
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

---

### Allow HTTPS

```bash id="i8m7wo"
sudo firewall-cmd --add-service=https --permanent
sudo firewall-cmd --reload
```

---

### List Rules

```bash id="c9tv94"
sudo firewall-cmd --list-all
```

---

## 📘 iptables Commands

### View Rules

```bash id="0ifwq7"
sudo iptables -L
```

---

### Allow SSH

```bash id="6j6v5d"
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

---

### Save Rules

```bash id="8vqvhf"
sudo service iptables save
```

---

# 📖 Linux Networking Practice Commands

---

## 📌 View IP Address

```bash id="4msx8r"
ip addr show
```

---

## 📌 Check Connectivity

```bash id="vcapje"
ping -c 4 google.com
```

---

## 📌 View Routing Table

```bash id="n3zcc9"
ip route
```

---

## 📌 Check Open Ports

```bash id="dkt6qr"
ss -tulnp
```

---

## 📌 Check Running Services

```bash id="d0aj3x"
systemctl list-units --type=service
```

---

## 📌 Check DNS Resolution

```bash id="1jlwm4"
dig +short google.com
```

---

## 📌 Check Public IP

```bash id="6g1l4z"
curl ifconfig.me
```

---

## 📌 Download File

```bash id="u8yyj2"
wget https://example.com/file.zip
```

---

## 📌 Transfer File

```bash id="7jlq2i"
scp file.txt user@server:/tmp/
```

---

# 📦 Bonus Networking Script

## Create Script

```bash id="ifh4lg"
nano network-check.sh
```

---

## Script

```bash id="aq7vv7"
#!/bin/bash

echo "===== NETWORK DETAILS ====="

echo "Hostname:"
hostname

echo "IP Address:"
hostname -I

echo "Default Gateway:"
ip route | grep default

echo "DNS Test:"
ping -c 2 google.com

echo "Open Ports:"
ss -tuln
```

---

## Run Script

```bash id="t0fzy0"
bash network-check.sh
```

---

# 📌 Important Networking Ports

| Service    | Port |
| ---------- | ---- |
| SSH        | 22   |
| HTTP       | 80   |
| HTTPS      | 443  |
| DNS        | 53   |
| FTP        | 21   |
| SMTP       | 25   |
| MySQL      | 3306 |
| PostgreSQL | 5432 |
| RDP        | 3389 |

---

# 📌 Important Points to Remember

## 🌐 IPv4 & IPv6

* IPv4 uses 32-bit addresses
* IPv6 uses 128-bit addresses
* IPv4 addresses are written in dotted decimal format
* IPv6 addresses are written in hexadecimal format
* IPv4 supports broadcast communication
* IPv6 removes broadcast traffic
* IPv6 loopback address is `::1`
* IPv4 loopback address is `127.0.0.1`
* Link-local IPv6 addresses begin with `FE80::`

---

## 🌐 IP Addressing

* Every device requires an IP address
* Public IPs are internet routable
* Private IPs are used within internal networks
* Static IP addresses remain fixed
* Dynamic IP addresses change automatically
* DHCP assigns IP addresses dynamically
* NAT converts private IPs into public IPs

---

## 🌐 Subnetting

* Subnetting divides large networks into smaller networks
* CIDR reduces IP wastage
* VLSM allows flexible subnet allocation
* FLSM uses equal subnet sizes
* Smaller subnets reduce broadcast traffic
* CIDR `/24` provides 254 usable hosts
* CIDR `/30` commonly used for point-to-point links

---

## 🌐 Networking Basics

* Routers connect different networks
* Switches connect devices within same network
* MAC addresses work at Layer 2
* IP addresses work at Layer 3
* ARP maps IP addresses to MAC addresses
* MTU defines maximum packet size

---

## 🌐 Protocols & Ports

* TCP is connection-oriented
* UDP is connectionless
* TCP provides reliable communication
* UDP is faster than TCP
* SSH uses port 22
* HTTP uses port 80
* HTTPS uses port 443
* DNS uses port 53

---

## 🌐 Linux Networking Commands

* `ping` checks connectivity
* `traceroute` identifies network path
* `ip addr` displays IP configuration
* `ip route` displays routing table
* `ss` is modern replacement for `netstat`
* `dig` provides detailed DNS information
* `curl` transfers data from URLs
* `wget` downloads files from internet

---

## 🔐 Networking Security

* Firewalls filter incoming and outgoing traffic
* `firewalld` is common in RHEL/CentOS systems
* `iptables` manages firewall rules
* Always reload firewall after rule changes
* Closed ports improve security
* Disable unused services and ports
* Use secure protocols like SSH and HTTPS
* Monitor open ports regularly

---

## ☁️ Cloud & DevOps Networking

* Cloud platforms rely heavily on subnetting
* Security Groups act like virtual firewalls
* Network ACLs provide subnet-level security
* Dual-stack supports both IPv4 and IPv6
* Tunneling helps IPv6 work over IPv4
* Understanding networking is critical for Cloud and DevOps roles
