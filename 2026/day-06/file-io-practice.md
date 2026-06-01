# Day 06 – Linux Fundamentals: Read and Write Text Files

## Objective

Practice basic file read/write operations using fundamental Linux commands.

---

## Step 1: Create a File

```bash
touch notes.txt
```

### What it does

Creates an empty file named `notes.txt`.

---

## Step 2: Write Text into the File

```bash
echo "Linux file practice - Line 1" > notes.txt
```

### What it does

Writes the first line into the file using `>`.

---

## Step 3: Append More Text

```bash
echo "Learning redirection operators - Line 2" >> notes.txt
echo "Using append mode in Linux - Line 3" >> notes.txt
```

### What it does

Appends new lines using `>>` without overwriting existing content.

---

## Step 4: Use tee Command

```bash
echo "Writing and displaying using tee - Line 4" | tee -a notes.txt
```

### What it does

Displays output on the terminal and appends it to the file at the same time.

---

## Step 5: Add More Practice Lines

```bash
echo "Reading files with cat - Line 5" >> notes.txt
echo "Viewing top lines with head - Line 6" >> notes.txt
echo "Viewing bottom lines with tail - Line 7" >> notes.txt
echo "Linux fundamentals practice complete - Line 8" >> notes.txt
```

---

## Step 6: Read the Full File

```bash
cat notes.txt
```

### What it does

Displays the complete contents of the file.

---

## Step 7: Read First Few Lines

```bash
head -n 2 notes.txt
```

### What it does

Shows the first 2 lines of the file.

---

## Step 8: Read Last Few Lines

```bash
tail -n 2 notes.txt
```

### What it does

Shows the last 2 lines of the file.

---

## Final File Content

```text
Linux file practice - Line 1
Learning redirection operators - Line 2
Using append mode in Linux - Line 3
Writing and displaying using tee - Line 4
Reading files with cat - Line 5
Viewing top lines with head - Line 6
Viewing bottom lines with tail - Line 7
Linux fundamentals practice complete - Line 8
```

---

## Key Learnings

* `>` overwrites file content
* `>>` appends new content
* `cat` reads the full file
* `head` shows top lines
* `tail` shows bottom lines
* `tee` writes and displays output simultaneously

---

## Why This Matters in DevOps

DevOps engineers work with:

* Log files
* Configuration files
* Scripts
* Deployment outputs

Understanding file operations helps in troubleshooting and automation tasks.
