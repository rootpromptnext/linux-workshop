# **Lab 02: File Management in Linux**

## **Objective**

Learn how to create, view, copy, move, rename, and delete files and directories. Practice searching for files, manipulating text content, using wildcards, and editing files using **Vim**.

---

## **Topics Covered**

* Creating files & directories
* Renaming files/directories
* Copying & moving files
* Deleting files & directories
* Viewing file contents (cat, less, head, tail)
* Searching files (find, grep)
* Using wildcard patterns
* Basic Vim editing
* File permissions quick check (read-only viewing)

---

## **Pre-requisites**

* Understanding of basic navigation (cd, ls, pwd)
* Linux VM or server

---

# **Create Files & Directories**

```bash
mkdir lab2_demo
cd lab2_demo

touch file1.txt file2.txt report.log
mkdir dir1 dir2
```

---

# **Rename Files & Directories**

```bash
mv file1.txt file1_renamed.txt
mv dir1 dir1_backup
```

---

# **Copy and Move Files**

```bash
cp file1_renamed.txt dir2/
mv file2.txt dir2/file2_moved.txt
```

---

# **Delete Files & Directories**

```bash
rm report.log
rm -r dir1_backup
rm -rf dir2   # use carefully
```

---

# **View File Contents**

```bash
echo "Welcome to Linux file management lab" > message.txt

cat message.txt          # View entire file
less message.txt         # Scroll inside file (q to exit)

head -n 5 /etc/passwd    # First 5 lines
tail -n 5 /etc/passwd    # Last 5 lines
```

**Follow live logs (if available):**

```bash
tail -f /var/log/syslog
```

(exit using **Ctrl + C**)

---

# **Work With Wildcards (Pattern Matching)**

```bash
touch app.log app1.log app2.log notes.txt
```

Patterns:

```bash
ls *.log        # All .log files
ls app?.log     # app + 1 character + .log
ls app*.log     # app + anything + .log
```

---

# **Search Files & Text**

### **Search for Files Using `find`**

```bash
find . -name "*.log"
find /etc -type f -name "host*"
```

### **Search Inside Files Using `grep`**

```bash
grep "root" /etc/passwd
grep -i "linux" message.txt     # case-insensitive
```

---

# **Check File Permissions (Basic View Only)**

```bash
ls -l
```

Example output:

```
-rw-r--r-- 1 user user 20 Feb 18  message.txt
```

---

# **Basic Vim Usage (Important for Editing Files)**

## **Open a File**

```bash
vim demo.txt
```

---

## **Insert Mode**

Press:

```
i
```

Now start typing.

---

## **Save & Exit**

| Action              | Command |
| ------------------- | ------- |
| Save file           | `:w`    |
| Quit Vim            | `:q`    |
| Save & quit         | `:wq`   |
| Quit without saving | `:q!`   |

---

## **Delete, Copy, Paste Lines**

| Action        | Key  |
| ------------- | ---- |
| Delete a line | `dd` |
| Copy a line   | `yy` |
| Paste         | `p`  |

---

## **Search Inside Vim**

```
/keyword
```

Jump to next match: `n`

---

## **Undo/Redo**

```
u         # undo
Ctrl + r  # redo
```

---

# **Extra Productivity Commands**

### **Word count**

```bash
wc -l message.txt     # number of lines
wc -w message.txt     # number of words
```

### **Compare two files**

```bash
diff file1_renamed.txt message.txt
```


