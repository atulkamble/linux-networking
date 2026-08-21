# Linux Networking — Basic Definitions, Diagrams & Commands

Linux networking is the process of connecting a Linux system to other computers, servers, networks, and the Internet using **network interfaces, IP addresses, protocols, routing, DNS, and ports**.

---

## 1. Basic Linux Network

### Definition

A **computer network** is a group of devices connected together so they can communicate and exchange data.

```text
                    INTERNET
                       │
                       │
                 ┌─────▼─────┐
                 │  Router   │
                 │192.168.1.1│
                 └─────┬─────┘
                       │
                ───────┴──────── LAN
                   │         │
           ┌───────▼───┐ ┌──▼──────────┐
           │ Linux PC  │ │ Linux Server│
           │192.168.1.10│ │192.168.1.20│
           └───────────┘ └─────────────┘
```

Here:

* **LAN** — Local Area Network connecting nearby devices.
* **Router** — Connects different networks.
* **Internet** — Global network of interconnected networks.
* **Linux host** — A Linux computer connected to the network.

---

# 2. Network Interface

### Definition

A **network interface** is the hardware or virtual connection Linux uses to communicate with a network.

Common interface names include:

```text
eth0
ens33
enp0s3
wlan0
lo
```

Diagram:

```text
Linux Machine
┌─────────────────────────────┐
│                             │
│ Application                 │
│      │                      │
│      ▼                      │
│ TCP / UDP                   │
│      │                      │
│      ▼                      │
│ IP                          │
│      │                      │
│      ▼                      │
│ Network Interface           │
│ eth0 / ens33 / enp0s3       │
│      │                      │
└──────┼──────────────────────┘
       │
       ▼
     Network
```

Check interfaces:

```bash
ip addr
```

Short version:

```bash
ip a
```

Check interface state:

```bash
ip link
```

---

# 3. Loopback Interface

### Definition

The **loopback interface** is a virtual network interface used by a Linux machine to communicate with itself.

Its standard IPv4 address is:

```text
127.0.0.1
```

Hostname:

```text
localhost
```

Diagram:

```text
          Linux Machine
       ┌─────────────────┐
       │                 │
       │ Application     │
       │      │          │
       │      ▼          │
       │   localhost     │
       │   127.0.0.1     │
       │      │          │
       │      ▼          │
       │     lo          │
       │                 │
       └─────────────────┘
```

Test it:

```bash
ping 127.0.0.1
```

or:

```bash
ping localhost
```

---

# 4. IP Address

### Definition

An **IP address** is a logical address assigned to a device or network interface so it can be identified and communicate on an IP network.

Example:

```text
192.168.1.10
```

Diagram:

```text
Linux PC                       Linux Server

192.168.1.10                   192.168.1.20
      │                              │
      └────────── Network ───────────┘
```

Check IP addresses:

```bash
ip addr
```

Quickly display host IP addresses:

```bash
hostname -I
```

---

# 5. IPv4 and IPv6

### IPv4 Definition

**IPv4** uses a 32-bit address.

Example:

```text
192.168.1.10
```

### IPv6 Definition

**IPv6** uses a 128-bit address and was introduced largely to provide a much larger address space.

Example:

```text
2001:db8::10
```

```text
IP Addresses
     │
     ├── IPv4
     │    └── 192.168.1.10
     │
     └── IPv6
          └── 2001:db8::10
```

---

# 6. Subnet and Subnet Mask

### Definition

A **subnet** is a logical subdivision of an IP network.

A **subnet mask/prefix** determines which part of an IPv4 address represents the network and which part identifies the host.

Example:

```text
IP Address     : 192.168.1.10
Subnet Mask    : 255.255.255.0
CIDR           : /24
Network        : 192.168.1.0/24
```

Diagram:

```text
              192.168.1.0/24
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼

 192.168.1.10   192.168.1.20   192.168.1.30
     PC             Server          PC
```

Devices in the same subnet can normally communicate directly at the local network layer.

---

# 7. Default Gateway

### Definition

A **default gateway** is the router Linux sends packets to when the destination is outside the directly connected networks and no more specific route exists.

Example:

```text
Linux IP : 192.168.1.10
Gateway  : 192.168.1.1
```

Diagram:

```text
Linux Machine
192.168.1.10
      │
      ▼
┌─────────────┐
│   Router    │
│192.168.1.1  │
│   Gateway   │
└──────┬──────┘
       │
       ▼
    Internet
```

Check gateway:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

---

