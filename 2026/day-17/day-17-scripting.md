# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Objective

Learn how to use loops, command-line arguments, package installation automation, and basic error handling in shell scripts.

---

# Task 1: For Loop

## Script: for_loop.sh

```bash
#!/bin/bash

for fruit in Apple Banana Mango Orange Grapes
do
    echo "$fruit"
done
```

### Output

```text
Apple
Banana
Mango
Orange
Grapes
```

---

## Script: count.sh

```bash
#!/bin/bash

for num in {1..10}
do
    echo "$num"
done
```

### Output

```text
1
2
3
4
5
6
7
8
9
10
```

---

# Task 2: While Loop

## Script: countdown.sh

```bash
#!/bin/bash

echo "Enter a number:"
read number

while [ $number -ge 0 ]
do
    echo "$number"
    number=$((number-1))
done

echo "Done!"
```

### Output

```text
Enter a number:
5
5
4
3
2
1
0
Done!
```

---

# Task 3: Command-Line Arguments

## Script: greet.sh

```bash
#!/bin/bash

if [ -z "$1" ]
then
    echo "Usage: ./greet.sh <name>"
else
    echo "Hello, $1!"
fi
```

### Output

```bash
./greet.sh Rizwan
```

```text
Hello, Rizwan!
```

---

## Script: args_demo.sh

```bash
#!/bin/bash

echo "Script Name: $0"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

### Output

```bash
./args_demo.sh Linux Docker Kubernetes
```

```text
Script Name: ./args_demo.sh
Total Arguments: 3
All Arguments: Linux Docker Kubernetes
```

---

# Task 4: Install Packages via Script

## Script: install_packages.sh

```bash
#!/bin/bash

# Check if running as root
if [ "$EUID" -ne 0 ]
then
    echo "Please run this script as root."
    exit 1
fi

packages=("nginx" "curl" "wget")

for pkg in "${packages[@]}"
do
    if dpkg -s "$pkg" &>/dev/null
    then
        echo "$pkg is already installed."
    else
        echo "Installing $pkg ..."
        apt update -y
        apt install -y "$pkg"
    fi
done
```

### Output Example

```text
nginx is already installed.
curl is already installed.
Installing wget ...
```

---

# Task 5: Error Handling

## Script: safe_script.sh

```bash
#!/bin/bash

set -e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || {
    echo "Failed to enter directory"
    exit 1
}

touch testfile.txt || {
    echo "Failed to create file"
    exit 1
}

echo "Script completed successfully."
```

### Output

```text
Directory already exists
Script completed successfully.
```

---

# Key Learnings

### 1. Loops

* Used `for` loops to iterate through lists and ranges.
* Used `while` loops for repeated execution based on conditions.

### 2. Command-Line Arguments

* `$1` = First argument
* `$#` = Number of arguments
* `$@` = All arguments
* `$0` = Script name

### 3. Error Handling

* Used `set -e` to stop script execution on errors.
* Used `||` operator to handle failures gracefully.
* Checked for root privileges using `$EUID`.

---

# Repository Structure

```text
2026/
└── day-17/
    ├── for_loop.sh
    ├── count.sh
    ├── countdown.sh
    ├── greet.sh
    ├── args_demo.sh
    ├── install_packages.sh
    ├── safe_script.sh
    └── day-17-scripting.md
```

---

# Conclusion

Day 17 focused on practical shell scripting skills used by DevOps engineers. I learned how to automate repetitive tasks using loops, accept user input through command-line arguments, install packages automatically, and make scripts more reliable using error handling techniques.
