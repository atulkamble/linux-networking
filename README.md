## 📖 Linux Networking Commands — With Practice Codes

---

### 🔍 1️⃣ View IP Address Information

```bash
ip addr show
```

or

```bash
ifconfig   # (Older systems)
```

**Practice:**
Check your active interfaces and IPs:

```bash
ip addr show | grep inet
```

---

### 📡 2️⃣ Test Network Connectivity (Ping)

```bash
ping google.com
```

**Practice:**
Ping a specific server for 5 packets:

```bash
ping -c 5 8.8.8.8
```

---

### 🌐 3️⃣ Display Routing Table

```bash
ip route show
```

or

```bash
route -n
```

**Practice:**
Check your default gateway:

```bash
ip route | grep default
```

---

### 🔌 4️⃣ Check Open Ports and Listening Services

```bash
netstat -tuln
```

or

```bash
ss -tuln
```

**Practice:**
List all TCP connections:

```bash
ss -tn
```

---

### 🕵️‍♂️ 5️⃣ DNS Lookup

```bash
nslookup google.com
```

or

```bash
dig google.com
```

**Practice:**
Get the A record of a domain:

```bash
dig +short google.com
```

---

### 📞 6️⃣ Trace Network Route

```bash
traceroute google.com
```

**Practice:**
Trace path to Cloudflare DNS:

```bash
traceroute 1.1.1.1
```

---

### 🌍 7️⃣ Download Files via Command Line

```bash
curl -O http://example.com/file.zip
```

or

```bash
wget http://example.com/file.zip
```

**Practice:**
Download a webpage source:

```bash
curl https://example.com
```

---

### 📊 8️⃣ Network Bandwidth Usage

Install:

```bash
sudo yum install -y iperf3
```

**Start a server (on one terminal):**

```bash
iperf3 -s
```

**Run client (on another terminal/server):**

```bash
iperf3 -c <server-ip>
```

---

### 📥 9️⃣ Check Public IP Address

```bash
curl ifconfig.me
```

or

```bash
curl ipinfo.io/ip
```

---

### 🗃️  🔒 10️⃣ Add/Delete Firewall Rules (Firewalld Example)

Check firewalld status:

```bash
sudo systemctl status firewalld
```

Open HTTP port:

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --reload
```

---

### 📡 11️⃣ Enable/Disable Network Interface

Disable eth0:

```bash
sudo ip link set eth0 down
```

Enable eth0:

```bash
sudo ip link set eth0 up
```

---

### 📥 12️⃣ Transfer Files Between Servers (scp)

```bash
scp file.txt user@192.168.1.20:/home/user/
```

**Practice:**
Transfer a local file to a remote server's `/tmp/` directory:

```bash
scp /etc/hosts user@<remote-ip>:/tmp/
```

---

## 📦 Bonus: Create a Simple Networking Script

A bash script to check if a list of hosts is reachable:

**Create `ping_hosts.sh`**

```bash
#!/bin/bash
for ip in "8.8.8.8" "1.1.1.1" "google.com"
do
  ping -c 2 $ip &> /dev/null
  if [ $? -eq 0 ]; then
    echo "$ip is reachable"
  else
    echo "$ip is NOT reachable"
  fi
done
```

**Run it**

```bash
bash ping_hosts.sh
```

---
