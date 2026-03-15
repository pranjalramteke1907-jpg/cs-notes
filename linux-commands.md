# Linux Commands Cheatsheet

Notes from TryHackMe Linux Fundamentals + Kali Linux practice.

---

## Navigation

| Command | What it does | Example |
|---------|-------------|---------|
| `pwd` | Print current directory (where am I?) | `pwd` |
| `ls` | List files in current folder | `ls -la` |
| `cd` | Change directory | `cd /home/user` |
| `cd ..` | Go up one folder | `cd ..` |

---

## Files and Folders

| Command | What it does | Example |
|---------|-------------|---------|
| `cat` | Read/display a file | `cat notes.txt` |
| `mkdir` | Make a new folder | `mkdir myfolder` |
| `rm` | Delete a file | `rm file.txt` |
| `rm -r` | Delete a folder | `rm -r myfolder` |
| `cp` | Copy a file | `cp file.txt backup.txt` |
| `mv` | Move or rename a file | `mv old.txt new.txt` |
| `touch` | Create an empty file | `touch newfile.txt` |

---

## Searching

| Command | What it does | Example |
|---------|-------------|---------|
| `grep` | Search for text inside files | `grep "password" file.txt` |
| `find` | Find files by name | `find / -name "*.txt"` |
| `locate` | Quickly find a file | `locate config.txt` |

---

## Permissions

| Command | What it does | Example |
|---------|-------------|---------|
| `chmod` | Change file permissions | `chmod 755 script.sh` |
| `chown` | Change file owner | `chown user file.txt` |
| `ls -la` | View permissions of all files | `ls -la` |

---

## Networking

| Command | What it does | Example |
|---------|-------------|---------|
| `ping` | Test if a host is reachable | `ping google.com` |
| `ifconfig` | View network interfaces | `ifconfig` |
| `ip a` | View IP addresses | `ip a` |
| `netstat` | View active connections | `netstat -an` |
| `curl` | Make HTTP requests | `curl http://example.com` |

---

## System Info

| Command | What it does | Example |
|---------|-------------|---------|
| `whoami` | Show current username | `whoami` |
| `uname -a` | Show OS and kernel info | `uname -a` |
| `ps aux` | List running processes | `ps aux` |
| `top` | Live process monitor | `top` |
| `history` | Show command history | `history` |

---

## Package Management (Kali / Debian)

| Command | What it does | Example |
|---------|-------------|---------|
| `sudo apt update` | Update package list | `sudo apt update` |
| `sudo apt install` | Install a tool | `sudo apt install nmap` |

---

## Notes

- `sudo` = run as administrator (super user do)
- Most commands have a `-h` or `--help` flag for instructions
- Tab key autocompletes file and folder names
