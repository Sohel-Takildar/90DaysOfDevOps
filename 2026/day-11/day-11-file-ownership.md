# Day 11 – File Ownership Challenge

## Files & Directories Created

### Files

* devops-file.txt
* team-notes.txt
* project-config.yaml
* heist-project/vault/gold.txt
* heist-project/plans/strategy.conf
* bank-heist/access-codes.txt
* bank-heist/blueprints.pdf
* bank-heist/escape-plan.txt

### Directories

* app-logs/
* heist-project/
* heist-project/vault/
* heist-project/plans/
* bank-heist/

---

# Task 1 – Understanding Ownership

## Command Used

```bash
ls -l
```

## Example Output

```bash
-rw-r--r-- 1 rizwan rizwan 0 Jun 6 12:00 devops-file.txt
```

## Ownership Format

```bash
-rw-r--r-- 1 owner group size date filename
```

## Difference Between Owner and Group

* **Owner** → The user who controls the file.
* **Group** → Multiple users can share access through the same group.

The owner has individual control over the file, while the group allows team-based permissions.

---

# Task 2 – Basic chown Operations

## Create File

```bash
touch devops-file.txt
```

## Check Current Owner

```bash
ls -l devops-file.txt
```

## Create Users (if not already created)

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
```

## Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

## Verify

```bash
ls -l devops-file.txt
```

## Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

## Verify Again

```bash
ls -l devops-file.txt
```

## Ownership Changes

```text
rizwan:rizwan → tokyo:rizwan
tokyo:rizwan → berlin:rizwan
```

---

# Task 3 – Basic chgrp Operations

## Create File

```bash
touch team-notes.txt
```

## Check Current Group

```bash
ls -l team-notes.txt
```

## Create Group

```bash
sudo groupadd heist-team
```

## Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

## Verify

```bash
ls -l team-notes.txt
```

## Group Change

```text
rizwan → heist-team
```

---

# Task 4 – Combined Owner & Group Change

## Create File

```bash
touch project-config.yaml
```

## Create User professor (if needed)

```bash
sudo useradd -m professor
```

## Change Owner and Group Together

```bash
sudo chown professor:heist-team project-config.yaml
```

## Verify

```bash
ls -l project-config.yaml
```

## Create Directory

```bash
mkdir app-logs
```

## Change Directory Ownership

```bash
sudo chown berlin:heist-team app-logs
```

## Verify

```bash
ls -ld app-logs
```

---

# Task 5 – Recursive Ownership

## Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

## Create Group

```bash
sudo groupadd planners
```

## Apply Recursive Ownership

```bash
sudo chown -R professor:planners heist-project/
```

## Verify Recursively

```bash
ls -lR heist-project/
```

## Result

All files and subdirectories inside `heist-project/` changed ownership recursively.

---

# Task 6 – Practice Challenge

## Create Users

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m nairobi
```

## Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

## Create Directory

```bash
mkdir bank-heist
```

## Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

## Set Ownership

### access-codes.txt

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

### blueprints.pdf

```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

### escape-plan.txt

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

## Verify

```bash
ls -l bank-heist/
```

## Expected Output

```bash
-rw-r--r-- 1 tokyo   vault-team access-codes.txt
-rw-r--r-- 1 berlin  tech-team  blueprints.pdf
-rw-r--r-- 1 nairobi vault-team escape-plan.txt
```

---

# Commands Used

```bash
ls -l
ls -ld
ls -lR

touch
mkdir
mkdir -p

sudo useradd -m
sudo groupadd

sudo chown
sudo chown -R
sudo chgrp
```

---

# What I Learned

1. File ownership in Linux is divided into **owner** and **group**.
2. `chown` is used to change file owners, while `chgrp` changes groups.
3. Recursive ownership (`-R`) is useful for managing entire application directories.

---

# Screenshots to Capture

* `ls -l` showing owner/group columns
* Before and after `chown`
* Before and after `chgrp`
* Recursive ownership output
* Final `bank-heist/` ownership structure

---

# Why File Ownership Matters in DevOps

Proper ownership is important for:

* Application deployments
* Shared team access
* CI/CD pipelines
* Container permissions
* Log management
* Secure production environments

---

# Conclusion

Today I learned how Linux manages file ownership and groups using `chown` and `chgrp`. I also practiced recursive ownership changes, which are commonly used in real DevOps environments for managing application directories and shared resources.
