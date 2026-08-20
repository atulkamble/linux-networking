# Subnetting — Easy Study Notes

## 1. What is Subnetting?

**Subnetting** is the process of dividing one large IP network into multiple smaller networks called **subnets**.

Example:

```text
Network: 192.168.1.0/24

Divide into smaller networks:

192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

### Why use subnetting?

* Better IP address utilization
* Smaller broadcast domains
* Better network performance
* Improved security and isolation
* Separate departments/environments
* Essential for AWS VPC and Azure VNet design

---

# 2. IPv4 Address Basics

An IPv4 address contains **32 bits** divided into 4 octets.

```text
192.168.1.10

192      168       1        10
 |        |        |         |
8 bits   8 bits   8 bits    8 bits

Total = 32 bits
```

Binary example:

```text
192 = 11000000
168 = 10101000
1   = 00000001
10  = 00001010
```

---

# 3. CIDR Notation

CIDR tells us how many bits belong to the **network portion**.

```text
192.168.1.0/24
              |
         24 network bits
```

That leaves:

```text
32 - 24 = 8 host bits
```

Common CIDRs:

| CIDR | Subnet Mask     | Total IPs | Traditional Usable Hosts |
| ---: | --------------- | --------: | -----------------------: |
|  /16 | 255.255.0.0     |    65,536 |                   65,534 |
|  /20 | 255.255.240.0   |     4,096 |                    4,094 |
|  /24 | 255.255.255.0   |       256 |                      254 |
|  /25 | 255.255.255.128 |       128 |                      126 |
|  /26 | 255.255.255.192 |        64 |                       62 |
|  /27 | 255.255.255.224 |        32 |                       30 |
|  /28 | 255.255.255.240 |        16 |                       14 |
|  /29 | 255.255.255.248 |         8 |                        6 |
|  /30 | 255.255.255.252 |         4 |                        2 |

The traditional host count formula is:

```text
Usable Hosts = 2^(Host Bits) - 2
```

The `-2` represents the network and broadcast addresses. Cloud platforms can reserve additional addresses.

---

# 4. Important Subnetting Formula

### Total IP addresses

```text
2^(32 - CIDR)
```

For `/26`:

```text
Host bits = 32 - 26
          = 6

Total IPs = 2^6
          = 64
```

Traditional usable hosts:

```text
64 - 2 = 62
```

---

# 5. Block Size Method

This is one of the easiest ways to solve subnetting questions.

Formula:

```text
Block Size = 256 - Subnet Mask
```

For `/26`:

```text
/26 = 255.255.255.192

Block Size = 256 - 192
           = 64
```

Therefore subnet boundaries occur every **64**:

```text
0
64
128
192
```

---

# 6. Example: Divide /24 into /26

Given:

```text
192.168.1.0/24
```

Create `/26` networks.

Subnet mask:

```text
255.255.255.192
```

Block size:

```text
256 - 192 = 64
```

Result:

| Subnet | Network Address  | Host Range  | Broadcast |
| ------ | ---------------- | ----------- | --------- |
| 1      | 192.168.1.0/26   | .1 – .62    | .63       |
| 2      | 192.168.1.64/26  | .65 – .126  | .127      |
| 3      | 192.168.1.128/26 | .129 – .190 | .191      |
| 4      | 192.168.1.192/26 | .193 – .254 | .255      |

Visual representation:

```text
192.168.1.0/24
        |
        +---- 192.168.1.0/26
        |
        +---- 192.168.1.64/26
        |
        +---- 192.168.1.128/26
        |
        +---- 192.168.1.192/26
```

---

# 7. How Many Subnets?

Original network:

```text
/24
```

New network:

```text
/26
```

Borrowed bits:

```text
26 - 24 = 2
```

Number of subnets:

```text
2^2 = 4
```

Therefore:

```text
/24 → /26 = 4 subnets
```

---

# 8. Quick CIDR Pattern

Very useful to memorize:

```text
/24 → 256 IPs
/25 → 128 IPs
/26 →  64 IPs
/27 →  32 IPs
/28 →  16 IPs
/29 →   8 IPs
/30 →   4 IPs
```

Notice that each additional CIDR bit **halves the address space**.

```text
/24
 ↓
/25  /25
 ↓
/26 /26 /26 /26
```

---

# 9. Example: /27

Given:

```text
10.0.0.0/27
```

Host bits:

```text
32 - 27 = 5
```

Total IPs:

```text
2^5 = 32
```

Traditional usable:

```text
32 - 2 = 30
```

Subnet mask:

```text
255.255.255.224
```

Block size:

```text
256 - 224 = 32
```

Networks therefore start at:

```text
10.0.0.0
10.0.0.32
10.0.0.64
10.0.0.96
10.0.0.128
10.0.0.160
10.0.0.192
10.0.0.224
```

---

# 10. Subnetting in AWS/Azure

A common cloud design could be:

```text
VPC/VNet: 10.0.0.0/16

├── Public Subnet
│   10.0.1.0/24
│
├── Application Subnet
│   10.0.2.0/24
│
└── Database Subnet
    10.0.3.0/24
```

This allows you to separate workloads such as:

```text
Internet
   |
Load Balancer
   |
Public Subnet
   |
Application Subnet
   |