# 8. MAC Address

### Definition

A **MAC address** is a Layer-2 hardware identifier associated with a network interface.

Example:

```text
00:1A:2B:3C:4D:5E
```

Simplified relationship:

```text
Application
     ↓
IP Address
192.168.1.10
     ↓
MAC Address
00:1A:2B:3C:4D:5E
     ↓
Network Interface
     ↓
Network
```

Check MAC address:

```bash
ip link
```

---

# 9. DNS

### Definition

**DNS — Domain Name System** translates domain names into IP addresses and provides other DNS records.

For example:

```text
google.com
     ↓
    DNS
     ↓
IP Address
```

Diagram:

```text
Linux Machine
     │
     │ "What is google.com's IP?"
     ▼
┌────────────┐
│ DNS Server │
└─────┬──────┘
      │
      │ IP Address
      ▼
Linux Machine
      │
      ▼
Google Server
```

Check DNS configuration:

```bash
cat /etc/resolv.conf
```

Test DNS:

```bash
nslookup google.com
```

or:

```bash
dig google.com
```

---

# 10. Routing

### Definition

**Routing** is the process of selecting where IP packets should be sent based on the destination address and the system's routing table.

Linux maintains a **routing table** containing available routes.

```text
                   Linux
               192.168.1.10
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
    Local Network          Default Gateway
   192.168.1.0/24          192.168.1.1
          │                     │
          ▼                     ▼
   Local Machines             Internet
```

View routing table:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0
```

---

# 11. TCP

### Definition

**TCP — Transmission Control Protocol** is a connection-oriented transport protocol that provides reliable, ordered delivery of a byte stream.

Common TCP applications include:

```text
SSH
HTTP/HTTPS
MySQL
PostgreSQL
```

Simplified flow:

```text
Client                           Server
  │                                │
  │ SYN ──────────────────────────►│
  │◄────────────────────── SYN-ACK │
  │ ACK ──────────────────────────►│
  │                                │
  │       Connection Ready         │
```

This is known as the **TCP three-way handshake**.

---

# 12. UDP

### Definition

**UDP — User Datagram Protocol** is a connectionless transport protocol with lower overhead than TCP. It does not itself guarantee delivery, ordering, or retransmission.

Common uses include:

```text
DNS
DHCP
Streaming
VoIP
```

Simplified:

```text
Client                    Server
   │                         │
   │──── Datagram ──────────►│
   │                         │
```

---

# 13. TCP vs UDP

| Feature            | TCP                     | UDP             |
| ------------------ | ----------------------- | --------------- |
| Connection         | Connection-oriented     | Connectionless  |
| Delivery guarantee | Yes, at transport layer | No              |
| Ordering           | Yes                     | No guarantee    |
| Overhead           | Higher                  | Lower           |
| Example uses       | SSH, HTTP/S             | DNS, DHCP, VoIP |

---

# 14. Port

### Definition

A **port** is a numbered transport-layer endpoint used to identify a network service or application on a host.

```text
IP Address + Port
       │
       ▼
192.168.1.20:22
```

Diagram:

```text
             Linux Server
            192.168.1.20
                  │
      ┌───────────┼───────────┐
      │           │           │
      ▼           ▼           ▼

   Port 22      Port 80     Port 443
     SSH          HTTP        HTTPS
```

Common ports:

| Port | Service    |
| ---: | ---------- |
|   22 | SSH        |
|   53 | DNS        |
|   80 | HTTP       |
|  443 | HTTPS      |
| 3306 | MySQL      |
| 5432 | PostgreSQL |

Check listening TCP/UDP sockets:

```bash
ss -tuln
```

Show associated processes where permitted:

```bash
sudo ss -tulnp
```

---

# 15. Client and Server

### Client Definition

A **client** requests a service.

### Server Definition

A **server** provides a service to clients.

```text
CLIENT                              SERVER
192.168.1.10                       192.168.1.20
     │                                   │
     │────── HTTP Request :80 ──────────►│
     │                                   │
     │◄──────── HTTP Response ───────────│
     │                                   │
```

Example:

```bash
curl http://192.168.1.20
```

---

# 16. Router

### Definition

A **router** is a Layer-3 device or software function that forwards IP packets between different networks.

```text
192.168.1.0/24

Linux PCs
    │
    ▼
┌────────┐
│ Router │
└───┬────┘
    │
    ▼
