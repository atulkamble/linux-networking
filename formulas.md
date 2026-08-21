# Linux Networking Formulas — Quick Study Guide

For Linux networking, the most useful formulas are mainly related to **IPv4 addressing, subnetting, CIDR, hosts, network/broadcast addresses, and bandwidth**.

## 1. IPv4 Address Size

IPv4 contains **32 bits**:

```text
8 bits + 8 bits + 8 bits + 8 bits = 32 bits
```

Example:

```text
192.168.1.10

192      168      1        10
11000000 10101000 00000001 00001010
```

## 2. CIDR Formula

CIDR tells you how many bits belong to the **network portion**.

```text
/24 = 24 Network Bits
```

Therefore:

```text
Host Bits = 32 - CIDR
```

Example:

```text
192.168.1.0/24

Host Bits = 32 - 24
          = 8
```

## 3. Total Number of IP Addresses

```text
Total IPs = 2^HostBits
```

Example `/24`:

```text
Host Bits = 8

Total IPs = 2^8
          = 256
```

## 4. Usable Host Formula

Traditionally:

```text
Usable Hosts = 2^HostBits - 2
```

We subtract:

```text
1 → Network Address
1 → Broadcast Address
```

Example `/24`:

```text
2^8 - 2
= 256 - 2
= 254 hosts
```

> `/31` and `/32` are special cases, so the `-2` formula does not universally apply.

## 5. Network Address Formula

Binary formula:

```text
Network Address = IP Address AND Subnet Mask
```

Example:

```text
IP:          192.168.1.50
Mask:        255.255.255.0
             ----------------
Network:     192.168.1.0
```

Linux:

```bash
ipcalc 192.168.1.50/24
```

## 6. Broadcast Address Formula

Conceptually:

```text
Broadcast = Network Address + Total IPs - 1
```

Example:

```text
192.168.1.0/24

Network     = 192.168.1.0
Total IPs   = 256

Broadcast   = 192.168.1.255
```

Therefore:

```text
192.168.1.0    → Network
192.168.1.1    → First Host
...
192.168.1.254  → Last Host
192.168.1.255  → Broadcast
```

## 7. First and Last Usable IP

For conventional subnets:

```text
First Host = Network Address + 1
```

```text
Last Host = Broadcast Address - 1
```

Example:

```text
Network:    10.0.0.0
Broadcast:  10.0.0.255

First Host: 10.0.0.1
Last Host:  10.0.0.254
```

## 8. Subnet Mask from CIDR

Common values:

|  CIDR | Subnet Mask     |  Total IPs | Traditional Usable Hosts |
| ----: | --------------- | ---------: | -----------------------: |
|  `/8` | 255.0.0.0       | 16,777,216 |               16,777,214 |
| `/16` | 255.255.0.0     |     65,536 |                   65,534 |
| `/24` | 255.255.255.0   |        256 |                      254 |
| `/25` | 255.255.255.128 |        128 |                      126 |
| `/26` | 255.255.255.192 |         64 |                       62 |
| `/27` | 255.255.255.224 |         32 |                       30 |
| `/28` | 255.255.255.240 |         16 |                       14 |
| `/29` | 255.255.255.248 |          8 |                        6 |
| `/30` | 255.255.255.252 |          4 |                        2 |
| `/31` | 255.255.255.254 |          2 |                  special |
| `/32` | 255.255.255.255 |          1 |              single host |

A very useful sequence to memorize:

```text
/24 → 256
/25 → 128
/26 → 64
/27 → 32
/28 → 16
/29 → 8
/30 → 4
```

Each additional CIDR bit **halves the subnet size**.

## 9. Number of Subnets

When borrowing host bits:

```text
Number of Subnets = 2^BorrowedBits
```

Example:

```text
Original = /24
New      = /27

Borrowed Bits = 27 - 24
              = 3

Subnets = 2^3
        = 8
```

So a `/24` can be divided into:

```text
8 × /27 networks
```

## 10. Block Size Formula

A useful subnetting shortcut:

```text
Block Size = 256 - Relevant Mask Octet
```

Example `/26`:

```text
Mask = 255.255.255.192

256 - 192 = 64
```

Networks therefore increment by 64:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

## 11. Bandwidth Conversion

```text
1 Byte = 8 bits
```

Therefore:

```text
Bytes/sec = bits/sec ÷ 8
```

Example:

```text
100 Mbps ÷ 8
≈ 12.5 MB/s
```

Ignoring protocol overhead:

```text
1 Gbps ÷ 8
≈ 125 MB/s
```

## 12. Transmission Time

Approximate formula:

```text
Time = Data Size / Transfer Rate
```

Make sure both values use compatible units.

Example:

```text
File = 100 MB
Network = 100 Mbps
```

Convert:

```text
100 MB × 8 = 800 Mb

Time = 800 Mb / 100 Mbps
     = 8 seconds
```

This is the theoretical minimum; real transfers have overhead and other limitations.

## Most Important Formulas to Memorize

```text
Host Bits = 32 - CIDR

Total IPs = 2^HostBits

Traditional Usable Hosts = 2^HostBits - 2

Network = IP AND Subnet Mask

Broadcast = Network + Total IPs - 1

First Host = Network + 1

Last Host = Broadcast - 1

Subnets = 2^BorrowedBits

Block Size = 256 - Mask Octet

1 Byte = 8 bits

Transfer Time = Data Size / Transfer Rate
```

### Example: `192.168.10.0/27`

```text
Host Bits = 32 - 27
          = 5

Total IPs = 2^5
          = 32

Usable Hosts = 32 - 2
             = 30

Subnet Mask = 255.255.255.224

Block Size = 256 - 224
           = 32
```

So the first subnet is:

```text
Network:     192.168.10.0
First Host:  192.168.10.1
Last Host:   192.168.10.30
Broadcast:   192.168.10.31
```

The next subnet begins at:

```text
192.168.10.32/27
```

These subnetting formulas are particularly useful with Linux commands such as `ip addr`, `ip route`, `ipcalc`, `ping`, `traceroute`, `ss`, and `netstat`.
