# Shell Scripting Cheat Sheet

A quick reference guide for Bash/Shell scripting used in Linux and DevOps.

---

# Quick Reference Table

| Topic    | Key Syntax               | Example                            |
| -------- | ------------------------ | ---------------------------------- |
| Variable | `VAR="value"`            | `NAME="DevOps"`                    |
| Argument | `$1`, `$2`               | `./script.sh arg1`                 |
| If       | `if [ condition ]; then` | `if [ -f file ]; then`             |
| For Loop | `for i in list; do`      | `for i in 1 2 3; do`               |
| Function | `name() { ... }`         | `greet() { echo "Hi"; }`           |
| Grep     | `grep pattern file`      | `grep -i error app.log`            |
| Awk      | `awk '{print $1}' file`  | `awk -F: '{print $1}' /etc/passwd` |
| Sed      | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt`  |

---

# 1. Basics

## Shebang

Defines the interpreter for the script.

```bash
#!/bin/bash
```

## Running a Script

```bash
chmod +x script.sh
./script.sh

# OR

bash script.sh
```

## Comments

```bash
# Single line comment

echo "Hello" # Inline comment
```

## Variables

```bash
NAME="Rizwan"

echo $NAME
echo "$NAME"
echo '$NAME'
```

**Difference**

* `$NAME` → Variable expands
* `"$NAME"` → Expands safely
* `'$NAME'` → Prints literally

## Read User Input

```bash
read -p "Enter name: " NAME
echo "Hello $NAME"
```

## Command-Line Arguments

```bash
echo $0   # Script name
echo $1   # First argument
echo $2   # Second argument
echo $#   # Number of arguments
echo $@   # All arguments
echo $?   # Previous command status
```

---

# 2. Operators and Conditionals

## String Comparisons

```bash
[ "$A" = "$B" ]
[ "$A" != "$B" ]
[ -z "$A" ]   # Empty
[ -n "$A" ]   # Not empty
```

## Integer Comparisons

```bash
[ $A -eq $B ]
[ $A -ne $B ]
[ $A -lt $B ]
[ $A -gt $B ]
[ $A -le $B ]
[ $A -ge $B ]
```

## File Test Operators

```bash
-f file.txt    # File exists
-d mydir       # Directory exists
-e file        # Exists
-r file        # Readable
-w file        # Writable
-x script.sh   # Executable
-s file        # Not empty
```

## If / Elif / Else

```bash
if [ $AGE -ge 18 ]; then
    echo "Adult"
elif [ $AGE -ge 13 ]; then
    echo "Teen"
else
    echo "Child"
fi
```

## Logical Operators

```bash
[ $A -gt 5 ] && echo "True"

[ $A -lt 5 ] || echo "False"

! grep "error" app.log
```

## Case Statement

```bash
case $1 in
    start)
        echo "Starting"
        ;;
    stop)
        echo "Stopping"
        ;;
    *)
        echo "Invalid option"
        ;;
esac
```

---

# 3. Loops

## For Loop

### List-Based

```bash
for i in 1 2 3 4 5
do
    echo $i
done
```

### C-Style

```bash
for ((i=1; i<=5; i++))
do
    echo $i
done
```

## While Loop

```bash
COUNT=1

while [ $COUNT -le 5 ]
do
    echo $COUNT
    ((COUNT++))
done
```

## Until Loop

```bash
COUNT=1

until [ $COUNT -gt 5 ]
do
    echo $COUNT
    ((COUNT++))
done
```

## Break

```bash
for i in {1..10}
do
    [ $i -eq 5 ] && break
    echo $i
done
```

## Continue

```bash
for i in {1..5}
do
    [ $i -eq 3 ] && continue
    echo $i
done
```

## Loop Through Files

```bash
for file in *.log
do
    echo $file
done
```

## Read Command Output

```bash
cat users.txt | while read line
do
    echo $line
done
```

---

# 4. Functions

## Define Function

```bash
greet() {
    echo "Hello"
}
```

## Call Function

```bash
greet
```

## Function Arguments

```bash
greet() {
    echo "Hello $1"
}