Database Subnet
```

## Key formulas to remember

```text
Host Bits = 32 - CIDR

Total IPs = 2^(Host Bits)

Traditional Usable Hosts = 2^(Host Bits) - 2

Borrowed Bits = New CIDR - Original CIDR

Number of Subnets = 2^(Borrowed Bits)

Block Size = 256 - interesting subnet-mask octet
```

For example:

```text
192.168.10.0/24 → /27

Borrowed bits = 27 - 24 = 3
Subnets       = 2^3 = 8
IPs/subnet    = 2^(32-27) = 32
Usable hosts  = 30
Block size    = 32
```

So the subnet addresses are:

```text
192.168.10.0/27
192.168.10.32/27
192.168.10.64/27
192.168.10.96/27
192.168.10.128/27
192.168.10.160/27
192.168.10.192/27
192.168.10.224/27
```

# Basic Subnetting on Linux (Amazon Linux)

Subnetting is used to divide a network into smaller networks (subnets).

---

# 1. Check Current Network Configuration

```bash
ip addr
```

OR

```bash
ifconfig
```

Check routing table:

```bash
ip route
```

---

# 2. CIDR Notation Basics

CIDR defines network size.

| CIDR | Subnet Mask     | Hosts      |
| ---- | --------------- | ---------- |
| /8   | 255.0.0.0       | 16 Million |
| /16  | 255.255.0.0     | 65,534     |
| /24  | 255.255.255.0   | 254        |
| /25  | 255.255.255.128 | 126        |
| /26  | 255.255.255.192 | 62         |
| /27  | 255.255.255.224 | 30         |
| /28  | 255.255.255.240 | 14         |

---

# 3. Example Subnet

Network:

```text
192.168.1.0/24
```

Breakdown:

| Item            | Value         |
| --------------- | ------------- |
| Network Address | 192.168.1.0   |
| First Host      | 192.168.1.1   |
| Last Host       | 192.168.1.254 |
| Broadcast       | 192.168.1.255 |
| Total Hosts     | 254           |

---

# 4. Divide /24 into 2 Subnets

Original:

```text
192.168.1.0/24
```

After subnetting:

| Subnet           | Range                         |
| ---------------- | ----------------------------- |
| 192.168.1.0/25   | 192.168.1.1 - 192.168.1.126   |
| 192.168.1.128/25 | 192.168.1.129 - 192.168.1.254 |

---

# 5. Create Smaller Subnets

## /26 Example

| Subnet           | Host Range |
| ---------------- | ---------- |
| 192.168.1.0/26   | 1 – 62     |
| 192.168.1.64/26  | 65 – 126   |
| 192.168.1.128/26 | 129 – 190  |
| 192.168.1.192/26 | 193 – 254  |

---

# 6. Temporary IP Configuration (Amazon Linux)

Assign IP manually:

```bash
sudo ip addr add 192.168.1.10/24 dev eth0
```

Bring interface up:

```bash
sudo ip link set eth0 up
```

Add gateway:

```bash
sudo ip route add default via 192.168.1.1
```

---

# 7. Remove IP Address

```bash
sudo ip addr del 192.168.1.10/24 dev eth0
```

---

# 8. Check Subnet Information

Install networking tools:

```bash
sudo dnf install net-tools -y
```

Check:

```bash
ifconfig
route -n
netstat -rn
```

---

# 9. Important Networking Commands

| Command       | Purpose        |
| ------------- | -------------- |
| `ip addr`     | Show IP        |
| `ip route`    | Show routing   |
| `ping`        | Connectivity   |
| `traceroute`  | Path tracing   |
| `ss -tulnp`   | Open ports     |
| `hostname -I` | Show IP        |
| `nmcli`       | NetworkManager |

---

# 10. AWS VPC Subnet Example

Suppose VPC CIDR:

```text
10.0.0.0/16
```

Subnets:

| Subnet      | Purpose  |
| ----------- | -------- |
| 10.0.1.0/24 | Public   |
| 10.0.2.0/24 | Private  |
| 10.0.3.0/24 | Database |

---

# 11. Quick Formula

Hosts calculation:

2^n - 2

Where:

* `n` = number of host bits
* `-2` = network + broadcast addresses

Example:

For `/24`

```text
32 - 24 = 8 host bits
2^8 - 2 = 254 hosts
```

---

# 12. Real-Time AWS Example

EC2 inside subnet:

```text
Subnet: 10.0.1.0/24
Gateway: 10.0.1.1
EC2 IP: 10.0.1.10
```

Check from EC2:

```bash
ip addr
ip route
ping 8.8.8.8
```

---

# 13. Points to Remember

* `/24` → most common subnet
* Smaller CIDR = larger network
* Larger CIDR = smaller network
* AWS reserves 5 IPs in every subnet
* Public subnet needs Internet Gateway
* Private subnet uses NAT Gateway

---

# 14. AWS Reserved IP Example

For subnet:

```text
10.0.1.0/24
```

AWS reserves:

| IP   | Purpose    |
| ---- | ---------- |
| .0   | Network    |
| .1   | Router     |
| .2   | DNS        |
| .3   | Future use |
| .255 | Broadcast  |

Usable starts from:

```text
10.0.1.4
```
