Linux networking is the set of technologies and tools that allow Linux systems to communicate with each other and with other networks. It covers everything from configuring IP addresses to routing, firewalls, VPNs, and network troubleshooting.

Here's a structured overview:

## 1. Linux Network Architecture

```
Application Layer
    │
Socket API
    │
TCP / UDP
    │
IP (IPv4 / IPv6)
    │
Ethernet / Wi-Fi
    │
Network Interface Card (NIC)
```

Linux uses the **TCP/IP protocol stack**, which is implemented inside the kernel.

---

## 2. Network Interfaces

View interfaces:

```bash
ip link show
```

View IP addresses:

```bash
ip addr show
```

Enable an interface:

```bash
sudo ip link set eth0 up
```

Disable an interface:

```bash
sudo ip link set eth0 down
```

---

## 3. IP Address Configuration

Assign an IP address:

```bash
sudo ip addr add 192.168.1.100/24 dev eth0
```

Remove an IP:

```bash
sudo ip addr del 192.168.1.100/24 dev eth0
```

Default gateway:

```bash
sudo ip route add default via 192.168.1.1
```

Display routing table:

```bash
ip route
```

---

## 4. Essential Networking Commands

| Command            | Purpose               |
| ------------------ | --------------------- |
| `ip`               | Network configuration |
| `ping`             | Test connectivity     |
| `ss`               | View sockets          |
| `netstat` (legacy) | Network statistics    |
| `traceroute`       | Trace packet path     |
| `dig`              | DNS lookup            |
| `nslookup`         | DNS queries           |
| `host`             | DNS resolution        |
| `curl`             | HTTP requests         |
| `wget`             | Download files        |
| `tcpdump`          | Packet capture        |
| `nmap`             | Network scanning      |

Example:

```bash
ping google.com
```

---

## 5. Routing

Show routes:

```bash
ip route show
```

Add route:

```bash
sudo ip route add 10.0.0.0/24 via 192.168.1.1
```

Delete route:

```bash
sudo ip route del 10.0.0.0/24
```

---

## 6. DNS Configuration

DNS servers are usually stored in:

```
/etc/resolv.conf
```

Example:

```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

Test DNS:

```bash
dig google.com
```

---

## 7. SSH

Connect to another Linux machine:

```bash
ssh user@192.168.1.10
```

Copy files:

```bash
scp file.txt user@192.168.1.10:/home/user/
```

Generate SSH key:

```bash
ssh-keygen
```

---

## 8. Network Services

Check listening ports:

```bash
ss -tuln
```

Example output:

```
LISTEN 0 128 0.0.0.0:22
```

Meaning:

* TCP service
* Listening
* Port 22 (SSH)

---

## 9. Firewall

Using `ufw`:

Enable:

```bash
sudo ufw enable
```

Allow SSH:

```bash
sudo ufw allow 22
```

Status:

```bash
sudo ufw status
```

Using `iptables`:

```bash
sudo iptables -L
```

---

## 10. Packet Capture

Capture packets:

```bash
sudo tcpdump -i eth0
```

Capture HTTP traffic:

```bash
sudo tcpdump port 80
```

Capture specific host:

```bash
sudo tcpdump host 192.168.1.100
```

---

## 11. Network Troubleshooting

Check connectivity:

```bash
ping 8.8.8.8
```

Check DNS:

```bash
dig google.com
```

Check routes:

```bash
ip route
```

Check interfaces:

```bash
ip addr
```

Check listening services:

```bash
ss -tuln
```

Trace network path:

```bash
traceroute google.com
```

---

## 12. Common Configuration Files

| File                                                   | Purpose                          |
| ------------------------------------------------------ | -------------------------------- |
| `/etc/hosts`                                           | Local hostname resolution        |
| `/etc/resolv.conf`                                     | DNS configuration                |
| `/etc/hostname`                                        | System hostname                  |
| `/etc/network/interfaces` (Debian)                     | Interface configuration (legacy) |
| `/etc/netplan/*.yaml` (Ubuntu)                         | Network configuration            |
| `/etc/sysconfig/network-scripts/` (RHEL/CentOS legacy) | Network configuration            |

---

## 13. Network Managers

Different Linux distributions use different network management tools:

* **NetworkManager** (desktop and many server distributions)
* **systemd-networkd** (systemd-based servers)
* **Netplan** (Ubuntu)
* **ifup/ifdown** (older Debian systems)

---

## 14. Important Networking Ports

| Port  | Service    |
| ----- | ---------- |
| 20/21 | FTP        |
| 22    | SSH        |
| 23    | Telnet     |
| 25    | SMTP       |
| 53    | DNS        |
| 67/68 | DHCP       |
| 80    | HTTP       |
| 110   | POP3       |
| 143   | IMAP       |
| 443   | HTTPS      |
| 3306  | MySQL      |
| 5432  | PostgreSQL |

---

## 15. Typical Troubleshooting Workflow

1. Check whether the network interface is up:

   ```bash
   ip link
   ```
2. Verify the IP address:

   ```bash
   ip addr
   ```
3. Verify the default route:

   ```bash
   ip route
   ```
4. Ping the default gateway:

   ```bash
   ping <gateway-ip>
   ```
5. Ping a public IP (for example, `8.8.8.8`) to test internet connectivity.
6. Test DNS resolution:

   ```bash
   dig google.com
   ```
7. Check for firewall rules:

   ```bash
   sudo ufw status
   ```

   or

   ```bash
   sudo iptables -L
   ```
8. Inspect listening services:

   ```bash
   ss -tuln
   ```

Linux networking is a broad topic, but mastering commands like `ip`, `ss`, `ping`, `curl`, `dig`, `tcpdump`, and understanding routing, DNS, and firewalls provides a strong foundation for system administration, DevOps, and cloud engineering.