greet Rizwan
```

## Return Values

### return

```bash
check() {
    return 0
}
```

### echo

```bash
sum() {
    echo $(($1+$2))
}

RESULT=$(sum 5 10)
```

## Local Variables

```bash
demo() {
    local NAME="DevOps"
    echo $NAME
}
```

---

# 5. Text Processing Commands

## grep

```bash
grep error app.log
grep -i error app.log
grep -r error .
grep -c error app.log
grep -n error app.log
grep -v error app.log
grep -E "error|warning" app.log
```

## awk

```bash
awk '{print $1}' file.txt

awk -F: '{print $1}' /etc/passwd

awk '/error/' app.log

awk 'BEGIN{print "Start"} {print $1} END{print "End"}' file.txt
```

## sed

```bash
sed 's/foo/bar/' file.txt

sed 's/foo/bar/g' file.txt

sed -i 's/foo/bar/g' config.txt

sed '5d' file.txt
```

## cut

```bash
cut -d',' -f1 file.csv

cut -c1-5 file.txt
```

## sort

```bash
sort file.txt

sort -n numbers.txt

sort -r file.txt

sort -u file.txt
```

## uniq

```bash
uniq file.txt

uniq -c file.txt
```

## tr

```bash
tr 'a-z' 'A-Z'

tr -d '0-9'
```

## wc

```bash
wc file.txt

wc -l file.txt

wc -w file.txt

wc -c file.txt
```

## head / tail

```bash
head file.txt

head -n 20 file.txt

tail file.txt

tail -n 20 file.txt

tail -f app.log
```

---

# 6. Useful One-Liners

## Delete Files Older Than 30 Days

```bash
find /tmp -type f -mtime +30 -delete
```

## Count Lines in All Log Files

```bash
wc -l *.log
```

## Replace Text Across Files

```bash
find . -name "*.conf" -exec sed -i 's/old/new/g' {} \;
```

## Check If Service Is Running

```bash
systemctl is-active nginx
```

## Disk Usage Alert

```bash
df -h | awk '$5+0 > 80 {print $0}'
```

## Parse JSON

```bash
cat file.json | jq .
```

## Parse CSV

```bash
cut -d',' -f1 data.csv
```

## Monitor Errors in Real Time

```bash
tail -f app.log | grep ERROR
```

---

# 7. Error Handling & Debugging

## Exit Codes

```bash
echo $?

exit 0

exit 1
```

## set -e

Exit script on first error.

```bash
set -e
```

## set -u

Treat undefined variables as errors.

```bash
set -u
```

## set -o pipefail

Catch failures inside pipelines.

```bash
set -o pipefail
```

## Strict Mode

Recommended for production scripts.

```bash
set -euo pipefail
```

## Debug Mode

```bash
set -x
```

Example:

```bash
#!/bin/bash
set -x

echo "Debugging"
```

## Trap Cleanup

```bash
cleanup() {
    echo "Cleaning up..."
}

trap cleanup EXIT
```

---

# Common Special Variables

| Variable | Description         |
| -------- | ------------------- |
| `$0`     | Script name         |
| `$1-$9`  | Arguments           |
| `$#`     | Argument count      |
| `$@`     | All arguments       |
| `$?`     | Exit code           |
| `$$`     | Current PID         |
| `$!`     | Last background PID |

---

# DevOps Script Template

```bash
#!/bin/bash

set -euo pipefail

cleanup() {
    echo "Cleaning resources..."
}

trap cleanup EXIT

echo "Script Started"

if [ $# -eq 0 ]; then
    echo "Usage: $0 <file>"
    exit 1
fi

FILE=$1

if [ ! -f "$FILE" ]; then
    echo "File not found"
    exit 1
fi

echo "Processing $FILE"
```

---

# Quick Revision Tips

* Always use `#!/bin/bash`
* Prefer `set -euo pipefail`
* Quote variables: `"$VAR"`
* Validate user inputs
* Check file existence before processing
* Use functions for reusable code
* Use `grep`, `awk`, `sed` daily
* Use `trap` for cleanup
* Test scripts before production deployment
