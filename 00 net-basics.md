# 🌐 Basics of Networking

Networking is the process of **connecting two or more devices so they can communicate and share data/resources**.

Example:

```text
Laptop ───── Wi-Fi Router ───── Internet
                                 │
                              Web Server
```

## 1. Basic Networking Components

| Component       | Definition                                          | Example                        |
| --------------- | --------------------------------------------------- | ------------------------------ |
| **Host**        | Any device connected to a network                   | Laptop, server, phone          |
| **NIC**         | Hardware/interface connecting a device to a network | Ethernet, Wi-Fi                |
| **IP Address**  | Logical address identifying a device                | `192.168.1.10`                 |
| **MAC Address** | Hardware address of a network interface             | `00:1A:2B:3C:4D:5E`            |
| **Switch**      | Connects devices within a LAN                       | Office switch                  |
| **Router**      | Connects different networks                         | Home Wi-Fi router              |
| **Gateway**     | Exit point from one network to another              | `192.168.1.1`                  |
| **DNS**         | Converts domain names to IP addresses               | `google.com → IP`              |
| **DHCP**        | Automatically provides IP configuration             | Router assigns laptop IP       |
| **Firewall**    | Allows/blocks network traffic using rules           | Linux firewall, cloud firewall |
| **Port**        | Identifies a particular network service             | SSH `22`, HTTP `80`            |

## 2. LAN and WAN

### LAN — Local Area Network

A LAN connects devices in a relatively small area.

```text
        Switch
       /   |   \
      /    |    \
   PC1    PC2   Server
```

Examples include a home network, office network, or computer lab.

### WAN — Wide Area Network

A WAN connects networks over large geographical areas.

```text
Office LAN
    │
 Router
    │
 Internet / WAN
    │
 Router
    │
Cloud / Data Center
```

The **Internet is the largest WAN**.

## 3. IP Address

An IP address identifies a device/interface on an IP network.

Example:

```text
192.168.1.10
```

Two major versions exist:

```text
IPv4
192.168.1.10

IPv6
2001:db8::10
```

A simple LAN might look like:

```text
           Router
        192.168.1.1
             │
          Switch
        ┌────┼────┐
        │    │    │
      PC1   PC2  Server
      .10   .20   .30
```

## 4. Public vs Private IP

**Private IP addresses** are commonly used inside internal networks.

Important IPv4 private ranges:

```text
10.0.0.0       - 10.255.255.255
172.16.0.0     - 172.31.255.255
192.168.0.0    - 192.168.255.255
```

A typical home network:

```text
Laptop
192.168.1.10
     │
     ▼
Router / NAT
Private IP: 192.168.1.1
Public IP: Internet-facing address
     │
     ▼
Internet
```

## 5. Subnet and Subnet Mask

A subnet divides an IP network into smaller networks.

Example:

```text
192.168.1.0/24
```

For a typical `/24`:

```text
Network:     192.168.1.0
Hosts:       192.168.1.1 - 192.168.1.254
Broadcast:   192.168.1.255
Mask:        255.255.255.0
```

CIDR notation such as `/24` tells us how many bits represent the **network portion**.

## 6. MAC Address

A MAC address identifies a network interface at the data-link layer.

Example:

```text
00:1A:2B:3C:4D:5E
```

Simplified local communication:

```text
IP Address
    ↓
ARP
    ↓
MAC Address
    ↓
Ethernet Frame
```

## 7. Switch vs Router

```text
PC1 ──┐
PC2 ──┼── Switch ─── Router ─── Internet
PC3 ──┘
```

A **switch** primarily connects devices in the same LAN, while a **router** forwards packets between different IP networks.

## 8. DNS

DNS stands for **Domain Name System**.

Humans use:

```text
www.example.com
```

Computers communicate using IP addresses, so DNS performs name resolution:

```text
www.example.com
       │
       ▼
    DNS Server
       │
       ▼
   IP Address
       │
       ▼
   Web Server
```

Think of DNS as a distributed directory for network names.

## 9. DHCP

DHCP stands for **Dynamic Host Configuration Protocol**.

