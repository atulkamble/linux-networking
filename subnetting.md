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
