# Lab 05: Networking Basics

## Objective
Understand basic Linux networking commands to inspect network interfaces, test connectivity, check routes, and identify open ports and services.

## Topics Covered
- Checking IP configuration  
- Testing connectivity (ping)  
- DNS lookup (nslookup, dig if available)  
- Checking routes  
- Viewing open ports and connections (`ss`, `netstat`)  
- Basic troubleshooting  

## Pre-requisites
- Linux VM with internet access  
- Basic command-line knowledge  

---
### View network interfaces & IP addresses
```bash
ip a
````

If using legacy tools:

```bash
ifconfig
```

### 2. View current routing table

```bash
ip route
```

### Test connectivity to a server

```bash
ping -c 4 google.com
```

### Check DNS resolution

```bash
nslookup google.com
```

If `dig` is installed:

```bash
dig google.com
```

### Check active ports and listening services

```bash
ss -tulnp
```

Or older tool:

```bash
netstat -tulnp
```

### Test port connectivity using telnet or nc

```bash
nc -zv google.com 80
```

### Verify hostname and hosts file

```bash
hostname
cat /etc/hosts
```
---

## Tips

* If `ping` fails:

  * Check network interface status using `ip a`
  * Check DNS using `nslookup`
  * Check gateway using `ip route`
* Use `ss -tulnp` to quickly find which service is listening on which port

