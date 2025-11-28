# **Lab 03: Users, Groups & Permissions**

## **Objective**

Learn how Linux manages users, groups, and permissions. Understand ownership, access control, numeric vs symbolic permissions, switching users, and basic privilege escalation.

---

## **Topics Covered**

* User & group creation
* Adding users to groups
* Understanding `/etc/passwd`, `/etc/shadow`, `/etc/group`
* File ownership (user/group)
* Permission types: read, write, execute
* Numeric (chmod 755) vs symbolic (u+rwx) permissions
* Changing ownership & group (chown, chgrp)
* Checking effective permissions
* Switching users (su)
* Using `sudo` (view privileges)

---

## **Pre-requisites**

* Linux VM
* Sudo access
* Basic command-line navigation

---

# **Create a New User**

```bash
sudo useradd -m -s /bin/bash labuser
sudo passwd labuser
```

Check if user created properly:

```bash
grep labuser /etc/passwd
```

---

# **Create a New Group and Add User to It**

```bash
sudo groupadd devgroup
sudo usermod -aG devgroup labuser
```

Verify:

```bash
id labuser
groups labuser
```

> **Note:** User must log out & log back in for group changes to take effect.

---

# **Inspect System User & Group Files**

```bash
cat /etc/passwd    # basic user database
sudo cat /etc/shadow   # password hashes (root only)
cat /etc/group     # group membership
```

---

# **Create a File and Check Permissions**

```bash
touch testfile.txt
ls -l testfile.txt
```

Example output:

```
-rw-r--r-- 1 ubuntu ubuntu 0 Feb 19 testfile.txt
```

Breakdown:

| Part          | Meaning            |
| ------------- | ------------------ |
| rw-           | User permissions   |
| r--           | Group permissions  |
| r--           | Others permissions |
| ubuntu ubuntu | Owner and group    |

---

# **Modify Permissions (Symbolic Mode)**

```bash
chmod u+rwx testfile.txt
chmod g+rw testfile.txt
chmod o-r testfile.txt
```

Check:

```bash
ls -l testfile.txt
```

---

# **Modify Permissions (Numeric Mode)**

```bash
chmod 754 testfile.txt
```

This changes to:

| Entity | Code | Meaning |
| ------ | ---- | ------- |
| User   | 7    | rwx     |
| Group  | 5    | r-x     |
| Others | 4    | r--     |

---

# **Change Ownership & Group**

```bash
sudo groupadd devgroup
sudo chown labuser testfile.txt
sudo chgrp devgroup testfile.txt
```

Or combine both:

```bash
sudo chown labuser:devgroup testfile.txt
```

---

# **Check Effective Permissions Using `namei`**

```bash
namei -l testfile.txt
```

This shows **permissions on every directory in the path**, useful for troubleshooting.

---

# **Switch Users**

Switch to the new user:

```bash
su - labuser
whoami
```

Try accessing the file:

```bash
ls -l /home/ubuntu/testfile.txt   # or correct path
```

Exit back:

```bash
exit
```

---

# **Check sudo Privileges**

```bash
sudo -l
```

This shows what commands the user can run with sudo.

---

# **Tips**

### **Permission numbers (cheat sheet)**

* `7 = rwx`
* `6 = rw-`
* `5 = r-x`
* `4 = r--`
* `0 = ---`

### **Useful permission shortcuts**

```bash
chmod 644 file     # normal text file
chmod 755 script   # executable script
chmod 700 private  # only owner can access
```

### **To apply group changes**

User must **log out and log back in**.


