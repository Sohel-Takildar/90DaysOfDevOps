# Day 09 Challenge – Linux User & Group Management

## Users & Groups Created

### Users

* tokyo
* berlin
* professor
* nairobi

### Groups

* developers
* admins
* project-team

---

# Task 1 – Create Users

## Commands Used

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

## Verification

### Check users in /etc/passwd

```bash
cat /etc/passwd | grep -E 'tokyo|berlin|professor'
```

### Check home directories

```bash
ls /home
```

---

# Task 2 – Create Groups

## Commands Used

```bash
sudo groupadd developers
sudo groupadd admins
```

## Verification

```bash
cat /etc/group | grep -E 'developers|admins'
```

---

# Task 3 – Assign Users to Groups

## Commands Used

### Add tokyo to developers

```bash
sudo usermod -aG developers tokyo
```

### Add berlin to developers and admins

```bash
sudo usermod -aG developers,admins berlin
```

### Add professor to admins

```bash
sudo usermod -aG admins professor
```

## Verification

```bash
groups tokyo
groups berlin
groups professor
```

### Example Output

```bash
tokyo : tokyo developers

berlin : berlin developers admins

professor : professor admins
```

---

# Task 4 – Shared Directory Setup

## Create Shared Directory

```bash
sudo mkdir -p /opt/dev-project
```

## Change Group Ownership

```bash
sudo chgrp developers /opt/dev-project
```

## Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

## Verify Permissions

```bash
ls -ld /opt/dev-project
```

### Example Output

```bash
drwxrwxr-x 2 root developers 4096 Jun 4 10:30 /opt/dev-project
```

## Test File Creation

### Create file as tokyo

```bash
sudo -u tokyo touch /opt/dev-project/tokyo-file.txt
```

### Create file as berlin

```bash
sudo -u berlin touch /opt/dev-project/berlin-file.txt
```

## Verify Files

```bash
ls -l /opt/dev-project
```

---

# Task 5 – Team Workspace

## Create User

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

## Create Group

```bash
sudo groupadd project-team
```

## Add Users to Group

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

## Create Workspace Directory

```bash
sudo mkdir -p /opt/team-workspace
```

## Change Group Ownership

```bash
sudo chgrp project-team /opt/team-workspace
```

## Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
```

## Verify Directory

```bash
ls -ld /opt/team-workspace
```

## Test File Creation as nairobi

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi-test.txt
```

## Verify Files

```bash
ls -l /opt/team-workspace
```

---

# Group Assignments

| User      | Groups                   |
| --------- | ------------------------ |
| tokyo     | developers, project-team |
| berlin    | developers, admins       |
| professor | admins                   |
| nairobi   | project-team             |

---

# Directories Created

| Directory           | Group Owner  | Permissions |
| ------------------- | ------------ | ----------- |
| /opt/dev-project    | developers   | 775         |
| /opt/team-workspace | project-team | 775         |

---

# Commands Used

```bash
useradd
passwd
groupadd
usermod
groups
mkdir
chgrp
chmod
ls
touch
cat
grep
```

---

# What I Learned

1. How to create Linux users with home directories.
2. How to manage groups and assign multiple users to them.
3. How Linux permissions and group ownership help teams collaborate securely.

---

# Screenshots to Capture

Take screenshots of:

1. User creation commands
2. `/etc/passwd` verification
3. `/etc/group` verification
4. `groups username` output
5. `ls -ld /opt/dev-project`
6. File creation inside shared directories
7. `ls -ld /opt/team-workspace`

---

# Real-World DevOps Use

Linux user and group management is important in DevOps because teams often share servers and deployment environments. Proper permissions help maintain security, collaboration, and controlled access to applications and infrastructure.
