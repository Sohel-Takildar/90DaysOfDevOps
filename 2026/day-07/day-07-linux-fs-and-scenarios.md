# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

## Part 1: Linux File System Hierarchy

---

## 1. `/` (Root Directory)

### Purpose

The root directory is the starting point of the Linux file system.
All files and directories exist under `/`.

### Command

```bash
ls -l /
```

### Example Output

```bash
bin  boot  dev  etc  home  opt  root  tmp  usr  var
```

### Notes

* `etc` contains configuration files
* `home` stores user directories

### I would use this when...

I need to understand the top-level structure of a Linux system.

---

## 2. `/home`

### Purpose

Contains home directories for normal users.

### Command

```bash
ls -l /home
```

### Example Output

```bash
rizwan/
ubuntu/
```

### Notes

* Each user usually gets a personal directory here
* User files, downloads, and scripts are stored here

### I would use this when...

I need to access user files or troubleshoot user-specific issues.

---

## 3. `/root`

### Purpose

Home directory of the root (administrator) user.

### Command

```bash
ls -l /root
```

### Example Output

```bash
backup.sh
notes.txt
```

### Notes

* Only root has access by default
* Stores admin-level files and scripts

### I would use this when...

Working as a system administrator or troubleshooting with root access.

---

## 4. `/etc`

### Purpose

Contains system-wide configuration files.

### Command

```bash
ls -l /etc
```

### Example Output

```bash
hostname
hosts
passwd
ssh/
```

### Notes

* `hostname` stores system hostname
* `ssh/` contains SSH configuration

### I would use this when...

Editing service configurations or checking system settings.

---

## 5. `/var/log`

### Purpose

Stores system and application log files.

### Command

```bash
ls -l /var/log
```

### Example Output

```bash
syslog
auth.log
kern.log
```

### Notes

* Logs are critical for troubleshooting
* Helps diagnose service failures and system issues

### I would use this when...

Investigating errors, crashes, or service failures.

---

## 6. `/tmp`

### Purpose

Stores temporary files created by applications and users.

### Command

```bash
ls -l /tmp
```

### Example Output

```bash
tmpfile123
systemd-private/
```

### Notes

* Files may be deleted automatically after reboot
* Used for temporary storage

### I would use this when...

Testing scripts or storing temporary data.

---

## 7. `/bin`

### Purpose

Contains essential command binaries needed for booting and basic system usage.

### Command

```bash
ls -l /bin
```

### Example Output

```bash
bash
cp
mv
ls
```

### Notes

* Includes important commands like `ls`, `cp`, and `mv`

### I would use this when...

Running basic Linux commands required for system operations.

---

## 8. `/usr/bin`

### Purpose

Contains user command binaries and installed applications.

### Command

```bash
ls -l /usr/bin
```

### Example Output

```bash
python3
git
vim
docker
```

### Notes

* Most installed applications are stored here

### I would use this when...

Finding installed software binaries or command paths.

---

## 9. `/opt`

### Purpose

Used for optional or third-party applications.

### Command

```bash
ls -l /opt
```

### Example Output

```bash
google/
custom-app/
```

### Notes

* Common location for manually installed software

### I would use this when...

Installing or managing third-party applications.

---

# Hands-on Practice

## Find Largest Log Files

```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

### What I Learned

This command helps identify large log files consuming disk space.

---

## Check Hostname Configuration

```bash
cat /etc/hostname
```

### What I Learned

The hostname file stores the system name.

---

## Check Home Directory Files

```bash
ls -la ~
```

### What I Learned

Shows hidden files, permissions, and user configurations.

---

# Part 2: Scenario-Based Practice

---

# Scenario 1: Service Not Starting

## Problem

A web application service called `myapp` failed to start after reboot.

---

### Step 1

```bash
systemctl status myapp
```

### Why

Checks whether the service is active, failed, or stopped.

---

### Step 2

```bash
journalctl -u myapp -n 50
```

### Why

Displays the latest logs related to the service.

---

### Step 3

```bash
systemctl is-enabled myapp
```

### Why

Checks if the service starts automatically on boot.

---

### Step 4

```bash
journalctl -xe
```

### Why

Shows detailed system errors and service-related issues.

---

## What I Learned

Always start with service status, then inspect logs for the root cause.

---

# Scenario 2: High CPU Usage

## Problem

The application server is running very slowly.

---

### Step 1

```bash
top
```

### Why

Shows live CPU and memory usage.

---

### Step 2

```bash
ps aux --sort=-%cpu | head -10
```

### Why

Lists top CPU-consuming processes.

---

### Step 3

```bash
htop
```

### Why

Provides an interactive process viewer.

---

### Step 4

```bash
ps -p <PID> -f
```

### Why

Gets detailed information about a suspicious process.

---

## What I Learned

Identify the process consuming the most CPU before taking action.

---

# Scenario 3: Finding Service Logs

## Problem

A developer asks where Docker logs are stored.

---

### Step 1

```bash
systemctl status docker
```

### Why

Checks Docker service health.

---

### Step 2

```bash
journalctl -u docker -n 50
```

### Why

Displays the last 50 Docker logs.

---

### Step 3

```bash
journalctl -u docker -f
```

### Why

Follows Docker logs in real-time.

---

### Step 4

```bash
journalctl -u docker --since "1 hour ago"
```

### Why

Shows logs generated in the last hour.

---

## What I Learned

systemd services store logs in journald and can be viewed using `journalctl`.

---

# Scenario 4: File Permission Issue

## Problem

The script `backup.sh` is not executing and shows “Permission denied”.

---

### Step 1: Check Current Permissions

```bash
ls -l /home/user/backup.sh
```

### Why

Checks whether execute permission exists.

---

### Step 2: Add Execute Permission

```bash
chmod +x /home/user/backup.sh
```

### Why

Adds execute permission to the script.

---

### Step 3: Verify Permissions

```bash
ls -l /home/user/backup.sh
```

### Why

Confirms that execute permission was added.

---

### Step 4: Run the Script

```bash
./backup.sh
```

### Why

Tests whether the issue is resolved.

---

## What I Learned

Scripts require execute (`x`) permission before they can run.

---

# Key Takeaways

* Linux stores logs mainly inside `/var/log`
* Configuration files are commonly found in `/etc`
* Troubleshooting should follow a step-by-step process
* Logs are the first place to check during failures
* Understanding permissions is essential for Linux administration

---
