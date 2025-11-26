# Linux Project (NGINX WebServer)

**“Deploy and Manage a Website Using NGINX ”**

At the end of this project, learners will have a fully working NGINX-based website managed entirely via Linux commands.
We will learn:

✔ Install and configure NGINX  
✔ Deploy a custom website  
✔ Work with Linux permissions & users  
✔ Manage and troubleshoot services  
✔ Test and verify networking components  
✔ Write a real-world automation script  


---
# Install NGINX

## Commands

Update packages:
```bash
sudo apt update
````

Install nginx:

```bash
sudo apt install nginx -y
```

Check status:

```bash
systemctl status nginx
```

Access in browser:

```
http://<server-ip>
```

List NGINX files:

```bash
ls -l /var/www/html
ls -l /etc/nginx
```

---

# Manage Website Files

Default web directory:
````

/var/www/html/

````

Replace default page:
```bash
cd /var/www/html
sudo mv index.nginx-debian.html index_backup.html
sudo vim index.html
````

Add below or refer -> https://github.com/rootpromptnext/linux-workshop/blob/main/sample-index.html

```html
<h1>Welcome to the Linux Workshop Website</h1>
<p>Powered by NGINX</p>
```

Check file permissions:

```bash
ls -l /var/www/html
```

Restart nginx:

```bash
sudo systemctl restart nginx
```
---


# Users & Permissions for Website

Create user:
```bash
sudo useradd webadmin
sudo passwd webadmin
````

Add user to www-data group:

```bash
sudo usermod -aG www-data webadmin
```

Change ownership:

```bash
sudo chown -R webadmin:www-data /var/www/html
```

Set directory permissions:

```bash
sudo chmod -R 755 /var/www/html
```

Test:

```bash
su - webadmin
vim /var/www/html/index.html
```
---

# Manage NGINX Service

Check service:
```bash
systemctl status nginx
````

Start / Stop / Restart:

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
sudo systemctl restart nginx
```

Enable on boot:

```bash
sudo systemctl enable nginx
```

Check running port:

```bash
ss -tulnp | grep 80
```

Check logs:

```bash
sudo journalctl -u nginx --since "10 min ago"
```

---

#  Networking & Troubleshooting

Check IP address:
```bash
ip a
````

Check connectivity:

```bash
ping -c 4 google.com
```

Check DNS:

```bash
nslookup google.com
```

Test local nginx:

```bash
curl http://localhost
```

Check routes:

```bash
ip route
```

Check listening port:

```bash
ss -tulnp | grep nginx
```
---

# NGINX Automation Script

Create script:
```bash
vim nginx_monitor.sh
````

Add:

```bash
#!/bin/bash

SERVICE="nginx"

if systemctl is-active --quiet $SERVICE
then
    echo "$(date): NGINX is running" >> nginx_status.log
else
    echo "$(date): NGINX is DOWN – restarting..." >> nginx_status.log
    sudo systemctl restart $SERVICE
fi
```

Make it executable:

```bash
chmod +x nginx_monitor.sh
```

Run:

```bash
./nginx_monitor.sh
```






