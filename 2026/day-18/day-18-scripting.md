# Day 18 – Shell Scripting: Functions & Intermediate Concepts

## Objective

Learn how to write reusable shell scripts using functions, local variables, return values, and strict mode (`set -euo pipefail`).

---

# Task 1: Basic Functions

## File: `functions.sh`

```bash
#!/bin/bash

greet() {
    echo "Hello, $1!"
}

add() {
  
}

greet "Rizwan"
add 10 20
```

### Run

```bash
chmod +x functions.sh
./functions.sh
```

### Output

```text
Hello, Rizwan!
Sum: 30
```

---

# Task 2: Functions with Return Values

## File: `disk_check.sh`

```bash
#!/bin/bash

check_disk() {
    echo "===== Disk Usage ====="
    df -h /
}

check_memory() {
    echo "===== Memory Usage ====="
    free -h
}

check_disk
echo
check_memory
```

### Run

```bash
chmod +x disk_check.sh
./disk_check.sh
```

### Sample Output

```text
===== Disk Usage =====
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   18G   30G  38% /

===== Memory Usage =====
               total        used        free
Mem:            7.6Gi       2.1Gi       4.5Gi
```

---

# Task 3: Strict Mode (`set -euo pipefail`)

## File: `strict_demo.sh`

```bash
#!/bin/bash

set -euo pipefail

echo "Testing set -u"
echo "$UNDEFINED_VAR"

echo "This line will not execute"
```

### Result

```text
./strict_demo.sh: line 6: UNDEFINED_VAR: unbound variable
```

---

## Demonstrating `set -e`

```bash
#!/bin/bash

set -euo pipefail

echo "Before failure"

false

echo "After failure"
```

### Result

```text
Before failure
```

Script exits immediately after `false`.

---

## Demonstrating `pipefail`

```bash
#!/bin/bash

set -euo pipefail

grep "hello" missingfile.txt | cat

echo "This line will not run"
```

### Result

```text
grep: missingfile.txt: No such file or directory
```

Script exits because one command in the pipeline failed.

---

## Explanation

### `set -e`

Exit immediately when any command returns a non-zero status.

### `set -u`

Treat undefined variables as errors.

### `set -o pipefail`

Pipeline fails if any command in the pipeline fails.

### Why use strict mode?

* Prevents silent failures
* Makes debugging easier
* Produces safer production scripts

---

# Task 4: Local Variables

## File: `local_demo.sh`

```bash
#!/bin/bash

use_local() {
    local name="Rizwan"
    echo "Inside function: $name"
}

use_global() {
    city="Pune"
    echo "Inside function: $city"
}

use_local
echo "Outside function: ${name:-Not Available}"

echo

use_global
echo "Outside function: $city"
```

### Output

```text
Inside function: Rizwan
Outside function: Not Available

Inside function: Pune
Outside function: Pune
```

### Observation

* `local` variables exist only inside functions.
* Normal variables remain available globally.

---

# Task 5: System Information Reporter

## File: `system_info.sh`

```bash
#!/bin/bash

set -euo pipefail

print_header() {
    echo
    echo "======================================="
    echo "$1"
    echo "======================================="
}

system_info() {
    echo "Hostname: $(hostname)"
    echo "OS: $(uname -a)"
}

uptime_info() {
    uptime
}

disk_usage() {
    du -ah / 2>/dev/null | sort -rh | head -5
}

memory_usage() {
    free -h
}

cpu_processes() {
    ps aux --sort=-%cpu | head -6
}

main() {
    print_header "SYSTEM INFORMATION"
    system_info

    print_header "UPTIME"
    uptime_info

    print_header "TOP 5 DISK USAGE"
    disk_usage

    print_header "MEMORY USAGE"
    memory_usage

    print_header "TOP 5 CPU PROCESSES"
    cpu_processes
}

main
```

### Run

```bash
chmod +x system_info.sh
./system_info.sh
```

### Sample Output

```text
=======================================
SYSTEM INFORMATION
=======================================
Hostname: devops-lab
OS: Linux devops-lab 6.x ...

=======================================
UPTIME
=======================================
18:20:01 up 2 days, 4:15, 2 users

=======================================
TOP 5 DISK USAGE
=======================================
2.5G /var/log
1.8G /home/user
...

=======================================
MEMORY USAGE
=======================================
free -h output

=======================================
TOP 5 CPU PROCESSES
=======================================
PID USER %CPU COMMAND
...
```

---

# What I Learned

### 1. Functions Improve Reusability

Functions help avoid repeating code and make scripts easier to maintain.

### 2. Strict Mode Makes Scripts Safer

Using `set -euo pipefail` prevents hidden errors and unexpected behavior.

### 3. Local Variables Improve Scope Control

The `local` keyword keeps variables limited to functions and prevents accidental overwrites.

---

# Directory Structure

```text
2026/
└── day-18/
    ├── functions.sh
    ├── disk_check.sh
    ├── strict_demo.sh
    ├── local_demo.sh
    ├── system_info.sh
    └── day-18-scripting.md
```

---

# Git Commands

```bash
git add .
git commit -m "Complete Day 18 Shell Scripting challenge"
git push origin main
```
