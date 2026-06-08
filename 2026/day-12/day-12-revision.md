# Day 12 – Breather & Revision (Days 01–11)

## Goal

Today was focused on revising Linux and DevOps fundamentals learned during Days 01–11.

---

# Revision Notes

## 1. Mindset & Learning Plan Review

* My goal is still to build strong Linux + DevOps fundamentals.
* I need more practice with:

  * File permissions
  * Service troubleshooting
  * Linux user/group management
* Going forward, I want to improve:

  * Command speed
  * Troubleshooting confidence
  * Real-world Linux administration skills

---

# 2. Processes & Services Revision

## Commands Practiced

```bash
ps aux
```

### Observation

* Displayed all running processes.
* Helpful for checking CPU and memory usage.

---

```bash
systemctl status nginx
```

### Observation

* Verified nginx service status.
* Checked whether service was active or failed.

---

```bash
journalctl -u nginx
```

### Observation

* Viewed logs for nginx service.
* Useful for troubleshooting startup errors.

---

# 3. File Skills Practice

## File Operations Practiced

### Append text to file

```bash
echo "DevOps Practice" >> notes.txt
```

### Change permissions

```bash
chmod 755 script.sh
```

### Copy file

```bash
cp notes.txt backup-notes.txt
```

### Create directory

```bash
mkdir revision-practice
```

### Check file permissions

```bash
ls -l
```

---

# 4. Cheat Sheet Refresh (Top 5 Commands)

| Command            | Purpose                     |
| ------------------ | --------------------------- |
| `ls -l`            | View files with permissions |
| `ps aux`           | Check running processes     |
| `chmod`            | Change file permissions     |
| `systemctl status` | Check service health        |
| `journalctl`       | Read service logs           |

---

# 5. User & Group Sanity Check

## Scenario Practiced

### Create User

```bash
sudo useradd testuser
```

### Verify User

```bash
id testuser
```

### Change File Ownership

```bash
sudo chown testuser:testuser demo.txt
```

### Verify Ownership

```bash
ls -l demo.txt
```

---

# Mini Self-Check

## 1. Which 3 commands save you the most time right now, and why?

### `ls -l`

Quickly checks permissions and ownership.

### `ps aux`

Helps identify running processes and resource usage.

### `systemctl status`

Instantly checks whether a service is healthy or failed.

---

## 2. How do you check if a service is healthy?

### Commands I run first:

```bash
systemctl status nginx
```

```bash
ps aux | grep nginx
```

```bash
journalctl -u nginx
```

---

## 3. How do you safely change ownership and permissions?

### Example

```bash
sudo chown rizwan:developers project.txt
chmod 644 project.txt
```

* First change ownership carefully.
* Then apply only required permissions.
* Always verify using:

```bash
ls -l
```

---

## 4. What will you improve in the next 3 days?

* More Linux troubleshooting practice
* Better understanding of permissions
* Faster command-line navigation
* More confidence with services and logs

---

# Key Takeaways

* Linux permissions and ownership are extremely important.
* Service logs help identify problems quickly.
* Small daily practice improves command memory.
* Troubleshooting becomes easier with repetition.

---
