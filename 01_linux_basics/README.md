# **Lab 01: Linux Basics (Enhanced)**

## **Objective**

Understand fundamental Linux commands, system information, basic navigation, user session details, processes, and help utilities.

## **Topics Covered**

* Terminal basics and navigation
* File system hierarchy
* Linux version, kernel & system info
* User/session information
* Process monitoring basics
* Package info basics
* Help & manual pages
* Network basics (very light)

---

## **Pre-requisites**

* Linux VM/server
* Terminal access (SSH/local)

---

# **Commands & Concepts**

---

## **Explore the Current Directory**

```bash
pwd
ls -l
```

---

## **Navigate the File System**

```bash
cd /home
cd ..
cd /tmp
```

---

## **List Hidden Files & Human-friendly Output**

```bash
ls -a
ls -lh
```

---

## **Check Linux Version, Distro & Kernel**

```bash
uname -a
cat /etc/os-release
hostnamectl
```

---

## **Check System Date & Uptime**

```bash
date
uptime
```

---

## **Check Logged-in Users & Your Username**

```bash
whoami
who
w
```

---

## **Check System Resource Usage**

**Disk usage:**

```bash
df -h
du -sh *
```

**Memory & CPU quick overview:**

```bash
free -h
top
```

(exit top using **q**)

---

## **Get Process Information**

```bash
ps
ps aux | head
```

**Check your own processes:**

```bash
ps -u $USER
```

---

## **Check Running Services (systemd)**

```bash
systemctl list-units --type=service --state=running
```

---

## **Basic Package Information (No installation)**

**Check package manager:**

```bash
which apt
which yum
which dnf
```

**Check if a package exists (example: curl):**

```bash
apt show curl 2>/dev/null
rpm -qi curl 2>/dev/null
```

---

## **Check Network Basics**

**IP address:**

```bash
ip a
```

**Routing table:**

```bash
ip route
```

**Check open ports (quick):**

```bash
ss -tulpn | head
```

---

## **Check Environment Variables**

```bash
printenv | head
echo $PATH
```

---

## **Use the Linux Help System**

**Manual pages:**

```bash
man ls
man pwd
```

(exit using **q**)

**Quick help:**

```bash
ls --help
cd --help 2>/dev/null
```

---

## **Check System Hardware Information**

**CPU:**

```bash
lscpu
```

**Memory:**

```bash
lsmem
```

**Block devices (disks):**

```bash
lsblk
```


