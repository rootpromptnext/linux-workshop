# Lab 02: File Management in Linux

## Objective
Learn how to create, view, copy, move, and delete files and directories using Linux command-line tools.

## Topics Covered
- Creating files & directories  
- Copying, moving, renaming files  
- Deleting files and directories  
- Viewing file contents  
- Using wildcard patterns  

## Pre-requisites
- Basic terminal navigation  
- Access to a Linux VM or server  

### Create files and directories
```bash
mkdir lab2_demo
cd lab2_demo
touch file1.txt file2.txt
mkdir dir1
````

### Copy and move files

```bash
cp file1.txt dir1/
mv file2.txt dir1/file2_renamed.txt
```

### Delete files and directories

```bash
rm file1.txt
rm -r dir1
```

### View file contents

```bash
echo "Welcome to Linux file management lab" > message.txt
cat message.txt
head -n 5 /etc/passwd
tail -n 5 /var/log/syslog  # if available
```

### Work with wildcards

```bash
touch app.log app1.log app2.log notes.txt
ls *.log
ls app?.log
```

