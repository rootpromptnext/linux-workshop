# Lab 03: Users, Groups & Permissions

## Objective
Understand how Linux handles users, groups, permissions, ownership, and access control.  
Learn to create users, assign groups, and modify permissions using `chmod`, `chown`, and `chgrp`.

## Topics Covered
- User and group management  
- File permissions (r, w, x)  
- Numeric vs symbolic permissions  
- Changing file ownership and group  
- Using `sudo` and switching users  

## Pre-requisites
- Basic Linux navigation  
- A Linux VM with sudo privileges  

---
### Create a new user
```bash
sudo useradd labuser
sudo passwd labuser
````

### Create a new group and add the user

```bash
sudo groupadd devgroup
sudo usermod -aG devgroup labuser
```

### Check user and group info

```bash
id labuser
groups labuser
cat /etc/passwd
cat /etc/group
```

### Create files and check permissions

```bash
touch testfile.txt
ls -l testfile.txt
```

### Modify permissions (symbolic)

```bash
chmod u+rwx testfile.txt
chmod g+rw testfile.txt
chmod o-r testfile.txt
```

### Modify permissions (numeric)

```bash
chmod 754 testfile.txt
```

### Change ownership & group

```bash
sudo chown labuser testfile.txt
sudo chgrp devgroup testfile.txt
```

### Test user switching

```bash
su - labuser
ls -l
exit
```

---

## Expected Outcomes

* Understand user & group creation
* Ability to modify permissions using numeric and symbolic modes
* Understand how ownership affects file access
* Confidently use `sudo`, `su`, `chmod`, `chown`, `chgrp`

---

## Tips

* Numeric permissions:

  * `7 = rwx`, `6 = rw-`, `5 = r-x`, `4 = r--`
* If a user is added to a group, they must **logout/login** for changes to apply