Internet
```

---

# 17. Switch

### Definition

A **switch** primarily connects devices within the same Layer-2 network and forwards Ethernet frames using MAC-address information.

```text
             Switch
          ┌──────────┐
          │          │
          └─┬───┬──┬─┘
            │   │  │
       ┌────┘   │  └────┐
       ▼        ▼       ▼
      PC1      PC2    Server
```

A basic distinction:

```text
Switch
  ↓
Connects devices within a LAN

Router
  ↓
Connects different IP networks
```

---

# 18. Firewall

### Definition

A **firewall** controls network traffic according to security rules.

It can allow or block traffic based on properties such as:

```text
Source IP
Destination IP
Protocol
Port
Direction
Connection state
```

Diagram:

```text
Internet
    │
    ▼
┌──────────┐
│ Firewall │
└────┬─────┘
     │
     │ Allowed
     ▼
Linux Server
```

Linux commonly uses technologies such as:

```bash
nftables
iptables
firewalld
ufw
```

The exact tool depends on the Linux distribution and configuration.

---

# 19. Linux Networking Stack

```text
┌─────────────────────────────┐
│ Application Layer           │
│ HTTP / SSH / DNS            │
├─────────────────────────────┤
│ Transport Layer             │
│ TCP / UDP                   │
├─────────────────────────────┤
│ Network Layer               │
│ IPv4 / IPv6 / ICMP          │
├─────────────────────────────┤
│ Data Link Layer             │
│ Ethernet / MAC              │
├─────────────────────────────┤
│ Physical Layer              │
│ Cable / Wi-Fi / Hardware    │
└─────────────────────────────┘
```

Simplified packet flow:

```text
Application
     ↓
TCP / UDP
     ↓
IP
     ↓
Ethernet / MAC
     ↓
Network Interface
     ↓
Switch
     ↓
Router
     ↓
Internet
```

---

# 20. Basic Linux Networking Troubleshooting

A useful troubleshooting flow is:

```text
Network Problem
      │
      ▼
1. Check Interface
      │
      ▼
2. Check IP Address
      │
      ▼
3. Check Local Connectivity
      │
      ▼
4. Check Gateway
      │
      ▼
5. Check Internet IP
      │
      ▼
6. Check DNS
      │
      ▼
7. Check Route
      │
      ▼
8. Check Port / Service
```

Commands:

```bash
ip link
ip addr

ping 127.0.0.1
ping <gateway-ip>
ping 8.8.8.8
ping google.com

ip route

nslookup google.com
dig google.com

ss -tulnp

curl http://example.com

traceroute google.com
```

A useful diagnosis pattern is:

```text
ping 8.8.8.8 works
        +
ping google.com fails
        ↓
Likely DNS problem
```

Whereas:

```text
Gateway unreachable
        ↓
Investigate interface,
IP/subnet, link, VLAN,
Wi-Fi/LAN, or routing
```

---

# Quick Revision

| Term              | Basic Definition                       | Useful Command                 |
| ----------------- | -------------------------------------- | ------------------------------ |
| Network Interface | Linux network connection               | `ip link`                      |
| IP Address        | Logical network address                | `ip addr`                      |
| MAC Address       | Layer-2 interface identifier           | `ip link`                      |
| Subnet            | Logical portion of an IP network       | `ip addr`                      |
| Gateway           | Router used to reach other networks    | `ip route`                     |
| DNS               | Resolves names and DNS records         | `dig`                          |
| Routing           | Determines packet paths                | `ip route`                     |
| TCP               | Reliable connection-oriented transport | `ss -t`                        |
| UDP               | Connectionless datagram transport      | `ss -u`                        |
| Port              | Identifies a network service endpoint  | `ss -tuln`                     |
| Firewall          | Filters network traffic                | `nft` / `firewall-cmd` / `ufw` |
| Loopback          | Local host networking interface        | `ping 127.0.0.1`               |
| DNS config        | Resolver configuration                 | `cat /etc/resolv.conf`         |
| Connectivity      | Test reachability                      | `ping`                         |
| HTTP/S            | Test web connectivity                  | `curl`                         |
| Route path        | Inspect network path                   | `traceroute`                   |

### Recommended learning order

**Network → Interface → MAC → IP → Subnet → Gateway → DNS → Routing → TCP/UDP → Ports → Client/Server → Firewall → Troubleshooting**

This sequence gives a strong foundation before moving to **Linux network configuration, NetworkManager, `nmcli`, static IP configuration, SSH, NAT, firewall rules, packet capture with `tcpdump`, and Linux network namespaces**.
