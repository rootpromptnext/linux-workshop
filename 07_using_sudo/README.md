# **Lab: Using `sudo` in Linux (Enhanced Version)**

## **Objective**

Learn how to run administrative commands using `sudo`, validate sudo permissions, understand least-privilege concepts, manage privileged actions, elevate to a root shell safely, and configure sudo access for new users.

## **Topics Covered**

* What is `sudo` and why it’s used
* Checking sudo privileges
* Running administrative commands
* Editing protected system files
* Managing system services
* Switching to root shell
* Granting sudo access to users
* Understanding `sudoers` syntax
* Logging and auditing sudo actions
* Passwordless sudo (optional & risky)

---

## **Pre-requisites**

* A Linux VM (Ubuntu or CentOS)
* A **non-root user** with sudo access
* Terminal or SSH access

---

# **Verify sudo access**

Check if your user is allowed to use sudo:

```bash
sudo -v
```

Check groups:

```bash
groups
```

Typical sudo groups:

* **Ubuntu/Debian:** `sudo`
* **CentOS/RHEL:** `wheel`

---

# **Run root-only commands**

```bash
sudo ls /root
sudo cat /etc/shadow   # Will show permission error if not allowed
```

Check system logs:

Ubuntu:

```bash
sudo tail /var/log/syslog
```

CentOS/RHEL:

```bash
sudo tail /var/log/messages
```

---

# **Installing software using sudo**

### **Ubuntu / Debian**

```bash
sudo apt update
sudo apt install tree -y
```

### **CentOS / RHEL**

```bash
sudo yum install tree -y
```

---

# **Edit system files using sudo**

```bash
sudo nano /etc/hosts
sudo vim /etc/hostname
```

Verify:

```bash
cat /etc/hosts
```

---

# **Manage services with sudo**

Check service status:

```bash
sudo systemctl status ssh
```

Restart:

```bash
sudo systemctl restart ssh
```

Enable on boot:

```bash
sudo systemctl enable ssh
```

List all services:

```bash
sudo systemctl list-units --type=service
```

---

# **Switching to root shell**

Start an interactive root shell:

```bash
sudo -i
```

Verify:

```bash
whoami
```

Exit root:

```bash
exit
```

---

# **Create a user and give sudo access**

**Create a user:**

```bash
sudo useradd testuser
sudo passwd testuser
```

### **Give sudo access:**

Ubuntu/Debian:

```bash
sudo usermod -aG sudo testuser
```

CentOS/RHEL:

```bash
sudo usermod -aG wheel testuser
```

Verify:

```bash
id testuser
```

---

# **Safely edit sudo permissions**

Always use:

```bash
sudo visudo
```

Typical entry:

```
%sudo  ALL=(ALL:ALL) ALL
```

CentOS alternative:

```
%wheel ALL=(ALL) ALL
```

> `visudo` prevents syntax errors that can lock you out of sudo.

---

# **Test sudo restrictions and permissions**

Try a safe command:

```bash
sudo -l
```

This displays what your user *is allowed* or *not allowed* to run.

---

# **Run a single command as another user**

Run as user `www-data` (Ubuntu):

```bash
sudo -u www-data whoami
```

Run a script as another user:

```bash
sudo -u nobody bash -c 'echo Hello'
```

---

# **Sudo security concepts (Important for DevOps)**

### Check sudo logs:

Ubuntu:

```bash
sudo grep sudo /var/log/auth.log
```

CentOS:

```bash
sudo grep sudo /var/log/secure
```

### Why avoid using sudo too often?

* Misuse can damage the system
* Wrong commands may delete/modify config
* Production servers follow least-privilege model

---

# **Passwordless sudo (Use only in automation)**

`visudo` entry:

```
prayag ALL=(ALL) NOPASSWD: ALL
```

> Used in automation tools (Ansible, Jenkins agents), but **never recommended for normal users**.

---

# **BONUS: Time-limited sudo session**

After entering password once, sudo stays active for 5 minutes.
You can reset timer manually:

```bash
sudo -k
```

Or disable timestamp caching completely:

```bash
sudo -k
sudo -v   # Forces password again
```

---

# **Tips & Best Practices**

* Never edit `/etc/sudoers` directly → always use **visudo**
* Give minimal required permissions (principle of least privilege)
* Prefer running **one sudo command** instead of `sudo -i` unless needed
* All sudo commands are logged for auditing
* Avoid passwordless sudo unless for controlled automation


