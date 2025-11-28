# **Lab 06: Shell Scripting Basics**

## **Objective**

Learn the fundamentals of Bash scripting including variables, conditionals, loops, functions, debugging, and automation basics.
By the end of this lab, you should be comfortable writing simple to moderate shell scripts used in DevOps and system administration.

## **Topics Covered**

* What is a shell script and why use it
* Creating & executing bash scripts
* Variables (system, user-defined)
* User input (`read`)
* Arithmetic operations
* Conditional statements (`if`, `elif`, `else`)
* Loops (`for`, `while`, `until`)
* Functions
* Exit codes and `$?`
* Script permissions
* Debugging (`set -x`)

---

## **Pre-requisites**

* Basic Linux usage
* Familiarity with `vim` or any text editor

---

# **Create your first script**

```bash
vim hello.sh
```

Add:

```bash
#!/bin/bash
echo "Hello, Linux Workshop!"
```

Run:

```bash
chmod +x hello.sh
./hello.sh
```

---

# **Variables (simple and dynamic)**

### **Static variable**

```bash
vim variables.sh
```

Add:

```bash
#!/bin/bash
name="Linux User"
course="Shell Scripting"
echo "Welcome, $name! You are learning $course."
```

Run:

```bash
./variables.sh
```

### **Using command substitution**

```bash
today=$(date)
echo "Today is $today"
```

---

# **User input**

```bash
vim input.sh
```

Add:

```bash
#!/bin/bash
echo -n "Enter your name: "
read user
echo "Hello, $user!"
```

Run:

```bash
./input.sh
```

---

# **Arithmetic Operations**

```bash
vim calc.sh
```

Add:

```bash
#!/bin/bash
a=10
b=5

echo "Addition: $((a + b))"
echo "Multiplication: $((a * b))"
```

Run:

```bash
./calc.sh
```

---

# **Conditions (`if/elif/else`)**

```bash
vim check_disk.sh
```

Add:

```bash
#!/bin/bash
usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ $usage -gt 90 ]; then
    echo "CRITICAL: Disk usage above 90%!"
elif [ $usage -gt 70 ]; then
    echo "Warning: Disk usage above 70%."
else
    echo "Disk usage normal."
fi
```
**Short explanation for usage variable:**

```
df -h / | awk 'NR==2 {print $5}' | sed 's/%//'
```

* `df -h /` → shows disk usage of `/`
* `awk 'NR==2 {print $5}'` → picks the **Use%** column from the 2nd line (e.g., `54%`)
* `sed 's/%//'` → removes `%`

**Final output:** only the number → e.g., `54`

---

# **Loops**

## **For loop**

```bash
vim loop.sh
```

Add:

```bash
#!/bin/bash
for i in {1..5}
do
    echo "Count: $i"
done
```

## **While loop**

```bash
vim while.sh
```

Add:

```bash
#!/bin/bash
count=1
while [ $count -le 5 ]
do
    echo "Number: $count"
    count=$((count + 1))
done
```

---

# **Until Loop (Less known but useful)**

```bash
vim until.sh
```

Add:

```bash
#!/bin/bash
x=1
until [ $x -gt 5 ]
do
    echo "Value: $x"
    x=$((x + 1))
done
```

---

# **Functions**

```bash
vim function.sh
```

Add:

```bash
#!/bin/bash

greet() {
    echo "Welcome to the Shell Scripting Lab!"
}

show_date() {
    echo "Today is: $(date)"
}

greet
show_date
```

---

# **Exit Codes and `$?`**

```bash
vim exitcode.sh
```

Add:

```bash
#!/bin/bash

ls /tmp
echo "Exit code of last command: $?"
```

Exit codes tell if a command succeeded:

* `0` → success
* Non-zero → error

---

# **Debugging Your Script**

### **Method 1: Run with debug mode**

```bash
bash -x script.sh
```

### **Method 2: Add inside script**

```bash
set -x   # enable debugging
# your script
set +x   # disable debugging
```

---

# ** Best Practices**

* Always start with:

  ```bash
  #!/bin/bash
  ```
* Use meaningful variable names
* Always handle input validation
* Use comments:

  ```bash
  # This script checks CPU load
  ```
* Test scripts with:

  ```bash
  bash -n script.sh   # syntax check
  ```

