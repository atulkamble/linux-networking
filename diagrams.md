 # 🌐 Basic Networking Diagrams

Here are the most important networking diagrams for learning Linux, cloud, and DevOps.

## 1. Basic Computer Network

```text
┌────────────┐
│ Computer A │
│192.168.1.10│
└─────┬──────┘
      │
      │ Ethernet / Wi-Fi
      │
┌─────▼──────┐
│   Switch   │
└─────┬──────┘
      │
┌─────▼──────┐
│ Computer B │
│192.168.1.20│
└────────────┘
```

**Network:** A group of devices connected so they can communicate and share resources.

---

## 2. LAN — Local Area Network

```text
 PC-1             PC-2
192.168.1.10    192.168.1.20
   │                 │
   └──────┐   ┌──────┘
          │   │
       ┌──▼───▼──┐
       │  Switch │
       └────┬────┘
            │
       ┌────▼────┐
       │ Router  │
       └─────────┘
```

**LAN:** A network connecting devices within a small geographical area such as a home, office, or lab.

---

## 3. Switch

```text
        ┌──────────────┐
        │    Switch    │
        └─┬───┬───┬───┘
          │   │   │
     ┌────┘   │   └────┐
     │        │        │
   PC-1     PC-2     Server
```

A **switch** connects devices inside the same LAN.

It mainly works using **MAC addresses**.

---

## 4. Router

```text
      LAN 1
192.168.1.0/24
      │
┌─────▼─────┐
│  Router   │
└─────┬─────┘
      │
      │
      ▼
   Internet
      │
┌─────▼─────┐
│  Router   │
└─────┬─────┘
      │
      LAN 2
10.0.0.0/24
```

A **router** connects different networks and forwards packets using **IP addresses**.

---

## 5. Home / Office Network

```text
 Laptop ──┐
          │
 Mobile ──┼── Wi-Fi
          │
 Printer ─┘
          │
     ┌────▼─────┐
     │  Router  │
     │ / Wi-Fi  │
     └────┬─────┘
          │
        Modem
          │
          ▼
       Internet
```

---

## 6. IP Address and Subnet

```text
IP Address
192.168.1.10
     │
     ├──────── Network
     │
     └──────── Host
```

For:

```text
192.168.1.10/24
```

Think of it as:

```text
Network Address : 192.168.1.0
Subnet Mask     : 255.255.255.0
Host Range      : 192.168.1.1 - 192.168.1.254
Broadcast       : 192.168.1.255
```

Diagram:

```text
192.168.1.0/24

        Switch
          │
 ┌────────┼────────┐
 │        │        │
 ▼        ▼        ▼
.10      .20      .30
PC       PC      Server
```

---

## 7. Default Gateway

```text
Linux PC
192.168.1.10
     │
     │
     ▼
Default Gateway
192.168.1.1
     │
     ▼
  Internet
```

The **default gateway** is the router a device sends traffic to when the destination is outside its local network.

Example:

```text
PC
192.168.1.10
     │
     │ Destination: 8.8.8.8
     ▼
Gateway
192.168.1.1
     │
     ▼
Internet
```

---

## 8. DNS

```text
User
 │
 │ google.com
 ▼
DNS Server
 │
 │ 142.x.x.x
 ▼
User
 │
 │ Connect using IP
 ▼
Google Server
```

**DNS — Domain Name System**

It converts:

```text
google.com
     ↓
IP Address
```

Useful Linux commands:

```bash
nslookup google.com
dig google.com
host google.com
```

---

## 9. DHCP

```text
       DHCP Server
     192.168.1.1
          │
          │ Assign IP
          ▼
      Linux PC
          │
          ▼
IP      : 192.168.1.10
Mask    : 255.255.255.0
Gateway : 192.168.1.1
DNS     : 8.8.8.8
```

**DHCP** automatically provides network configuration to devices.

---

## 10. MAC Address vs IP Address

```text
Application
    │
    ▼
IP Address
192.168.1.10
    │
    ▼
MAC Address
AA:BB:CC:DD:EE:FF
    │
    ▼
Network Interface
    │
    ▼
Ethernet / Wi-Fi
```

**IP address** identifies a device logically across networks.

**MAC address** identifies a network interface on the local network.

---

## 11. Client-Server Architecture

```text
             Internet
                │
       ┌────────┴────────┐
       │                 │
   Client-1          Client-2
   Browser           Browser
       │                 │
       └────────┬────────┘
                │
                ▼
         ┌────────────┐
         │ Web Server │
         │   Nginx    │
         │   Apache   │
         └─────┬──────┘
               │
               ▼
         ┌────────────┐
         │  Database  │
         └────────────┘
```

The **client** requests a service, while the **server** provides it.

---

## 12. Ports

```text
                    Linux Server
                 192.168.1.100
                        │
       ┌────────────────┼────────────────┐
       │                │                │
       ▼                ▼                ▼
    Port 22           Port 80          Port 443
      SSH               HTTP             HTTPS
```

Common ports:

