Here is the **enhanced and complete version of Lab 04**, matching the improved quality of your previous labs — clearer, more structured, and with extra useful commands/features.

---

# **Lab 04: Processes & Services (Enhanced)**

## **Objective**

Understand how Linux manages running programs and background tasks. Learn how to list, monitor, kill, and control processes, and how to manage system services using **systemd** tools (`systemctl`, `journalctl`).

---

## **Topics Covered**

* Viewing processes (`ps`, `top`, `htop`)
* Monitoring real-time CPU & memory usage
* Foreground vs background jobs
* Killing processes (`kill`, `pkill`)
* Checking open ports & process owners
* Managing services (`systemctl start/stop/enable`)
* Viewing logs via `journalctl`

---

## **Pre-requisites**

* Basic command-line understanding
* Linux VM with **systemd** (Ubuntu/CentOS/RHEL/Rocky)

---

# **1. List Running Processes**

Two common process listing formats:

```bash
ps aux     # BSD style
ps -ef     # Unix style
```

Filter specific processes:

```bash
ps aux | grep ssh
```

---

# **2. Monitor Live System Activity**

```bash
top
```

Press inside **top**:

| Key | Action         |
| --- | -------------- |
| `q` | quit           |
| `k` | kill process   |
| `M` | sort by memory |
| `P` | sort by CPU    |

### Optional (if installed)

```bash
htop
```

(Scroll, search with `/`, kill processes using F9)

---

# **3. Check Which Processes Are Listening on Ports**

```bash
sudo ss -tulnp
```

or

```bash
sudo lsof -i -P -n
```

---

# **4. Foreground vs Background Processes**

Start a long-running process:

```bash
sleep 500
```

**Send to background** (press `Ctrl + Z`):

```bash
bg
```

Run directly in background:

```bash
sleep 500 &
```

List background jobs:

```bash
jobs
```

Bring a job back to foreground:

```bash
fg %1
```

---

# **5. Kill a Process**

### Kill by PID:

```bash
ps -ef | grep sleep
kill <PID>
```

### Kill by name:

```bash
pkill sleep
```

### Kill forcefully (use only if needed):

```bash
kill -9 <PID>
```

---

# **6. Manage Services Using systemctl**

### Check service status:

```bash
systemctl status ssh
```

### Start, stop, restart a service:

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
```

### Check if service is running:

```bash
systemctl is-active nginx
```

### Check if service is enabled at boot:

```bash
systemctl is-enabled nginx
```

---

# **7. Install and Work With NGINX (Example Service)**

```bash
sudo apt update && sudo apt -y install nginx
sudo systemctl start nginx
sudo systemctl restart nginx
sudo systemctl stop nginx
```

---

# **8. Enable or Disable a Service at Boot**

```bash
sudo systemctl enable ssh
sudo systemctl disable ssh
```

---

# **9. View Logs Using journalctl**

### View logs for a specific service:

```bash
sudo journalctl -u ssh
```

Limit time:

```bash
sudo journalctl -u ssh --since "10 minutes ago"
```

Follow logs live (like `tail -f`):

```bash
sudo journalctl -u ssh -f
```

View detailed errors:

```bash
sudo journalctl -xe
```

---

# **Extra Commands (Very Useful)**

### Show top 10 memory-consuming processes:

```bash
ps aux --sort=-%mem | head
```

### Show top 10 CPU-consuming processes:

```bash
ps aux --sort=-%cpu | head
```

### Kill all processes owned by a user:

```bash
sudo pkill -u username
```

---

# **Tips**

* Use `kill -9` only if normal `kill` fails
* Use `top` or `htop` when diagnosing high CPU/memory issues
* Always run `systemctl status <service>` when a service fails
* `journalctl -xe` gives detailed logs for failed units


