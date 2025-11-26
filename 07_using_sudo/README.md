# **Lab: Using sudo in Linux**

## Objective

Learn how to run administrative commands using `sudo`, validate sudo permissions, manage privileged commands, and safely perform system-level tasks.

## Topics Covered

* Understanding sudo privileges
* Running commands as root
* Editing system files
* Managing services with sudo
* Switching to root shell
* Adding users to sudo/wheel group

## Pre-requisites

* A Linux VM (Ubuntu/CentOS)
* Non-root user with sudo access
* Terminal or SSH access

---

### Verify sudo access

```bash
sudo -v
groups
```

### Run root-only commands

```bash
sudo ls /root
sudo tail /var/log/syslog   # Ubuntu
sudo tail /var/log/messages # CentOS/RHEL
```

### Install software using sudo

**Ubuntu / Debian**

```bash
sudo apt update
sudo apt install tree -y
```

**CentOS / RHEL**

```bash
sudo yum install tree -y
```

### Edit system files

```bash
sudo nano /etc/hosts
cat /etc/hosts
```

### Manage services with sudo

```bash
sudo systemctl status ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
```

### Switch to root shell

```bash
sudo -i
whoami
exit
```

### Add a new user and provide sudo access

*(Only if you already have sudo)*

Create a user:

```bash
sudo useradd testuser
sudo passwd testuser
```

Add user to sudo/wheel group:

**Ubuntu/Debian**

```bash
sudo usermod -aG sudo testuser
```

**CentOS/RHEL**

```bash
sudo usermod -aG wheel testuser
```

### Safely edit sudo permissions

```bash
sudo visudo
```

Check for:

```
%sudo  ALL=(ALL:ALL) ALL
```
---

## Tips

* Always use `visudo` instead of editing `/etc/sudoers` directly
* Use sudo only when required for system-level tasks
* Every sudo action is logged in `/var/log/auth.log`
* Avoid enabling passwordless sudo unless necessary