| Port | Protocol   | Purpose         |
| ---: | ---------- | --------------- |
|   22 | SSH        | Remote login    |
|   53 | DNS        | Name resolution |
|   80 | HTTP       | Website         |
|  443 | HTTPS      | Secure website  |
| 3306 | MySQL      | Database        |
| 5432 | PostgreSQL | Database        |

---

## 13. TCP Connection

```text
Client                         Server
  │                              │
  │ -------- SYN --------------> │
  │                              │
  │ <----- SYN + ACK ----------- │
  │                              │
  │ -------- ACK --------------> │
  │                              │
  │      Connection Ready        │
  │ <==========================> │
```

This is the **TCP three-way handshake**.

---

## 14. Firewall

```text
                 Internet
                    │
                    ▼
             ┌────────────┐
             │  Firewall  │
             └─────┬──────┘
                   │
       ┌───────────┼───────────┐
       │           │           │
    SSH :22     HTTP :80    MySQL :3306
    Allow       Allow        Deny
       │           │
       ▼           ▼
             Linux Server
```

A firewall controls which network traffic is allowed or denied.

---

## 15. NAT

```text
Private Network

192.168.1.10 ──┐
192.168.1.20 ──┼──► Router/NAT ──► Internet
192.168.1.30 ──┘       │
                       ▼
                  Public IP
                203.0.113.10
```

**NAT — Network Address Translation** allows private IP devices to communicate with external networks through a public IP.

---

## 16. OSI Model

```text
┌──────────────────────────┐
│ 7  Application           │ ← HTTP, DNS, SSH
├──────────────────────────┤
│ 6  Presentation          │
├──────────────────────────┤
│ 5  Session               │
├──────────────────────────┤
│ 4  Transport             │ ← TCP / UDP
├──────────────────────────┤
│ 3  Network               │ ← IP / Router
├──────────────────────────┤
│ 2  Data Link             │ ← MAC / Switch
├──────────────────────────┤
│ 1  Physical              │ ← Cable / Signals
└──────────────────────────┘
```

For practical Linux networking, remember:

```text
Application     HTTP / SSH / DNS
      ↓
Transport       TCP / UDP + Ports
      ↓
Network         IP + Router
      ↓
Data Link       MAC + Switch
      ↓
Physical        Ethernet / Wi-Fi
```

## Big Picture

```text
                     INTERNET
                         │
                         ▼
                  ┌────────────┐
                  │ ISP/Modem  │
                  └─────┬──────┘
                        │
                  ┌─────▼──────┐
                  │   Router   │
                  │ Gateway/NAT│
                  └─────┬──────┘
                        │
                  ┌─────▼──────┐
                  │   Switch   │
                  └──┬──┬──┬──┘
                     │  │  │
          ┌──────────┘  │  └──────────┐
          ▼             ▼             ▼
      Linux PC       Windows PC     Server
    192.168.1.10    192.168.1.20  192.168.1.30
                                      │
                              ┌───────┼───────┐
                              ▼       ▼       ▼
                            SSH      HTTP    HTTPS
                            :22      :80      :443
```

### Recommended learning order

**Network → LAN/WAN → IP Address → Subnet Mask → MAC → Switch → Router → Gateway → DNS → DHCP → Ports → TCP/UDP → NAT → Firewall → Routing → OSI/TCP-IP → Linux networking commands**

![Image](https://images.openai.com/static-rsc-4/4qQ86akLTNfA4hpi8LcSGnulCvi612LwDMBfGRiFXLwGHijE7xf5RVx0DQWH7cDJqk2p3x_qzn8DD9iy-RmzL9tzvl5Sd09XoLaaQZ3-DdCVOs5hJNjb-7241O5sgeNfu7GSSbOaz2iAR6Gy2jU_V7XH_ofHRJE6YtPVKgV1d5AmgPiTgJJNORjT2jw6mHsv?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/VxMA25tR_s0zFat2X5erQo5FTkA0VovvH1vlizXEPtjPXS4NTT-5Px8zHP9FLg7pWmmVDeKhofKXGPVKVR5VO_13veqj2xLcq4gjnAO7b0tTNQjRnViKqRUrr7cT5fJ3F8ydm7SjnI3_-znCvOEg7kxU6TKD758dUFxRE0lsH2bb9uL-YtXxNmqnHcfyfCCw?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/OICL7I8uJKRtJ_7IQep1bFgH9DeOUvaQ1vV_qAQQK23JAS25yiqOS51VOC62qrR1hX_owXxBeiuu6D6ijT3HCdVHGaF-obhQLLgy5dep3L55831L0HSUQlK4Exte9IoqgtO6nMliG6YyPVB5pHFczTPHPnwUW6R09a1QUKvuWcAMzw3r0z9Q-rl9t9WCJVvt?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/AbE62OjNffQ7FswaSY8eZIt1BUq8xHWGG7DT2K4nRA18NFr7J0oZtTF0mzZoP5QHdFe5zXv9bjWSRCEZku4UyEnuhD43iTe6jeqKUPSJBir1yXQr47ACKkLHIq_6a4vMtOEaRZUKeg3BTsexlWUE8QwMO76mpisQ55KNV2iF6Y7aJ0WJqOo4Ax5AjmrE7XiR?purpose=fullsize)
