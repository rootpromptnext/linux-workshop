# **Lab 05: Networking Basics (Enhanced)**

## **Objective**

Learn how to inspect Linux network configuration, test connectivity, verify DNS, check routing, and identify open ports and services. Gain hands-on experience troubleshooting basic network issues.

---

## **Topics Covered**

* Viewing IP configuration (`ip`, `ifconfig`)
* Checking link status & interface statistics
* Testing connectivity with `ping`
* DNS lookups (`nslookup`, `dig`)
* Checking routes & gateways
* Finding open ports (`ss`, `netstat`)
* Testing remote port connectivity (`nc`)
* Viewing hostname & hosts file
* Basic troubleshooting steps

---

## **Pre-requisites**

* Linux VM with internet access
* Basic terminal usage

---

# **View Network Interfaces & IP Addresses**

```bash
ip a
```

Check only active interfaces:

```bash
ip -br a
```

Legacy tool (if installed):

```bash
ifconfig
```

---

# **View Routing Table**

```bash
ip route
```

Check the default gateway:

```bash
ip route | grep default
```

---

# **Check Link Status & Statistics**

Check if cable/virtual NIC is up/down:

```bash
ip link
```

View interface statistics:

```bash
ip -s link
```

---

# **Test Network Connectivity**

Ping a public domain:

```bash
ping -c 4 google.com
```

Ping an IP directly:

```bash
ping -c 4 8.8.8.8
```

> If `google.com` fails but `8.8.8.8` works → DNS issue.

---

# **DNS Lookup**

Using `nslookup`:

```bash
nslookup google.com
```

Using `dig` (if available):

```bash
dig google.com
dig +short google.com
```

Check DNS server being used:

```bash
cat /etc/resolv.conf
```

---

# **Identify Listening Ports & Active Connections**

Modern recommended tool:

```bash
ss -tulnp
```

Breakdown:

* `t` → TCP
* `u` → UDP
* `l` → listening
* `n` → numeric
* `p` → show process

Older tool:

```bash
netstat -tulnp
```

List TCP connections:

```bash
ss -tn
```

List UDP ports:

```bash
ss -un
```

---

# **Test Port Connectivity**

Check if a remote port is open:

```bash
nc -zv google.com 80
```

Check a local port:

```bash
nc -zv 127.0.0.1 22
```

Test manually by connecting (useful for debugging services):

```bash
nc google.com 80
```

---

# **Check Hostname & Hosts File**

```bash
hostname
hostname -I
cat /etc/hosts
```

Add a manual hostname entry (example):

```bash
sudo nano /etc/hosts
```

---

# **Verify External IP**

```bash
curl ifconfig.me
```

---

# **ARP Table (Local Network Discovery)**

```bash
ip neigh
```

---

# **Tips**

### If **ping google.com** fails:

* Check interface status:

  ```bash
  ip a
  ```
* Check if default gateway exists:

  ```bash
  ip route
  ```
* Test DNS resolution:

  ```bash
  nslookup google.com
  ```

### If a service is not reachable:

* Check if service is running:

  ```bash
  systemctl status <service>
  ```
* Check if it’s listening on the port:

  ```bash
  ss -tulnp | grep <port>
  ```

### Quick network reset (Ubuntu):

```bash
sudo systemctl restart NetworkManager
```