It can automatically provide devices with:

```text
IP Address
Subnet Mask
Default Gateway
DNS Server
```

Basic DHCP process:

```text
Client
  │
  │ Discover
  ▼
DHCP Server
  │
  │ Offer
  ▼
Client
  │
  │ Request
  ▼
DHCP Server
  │
  │ Acknowledge
  ▼
Client gets IP configuration
```

This is commonly remembered as **DORA**:

```text
Discover → Offer → Request → Acknowledge
```

## 10. Default Gateway

The default gateway is normally the router used to reach networks outside the local subnet.

```text
Laptop
192.168.1.10
     │
     ▼
Default Gateway
192.168.1.1
     │
     ▼
Internet
```

If the destination is outside the laptop's local subnet, the packet is generally sent toward the gateway.

## 11. Ports

An IP address identifies a host/interface, while a **port identifies an application/service endpoint**.

```text
Server
192.168.1.20
     │
     ├── 22   SSH
     ├── 53   DNS
     ├── 80   HTTP
     └── 443  HTTPS
```

Common ports:

|   Port | Service    |
| -----: | ---------- |
|   `22` | SSH        |
|   `53` | DNS        |
|   `80` | HTTP       |
|  `443` | HTTPS      |
| `3306` | MySQL      |
| `5432` | PostgreSQL |

## 12. TCP and UDP

Both operate at the **transport layer**.

**TCP** is connection-oriented and provides reliable, ordered delivery.

```text
Client                  Server
  │ ---- SYN ----------> │
  │ <--- SYN-ACK ------- │
  │ ---- ACK ----------> │
  │                      │
  │ ===== Data ========> │
```

This beginning is the TCP **three-way handshake**.

**UDP** is connectionless and has lower protocol overhead.

```text
Client ---- Data ----> Server
Client ---- Data ----> Server
```

Examples commonly associated with UDP include DNS queries, streaming, voice/video traffic, and gaming, depending on the application protocol.

## 13. OSI Model

The OSI model is important for understanding and troubleshooting networking.

```text
7  Application     HTTP, DNS, SSH
6  Presentation    Encoding, encryption concepts
5  Session         Session management
4  Transport       TCP, UDP
3  Network         IP, routing
2  Data Link       Ethernet, MAC
1  Physical        Cable, radio, signals
```

A useful learning path is:

```text
Application
     ↓
TCP / UDP
     ↓
IP
     ↓
Ethernet / Wi-Fi
     ↓
Physical Network
```

## 14. How a Website Request Works

Suppose you open:

```text
https://example.com
```

A simplified flow is:

```text
Browser
   │
   ▼
DNS Lookup
   │
   ▼
Server IP
   │
   ▼
Routing / Gateway
   │
   ▼
Internet
   │
   ▼
Web Server :443
   │
   ▼
HTTPS Response
   │
   ▼
Browser
```

There are additional details such as ARP/neighbor discovery, TCP or QUIC, TLS, NAT, routing, and caching, but this is a good starting mental model.

## 15. Important Linux Networking Commands

```bash
ip addr
ip link
ip route
ping google.com
ss -tulpn
ip neigh
traceroute google.com
nslookup google.com
dig google.com
curl https://example.com
```

For modern Linux, prioritize the `ip` and `ss` commands over older commands such as `ifconfig`, `route`, and `netstat`.

## Recommended Learning Order

```text
Networking
   ↓
LAN / WAN
   ↓
IP Addressing
   ↓
Subnet Mask & CIDR
   ↓
MAC + ARP
   ↓
Switching
   ↓
Routing + Gateway
   ↓
DNS + DHCP
   ↓
TCP / UDP + Ports
   ↓
OSI & TCP/IP Models
   ↓
NAT + Firewall
   ↓
Linux Networking Commands
   ↓
Cloud Networking
   ↓
AWS VPC / Azure VNet / Kubernetes Networking
```

For **Linux, DevOps and Cloud**, the most important foundations are **IP addressing, subnetting, DNS, ports, TCP/UDP, routing, NAT, firewalls and troubleshooting commands**.
