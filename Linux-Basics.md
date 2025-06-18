# Linux Basics for DevOps

This guide explains the core concepts of Linux from a DevOps perspective. It includes users and permission management, file system navigation, package installation, system monitoring, and essential tools for daily operations. It is structured for clarity and applies directly to server maintenance, CI/CD pipelines, cloud environments, and containerized systems.

## 🔐 Linux Users and Permissions

### User Types:

* **Root User** (`UID = 0`): Superuser with unrestricted access.
* **Normal Users**: Limited access, usually for human operators.
* **System Users**: Non-human accounts for services like `nginx`, `mysql`.

### Understanding Permissions:

Each file or directory has three permission sets:

* **User (owner)**
* **Group (group members)**
* **Others (everyone else)**

Each set uses three permission types:

* `r` – read
* `w` – write
* `x` – execute

Example from `ls -l` output:

```
-rwxr-xr-- 1 user group 1024 Jun 17 08:00 script.sh
```

Means:

* User: `rwx` → read/write/execute
* Group: `r-x` → read/execute
* Others: `r--` → read-only

### Permission Commands:

```bash
ls -l                      # View permissions
chmod 755 file.sh         # rwxr-xr-x
chmod +x script.sh        # Add execute
chown wahba:admin file.sh # Change owner and group
```

## 📁 Filesystem and Directories

### Navigation Commands:

```bash
cd /var/log      # Go to folder
ls -lah          # Detailed list + hidden files
pwd              # Show current path
```

### Important Linux Directories:

| Directory  | Purpose                           |
| ---------- | --------------------------------- |
| `/`        | Root directory                    |
| `/etc`     | System configuration files        |
| `/home`    | User home directories             |
| `/var`     | Logs, caches, databases           |
| `/usr/bin` | User commands and apps            |
| `/bin`     | Core binaries (e.g., `ls`, `cat`) |
| `/tmp`     | Temporary files (auto-cleaned)    |
| `/dev`     | Device files (disks, input)       |
| `/proc`    | Virtual filesystem (kernel info)  |
| `/root`    | Root user’s home directory        |
| `/boot`    | Bootloader, kernel files          |

## 📦 Package Management

### Debian/Ubuntu:

```bash
sudo apt update          # Refresh package index
sudo apt install nginx   # Install nginx
sudo apt remove nginx    # Remove nginx
```

### RHEL/CentOS:

```bash
sudo yum update            # Refresh packages (older systems)
sudo yum install httpd     # Install Apache
sudo dnf install nginx     # Use dnf on newer RHEL/CentOS
```

## 🧠 System & Process Monitoring

### View Processes:

```bash
ps aux          # All processes
htop            # Interactive process monitor
top             # Dynamic process view
```

### Kill Processes:

```bash
kill 1234       # Gracefully stop PID 1234
kill -9 1234    # Force kill PID 1234
```

### System Info:

```bash
uname -a        # Kernel info
hostname        # System hostname
df -h           # Disk usage (human-readable)
free -m         # Memory in MB
uptime          # Load and uptime
whoami          # Current user
```

## 📡 Networking & Connectivity

### Interface and IP:

```bash
ip a                  # Show all IPs
ip route              # Routing table
```

### Testing Tools:

```bash
ping 8.8.8.8          # Connectivity test
curl https://google.com  # HTTP GET
wget https://file.com   # Download file
```

### Ports & Listeners:

```bash
ss -tuln             # Show TCP/UDP listeners
netstat -tuln        # Legacy alternative
```

### Tracing:

```bash
traceroute 8.8.8.8   # Network path to host
```

## 📂 Text Processing & File Search

### File Discovery:

```bash
find /etc -name "*.conf"         # Find all config files
```

### Grep / Awk / Sed:

```bash
grep "ERROR" logfile.txt         # Find error lines
awk '{print $1}' file.txt         # Print first column
sed 's/old/new/g' file.txt        # Replace text
```

### Utilities:

```bash
cut -d":" -f1 /etc/passwd         # Extract usernames
tee output.log                    # Print + write to file
```

## 👤 User & Group Management

### Create Users:

```bash
adduser wahba
passwd wahba
usermod -aG sudo wahba     # Give sudo access
```

### View Info:

```bash
id              # UID/GID and groups
who             # Who is logged in
last            # Last logins
```

## 🔒 File Permission Modes

### Symbolic to Numeric:

| Symbolic  | Numeric | Meaning                |
| --------- | ------- | ---------------------- |
| rwx------ | 700     | Only owner full access |
| rwxr-xr-- | 754     | Owner full, group RX   |
| rw-r--r-- | 644     | Owner RW, rest read    |

```bash
chmod 644 file.txt
chmod u+x deploy.sh
```

## Tips

* `man <command>` → Manual pages
* Use `TAB` to auto-complete commands/paths
* Use `!!` to repeat last command
* `history | grep ssh` → Search shell history
* `alias ll='ls -lah'` → Add to `~/.bashrc` for convenience

> 📘 **Author**: Wahba Mousa — Senior DevOps Engineer (2025)

📁 [Back to Linux Essentials Overview](./README.md)