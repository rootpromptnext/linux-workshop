# Lab 01: Linux Basics

## Objective
Get familiar with Linux terminal, basic commands, and the Linux file system structure.  

## Topics Covered
- Terminal basics and navigation  
- File system hierarchy (`/home`, `/etc`, `/var`, `/tmp`)  
- Linux version and kernel information  

## Pre-requisites
- Access to a Linux machine (VM or server)  
- Terminal or SSH access  

**Explore current directory**  
   ```bash
   pwd
   ls -l
````

**Navigate the file system**

   ```bash
   cd /home
   cd ..
   cd /tmp
   ```

**List hidden files and details**

   ```bash
   ls -a
   ls -lh
   ```

**Check Linux version and kernel**

   ```bash
   uname -a
   cat /etc/os-release
   ```

**Check disk usage**

   ```bash
   df -h
   du -sh *
   ```
