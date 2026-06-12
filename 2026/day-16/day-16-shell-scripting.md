# Day 16 – Shell Scripting Basics

## Objective

Learn the fundamentals of Bash scripting including:

* Shebang (`#!/bin/bash`)
* Variables
* User Input (`read`)
* If-Else Conditions
* Simple Automation Script

---

# Task 1: Your First Script

## Script: hello.sh

```bash
#!/bin/bash

echo "Hello, DevOps!"
```

### Make Executable

```bash
chmod +x hello.sh
```

### Run Script

```bash
./hello.sh
```

### Output

```text
Hello, DevOps!
```

### What Happens If Shebang Is Removed?

If the shebang (`#!/bin/bash`) is removed and the script is executed using:

```bash
./hello.sh
```

the system may not know which interpreter should run the script.

However, running:

```bash
bash hello.sh
```

will still work because Bash is explicitly specified.

---

# Task 2: Variables

## Script: variables.sh

```bash
#!/bin/bash

NAME="Rizwan"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

### Output

```text
Hello, I am Rizwan and I am a DevOps Engineer
```

### Single Quotes vs Double Quotes

#### Double Quotes

```bash
echo "My name is $NAME"
```

Output:

```text
My name is Rizwan
```

#### Single Quotes

```bash
echo 'My name is $NAME'
```

Output:

```text
My name is $NAME
```

### Difference

* Double quotes expand variables.
* Single quotes treat everything literally.

---

# Task 3: User Input with read

## Script: greet.sh

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
```

### Sample Output

```text
Enter your name: Rizwan
Enter your favourite tool: Docker

Hello Rizwan, your favourite tool is Docker
```

---

# Task 4: If-Else Conditions

## Script: check_number.sh

```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ "$NUM" -gt 0 ]; then
    echo "Positive Number"
elif [ "$NUM" -lt 0 ]; then
    echo "Negative Number"
else
    echo "Zero"
fi
```

### Sample Output

```text
Enter a number: 10
Positive Number
```

---

## Script: file_check.sh

```bash
#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists."
else
    echo "File does not exist."
fi
```

### Sample Output

```text
Enter filename: hello.sh
File exists.
```

---

# Task 5: Combine It All

## Script: server_check.sh

```bash
#!/bin/bash

SERVICE="nginx"

read -p "Do you want to check the status of $SERVICE? (y/n): " CHOICE

if [ "$CHOICE" = "y" ]; then

    if systemctl is-active --quiet "$SERVICE"; then
        echo "$SERVICE is active."
    else
        echo "$SERVICE is not active."
    fi

elif [ "$CHOICE" = "n" ]; then
    echo "Skipped."
else
    echo "Invalid option."
fi
```

### Sample Output

```text
Do you want to check the status of nginx? (y/n): y

nginx is active.
```

OR

```text
nginx is not active.
```

---

# What I Learned

### 1. Shebang Matters

The shebang (`#!/bin/bash`) tells Linux which interpreter should execute the script.

### 2. Variables Make Scripts Dynamic

Variables store reusable values and can be accessed using `$VARIABLE_NAME`.

### 3. Conditions Enable Automation

Using `if`, `elif`, and `else` allows scripts to make decisions based on user input or system state.

---

# Files Created

```text
2026/day-16/
├── hello.sh
├── variables.sh
├── greet.sh
├── check_number.sh
├── file_check.sh
├── server_check.sh
└── day-16-shell-scripting.md
```

# Day 16 Completed ✅

First step into Bash scripting completed successfully.
