# Day 22 Notes - Introduction to Git

## 1. What is the difference between git add and git commit?

git add moves changes to the staging area.
git commit saves the staged changes permanently in the repository history.

---

## 2. What does the staging area do? Why doesn't Git commit directly?

The staging area acts as a preparation zone where changes are reviewed before committing. It allows developers to choose exactly which changes should be included in a commit instead of committing everything automatically.

---

## 3. What information does git log show you?

git log displays:

* Commit ID (SHA)
* Author name
* Author email
* Date and time
* Commit message

---

## 4. What is the .git folder and what happens if you delete it?

The .git folder contains all repository data, commit history, branches, and configuration. If it is deleted, Git tracking and commit history are lost and the folder becomes a normal directory.

---

## 5. What is the difference between a working directory, staging area, and repository?

### Working Directory

Where files are edited and modified.

### Staging Area

Temporary area where changes are prepared before committing.

### Repository

Permanent storage containing all commits and project history.

Workflow:

Working Directory
↓
git add
↓
Staging Area
↓
git commit
↓
Repository
