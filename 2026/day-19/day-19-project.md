# Day 19 – Shell Scripting Project: Log Rotation, Backup & Crontab

## Objective

Apply shell scripting concepts by creating real-world automation scripts for:

* Log Rotation
* Server Backup
* Cron Scheduling
* Combined Maintenance Automation

---

# Task 1: Log Rotation Script

### File: `log_rotate.sh`

```bash
#!/bin/bash

set -euo pipefail

if [ $# -ne 1 ]; then
    echo "Usage: $0 <log_directory>"
    exit 1
fi

LOG_DIR="$1"

if [ ! -d "$LOG_DIR" ]; then
    echo "Error: Directory does not exist."
    exit 1
fi

compressed=0
deleted=0

while IFS= read -r file; do
    gzip "$file"
    ((compressed++))
done < <(find "$LOG_DIR" -type f -name "*.log" -mtime +7)

while IFS= read -r file; do
    rm -f "$file"
    ((deleted++))
done < <(find "$LOG_DIR" -type f -name "*.gz" -mtime +30)

echo "Compressed files: $compressed"
echo "Deleted files: $deleted"
```

### Make Executable

```bash
chmod +x log_rotate.sh
```

### Example Run

```bash
./log_rotate.sh /var/log/myapp
```

### Sample Output

```text
Compressed files: 4
Deleted files: 2
```

---

# Task 2: Server Backup Script

### File: `backup.sh`

```bash
#!/bin/bash

set -euo pipefail

if [ $# -ne 2 ]; then
    echo "Usage: $0 <source_directory> <backup_destination>"
    exit 1
fi

SOURCE_DIR="$1"
BACKUP_DIR="$2"

if [ ! -d "$SOURCE_DIR" ]; then
    echo "Error: Source directory does not exist."
    exit 1
fi

mkdir -p "$BACKUP_DIR"

DATE=$(date +%Y-%m-%d)
ARCHIVE="$BACKUP_DIR/backup-$DATE.tar.gz"

tar -czf "$ARCHIVE" "$SOURCE_DIR"

if [ ! -f "$ARCHIVE" ]; then
    echo "Backup failed."
    exit 1
fi

SIZE=$(du -h "$ARCHIVE" | awk '{print $1}')

echo "Backup created successfully."
echo "Archive: $ARCHIVE"
echo "Size: $SIZE"

find "$BACKUP_DIR" -type f -name "*.tar.gz" -mtime +14 -delete
```

### Make Executable

```bash
chmod +x backup.sh
```

### Example Run

```bash
./backup.sh /etc /backups
```

### Sample Output

```text
Backup created successfully.
Archive: /backups/backup-2026-06-16.tar.gz
Size: 18M
```

---

# Task 3: Crontab

## View Existing Cron Jobs

```bash
crontab -l
```

## Cron Syntax

```text
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

## Cron Entries

### Run log rotation daily at 2:00 AM

```cron
0 2 * * * /home/user/scripts/log_rotate.sh /var/log/myapp
```

### Run backup every Sunday at 3:00 AM

```cron
0 3 * * 0 /home/user/scripts/backup.sh /etc /backups
```

### Run health check every 5 minutes

```cron
*/5 * * * * /home/user/scripts/health_check.sh
```

---

# Task 4: Scheduled Maintenance Script

### File: `maintenance.sh`

```bash
#!/bin/bash

set -euo pipefail

LOG_FILE="/var/log/maintenance.log"

log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') : $1" >> "$LOG_FILE"
}

log_message "Maintenance Started"

/home/user/scripts/log_rotate.sh /var/log/myapp >> "$LOG_FILE" 2>&1
/home/user/scripts/backup.sh /etc /backups >> "$LOG_FILE" 2>&1

log_message "Maintenance Completed"
```

### Make Executable

```bash
chmod +x maintenance.sh
```

### Sample Log Output

```text
2026-06-16 01:00:00 : Maintenance Started
Compressed files: 4
Deleted files: 2
Backup created successfully.
Archive: /backups/backup-2026-06-16.tar.gz
Size: 18M
2026-06-16 01:00:15 : Maintenance Completed
```

---

# Cron Entry for Maintenance Script

Run daily at 1:00 AM:

```cron
0 1 * * * /home/user/scripts/maintenance.sh
```

---

# Project Directory Structure

```text
2026/
└── day-19/
    ├── day-19-project.md
    ├── log_rotate.sh
    ├── backup.sh
    └── maintenance.sh
```

---

# What I Learned

### 1. Automating Log Management

Using `find`, `gzip`, and file age filters helps automate log cleanup and saves disk space.

### 2. Creating Reliable Backups

`tar` combined with timestamps provides organized backups and makes recovery easier.

### 3. Scheduling Tasks with Cron

Cron allows recurring jobs to run automatically without manual intervention, improving system maintenance.

---
