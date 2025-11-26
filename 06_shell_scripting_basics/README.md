# Lab 06: Shell Scripting Basics

## Objective
Learn the fundamentals of Bash shell scripting including variables, conditionals, loops, and script execution.  
By the end of this lab, you will be able to write and run basic automation scripts in Linux.

## Topics Covered
- Creating and executing bash scripts  
- Variables and user input  
- Conditional statements (`if`, `else`)  
- Loops (`for`, `while`)  
- Using functions (optional)  
- Script permissions (`chmod +x`)  

## Pre-requisites
- Basic Linux command usage  
- Text editor knowledge (nano / vim)

---

### Create your first script
```bash
nano hello.sh
````

Add the following:

```bash
#!/bin/bash
echo "Hello, Linux Workshop!"
```

Run it:

```bash
chmod +x hello.sh
./hello.sh
```

### Script with variables

```bash
nano variables.sh
```

Add:

```bash
#!/bin/bash
name="Linux User"
echo "Welcome, $name!"
```

Run:

```bash
./variables.sh
```

### User input script

```bash
nano input.sh
```

Add:

```bash
#!/bin/bash
echo -n "Enter your name: "
read user
echo "Hello, $user!"
```

### Script with conditions

```bash
nano check_disk.sh
```

Add:

```bash
#!/bin/bash
usage=$(df -h / | awk 'NR==2 {print $5}' | sed 's/%//')

if [ $usage -gt 70 ]; then
    echo "Warning: Disk usage is above 70%!"
else
    echo "Disk usage is normal."
fi
```

### Script with loops

```bash
nano loop.sh
```

Add:

```bash
#!/bin/bash
for i in 1 2 3 4 5
do
    echo "Count: $i"
done
```

### Bonus: Function inside script

```bash
nano function.sh
```

Add:

```bash
#!/bin/bash
greet() {
    echo "Welcome to the Shell Scripting Lab!"
}

greet
```
---

## Tips

* Always start scripts with:

  ```bash
  #!/bin/bash
  ```
* Use `bash -x script.sh` for debugging
* Make scripts executable using:

  ```bash
  chmod +x <scriptname>
  ```
