# Linux Networking Commands

Here are the most important Linux networking commands, arranged from basic to troubleshooting.

| Command       | Purpose                            | Example                         |
| ------------- | ---------------------------------- | ------------------------------- |
| `ip addr`     | Show IP addresses/interfaces       | `ip addr`                       |
| `ip link`     | Show network interfaces            | `ip link`                       |
| `ip route`    | Show routing table/default gateway | `ip route`                      |
| `hostname`    | Show hostname                      | `hostname`                      |
| `hostname -I` | Show system IP addresses           | `hostname -I`                   |
| `ping`        | Test connectivity                  | `ping google.com`               |
| `ss`          | Show ports/connections             | `ss -tulnp`                     |
| `curl`        | Test HTTP/HTTPS services           | `curl https://example.com`      |
| `wget`        | Download/test web resources        | `wget https://example.com/file` |
| `nslookup`    | DNS lookup                         | `nslookup google.com`           |
| `dig`         | Detailed DNS lookup                | `dig google.com`                |
| `traceroute`  | Trace network path                 | `traceroute google.com`         |
| `tracepath`   | Trace path without root            | `tracepath google.com`          |
| `arp`         | View ARP table (older)             | `arp -a`                        |
| `ip neigh`    | View neighbor/ARP table            | `ip neigh`                      |
| `nmcli`       | Manage NetworkManager              | `nmcli device status`           |
| `ethtool`     | Ethernet/interface details         | `ethtool eth0`                  |
| `tcpdump`     | Capture network packets            | `sudo tcpdump -i eth0`          |
| `lsof`        | Check processes using ports        | `sudo lsof -i :80`              |
| `nc`          | Test TCP/UDP ports                 | `nc -zv server 80`              |

## 1. IP Address and Interfaces

```bash
ip addr
```

Short form:

```bash
ip a
```

Example output:

```text
eth0
 └── 192.168.1.10/24
```

Show only IP addresses:

```bash
hostname -I
```

Show interfaces:

```bash
ip link
```

Bring an interface up/down:

```bash
sudo ip link set eth0 up
sudo ip link set eth0 down
```

## 2. Connectivity Testing

```bash
ping google.com
```

Send only 4 packets:

```bash
ping -c 4 google.com
```

Concept:

```text
Linux Machine
     |
     | ICMP
     ↓
   Router
     |
     ↓
  Internet
     |
     ↓
google.com
```

A successful `ping` generally confirms basic IP connectivity to the destination.

## 3. Routing Commands

Show routing table:

```bash
ip route
```

or:

```bash
ip r
```

Typical output:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0
```

Concept:

```text
Linux
192.168.1.10
    |
    ↓
Gateway
192.168.1.1
    |
    ↓
 Internet
```

## 4. DNS Commands

Basic DNS lookup:

```bash
nslookup google.com
```

More detailed lookup:

```bash
dig google.com
```

Check configured DNS servers:

```bash
cat /etc/resolv.conf
```

DNS flow:

```text
google.com
    ↓
DNS Server
    ↓
142.x.x.x
```

## 5. Ports and Connections

One of the most useful commands:

```bash
ss -tulnp
```

Meaning:

```text
-t  TCP
-u  UDP
-l  Listening
-n  Numeric ports
-p  Process
```

For example, check port `80`:

```bash
sudo ss -tulnp | grep :80
```

Another useful command:

```bash
sudo lsof -i :80
```

This is especially useful when Apache or Nginx cannot start because another process is already using port 80.

## 6. Test a Web Server

```bash
curl http://localhost
```

Check headers:

```bash
curl -I https://google.com
```

Verbose troubleshooting:

```bash
curl -v https://example.com
```

## 7. Test Whether a Port Is Reachable

```bash
nc -zv google.com 443
```

Test a server:

```bash
nc -zv 192.168.1.10 22
```

Concept:

```text
Client
  |
  | TCP :22
  ↓
Server
  |
  └── SSH
```

## 8. Trace Network Path

```bash
traceroute google.com
```

or:

```bash
tracepath google.com
```

Concept:

```text
Your Linux
    ↓
Router
    ↓
ISP Router
    ↓
Internet Routers
    ↓
Destination
```

## 9. ARP / Neighbor Information

Modern command:

```bash
ip neigh
```

Example:

```text
192.168.1.1 dev eth0 lladdr aa:bb:cc:dd:ee:ff REACHABLE
```

It helps map local-network IP addresses to MAC addresses.

## 10. Packet Capture

Capture packets:

```bash
sudo tcpdump
```

Specific interface:

```bash
sudo tcpdump -i eth0
```

Specific port:

```bash
sudo tcpdump -i eth0 port 80
```

## Recommended Learning Order

For Linux networking practice, learn these first:

```text
ip addr
   ↓
ip link
   ↓
ip route
   ↓
ping
   ↓
nslookup / dig
   ↓
ss
   ↓
curl
   ↓
nc
   ↓
traceroute
   ↓
ip neigh
   ↓
tcpdump
```

The **five commands to master first** are `ip addr`, `ip route`, `ping`, `ss -tulnp`, and `curl`. These cover IP configuration, routing, connectivity, ports, and application-level testing.
