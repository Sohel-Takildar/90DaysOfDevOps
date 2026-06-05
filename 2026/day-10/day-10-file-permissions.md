# Day 10 Challenge – File Permissions & File Operations

## Task 1 – Create Files

### Commands Used

```bash
touch devops.txt

echo "Linux file permissions practice" > notes.txt

vim script.sh
```

### Content Added in `script.sh`

```bash
echo "Hello DevOps"
```

### Verify Files

```bash
ls -l
```

### Output Example

```bash
-rw-rw-r-- 1 user user    0 Jun  5 18:00 devops.txt
-rw-rw-r-- 1 user user   35 Jun  5 18:02 notes.txt
-rw-rw-r-- 1 user user   21 Jun  5 18:05 script.sh
```

---

# Task 2 – Read Files

## Commands Used

### Read `notes.txt`

```bash
cat notes.txt
```

### Open `script.sh` in Read-Only Mode

```bash
vim -R script.sh
```

### First 5 Lines of `/etc/passwd`

```bash
head -n 5 /etc/passwd
```

### Last 5 Lines of `/etc/passwd`

```bash
tail -n 5 /etc/passwd
```

---

# Task 3 – Understand Permissions

## Command Used

```bash
ls -l devops.txt notes.txt script.sh
```

## Permission Explanation

### Example

```bash
-rw-rw-r-- 
```

Breakdown:

* Owner → read & write
* Group → read & write
* Others → read only

### Meaning of Permission Values

| Permission | Value |
| ---------- | ----- |
| r          | 4     |
| w          | 2     |
| x          | 1     |

---

# Task 4 – Modify Permissions

## 1. Make `script.sh` Executable

```bash
chmod +x script.sh
```

### Run Script

```bash
./script.sh
```

### Output

```bash
Hello DevOps
```

---

## 2. Make `devops.txt` Read-Only

```bash
chmod a-w devops.txt
```

### Verify

```bash
ls -l devops.txt
```

### Output Example

```bash
-r--r--r-- 1 user user 0 Jun 5 18:00 devops.txt
```

---

## 3. Set `notes.txt` Permission to 640

```bash
chmod 640 notes.txt
```

### Verify

```bash
ls -l notes.txt
```

### Output Example

```bash
-rw-r----- 1 user user 35 Jun 5 18:02 notes.txt
```

Meaning:

* Owner → read & write
* Group → read only
* Others → no permission

---

## 4. Create `project/` Directory with Permission 755

```bash
mkdir project

chmod 755 project
```

### Verify

```bash
ls -ld project
```

### Output Example

```bash
drwxr-xr-x 2 user user 4096 Jun 5 18:20 project
```

---

# Task 5 – Test Permissions

## 1. Try Writing to Read-Only File

```bash
echo "test" >> devops.txt
```

### Error

```bash
Permission denied
```

---

## 2. Remove Execute Permission and Try Running Script

```bash
chmod -x script.sh

./script.sh
```

### Error

```bash
Permission denied
```

---

# Screenshots Added

* File creation
* Permission before changes
* Permission after changes
* Script execution
* Permission denied errors

---

# Commands Used

```bash
touch
echo
cat
vim
head
tail
ls -l
chmod
mkdir
```

---

# What I Learned

1. Linux permissions are controlled using read, write, and execute values.
2. `chmod` is used to change file and directory permissions.
3. Execute permission is required to run shell scripts.
4. Directories use permissions differently from files.
5. Permission errors help protect files from unauthorized access.
