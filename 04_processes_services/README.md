# Lab 04: Processes & Services

## Objective
Learn how to view, manage, and control system processes and services in Linux.  
Understand how to monitor system activity, kill processes, and manage services using `systemctl`.

## Topics Covered
- Viewing running processes (`ps`, `top`, `htop`)  
- Killing processes (`kill`, `pkill`)  
- Foreground vs background processes  
- Managing services (`systemctl start/stop/status`)  
- Checking logs (`journalctl`)  

## Pre-requisites
- Basic command line usage  
- A Linux system with systemd (Ubuntu/CentOS)  


### List running processes
```bash
ps aux
ps -ef
````

### Monitor live system activity

```bash
top
# press 'q' to quit
```

### Optional (if installed):

```bash
htop
```

### Start a process and send it to background

```bash
sleep 500 &
jobs
```

### Kill a process by PID

```bash
ps -ef | grep sleep
kill <PID>
```

### Kill processes by name

```bash
pkill sleep
```

### Check service status

```bash
systemctl status ssh
```

### Install nginx

```bash
sudo apt update && sudo apt -y install nginx
sudo systemctl start  nginx
sudo systemctl restart  nginx
```

### Start and stop a service

```bash
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
```

### Enable or disable a service at boot

```bash
sudo systemctl enable ssh
sudo systemctl disable ssh
```

### Check service logs

```bash
sudo journalctl -u ssh --since "10 minutes ago"
```

## Tips

* `kill -9 <PID>` should be last option (force kill)
* Use `systemctl status <service>` anytime a service misbehaves
* Use `journalctl -xe` for detailed error logs
