# Lab 4: Finding Files and Working with Data

## Introduction

In Lab 3 you learned how to process text and logs using commands such as:

```text
grep
cut
sort
uniq
wc
```

In this lab, we will focus on locating files and working with collections of files.

This is useful in cybersecurity when you need to:

* locate suspicious files;
* identify scripts or executables;
* find configuration files;
* search large directory structures;
* identify files by type;
* compare files;
* process many files automatically.

---

## Objectives

By the end of this lab, you should be able to:

1. Use wildcards to match filenames.
2. Search for files using `find`.
3. Search based on name and file type.
4. Identify file contents using `file`.
5. Work with filenames and paths.
6. Compare files using `diff`.
7. Send lists of files into other commands.
8. Use `xargs`.
9. Combine `find`, `grep`, and other commands.
10. Perform simple file triage tasks.

---

# Part 1: Set Up Lab 4

Open your existing Codespace.

Return to the repository root.

Create:

```bash
mkdir lab04
cd lab04
```

Confirm your location:

```bash
pwd
```

---

# Part 2: Create a Sample Directory Structure

Create the following directories:

```bash
mkdir logs scripts configs evidence backups
```

Create files:

```bash
touch logs/auth.log
touch logs/access.log
touch logs/firewall.log

touch scripts/check.sh
touch scripts/scan.py
touch scripts/report.py

touch configs/app.conf
touch configs/server.conf
touch configs/backup.conf

touch evidence/image.jpg
touch evidence/document.txt
touch evidence/malware.bin

touch backups/config.old
touch backups/users.old
```

Check:

```bash
ls
```

---

# Part 3: Wildcards

Linux shells allow us to match filenames using wildcards.

The most common wildcard is:

```text
*
```

It means:

> zero or more characters

Try:

```bash
ls scripts/*.py
```

This should display:

```text
scripts/report.py
scripts/scan.py
```

Try:

```bash
ls configs/*.conf
```

---

# Part 4: The `?` Wildcard

The `?` symbol matches exactly one character.

Create:

```bash
touch file1.txt file2.txt file3.txt file10.txt
```

Try:

```bash
ls file?.txt
```

Which files match?

Now try:

```bash
ls file*.txt
```

Notice the difference.

---

# Exercise 1: Wildcards

Use wildcards to display:

1. all `.py` files;
2. all `.log` files;
3. all `.conf` files;
4. all filenames beginning with `file`;
5. only `file1.txt`, `file2.txt`, and `file3.txt`.

---

# Part 5: Introduction to `find`

The `find` command searches directory structures.

Basic syntax:

```text
find location criteria
```

Try:

```bash
find .
```

The `.` means:

```text
start searching from the current directory
```

This displays all files and directories below your current location.

---

# Part 6: Find Files by Name

Search for:

```bash
find . -name "scan.py"
```

Search for all Python files:

```bash
find . -name "*.py"
```

Search for all log files:

```bash
find . -name "*.log"
```

---

# Exercise 2

Use `find` to locate:

1. `auth.log`;
2. every `.py` file;
3. every `.conf` file;
4. every `.txt` file;
5. every filename ending in `.old`.

---

# Part 7: Case-Insensitive Searching

Try:

```bash
find . -iname "*.PY"
```

The option:

```text
-iname
```

performs a case-insensitive name search.

---

# Part 8: File Types

`find` can distinguish between files and directories.

Find regular files:

```bash
find . -type f
```

Find directories:

```bash
find . -type d
```

Find only Python files:

```bash
find . -type f -name "*.py"
```

---

# Exercise 3

Use `find` to:

1. list all directories;
2. list all regular files;
3. find regular `.log` files;
4. find directories whose names contain `config`.

---

# Part 9: Searching Within a Specific Directory

Instead of searching from:

```text
.
```

you can choose a specific directory.

For example:

```bash
find scripts -type f
```

Try:

```bash
find evidence -type f
```

---

# Part 10: Using `file`

The `file` command attempts to identify a file based on its contents.

Try:

```bash
file scripts/scan.py
```

Now:

```bash
file configs/server.conf
```

Try:

```bash
file evidence/malware.bin
```

Because these files are currently empty, many may simply be reported as empty.

Let's add some content.

---

# Part 11: Add Sample Content

Add Python code:

```bash
echo 'print("Scanning...")' > scripts/scan.py
```

Add shell code:

```bash
echo '#!/bin/bash' > scripts/check.sh
echo 'echo "Checking system"' >> scripts/check.sh
```

Add configuration data:

```bash
echo 'port=8080' > configs/server.conf
```

Run:

```bash
file scripts/scan.py
file scripts/check.sh
file configs/server.conf
```

---

# Exercise 4

Use `file` on at least five files in your lab.

Record the file types reported.

---

# Part 12: `basename`

The `basename` command removes directory information from a path.

Try:

```bash
basename /workspaces/scripting-for-cybersecurity/lab04/scripts/scan.py
```

Output:

```text
scan.py
```

Try:

```bash
basename configs/server.conf
```

---

# Part 13: `dirname`

The `dirname` command does the opposite.

Try:

```bash
dirname /workspaces/scripting-for-cybersecurity/lab04/scripts/scan.py
```

This displays the directory part of the path.

---

# Exercise 5

Use `basename` and `dirname` on:

```text
/workspaces/scripting-for-cybersecurity/lab04/logs/auth.log
```

Determine:

1. the filename;
2. the directory path.

---

# Part 14: Comparing Files with `diff`

Create:

```text
config1.txt
```

containing:

```text
server=web01
port=443
logging=enabled
timeout=30
```

Create:

```text
config2.txt
```

containing:

```text
server=web01
port=8443
logging=enabled
timeout=60
```

Compare them:

```bash
diff config1.txt config2.txt
```

The output shows the lines that differ.

---

# Exercise 6

Create two small text files with mostly identical content but at least two differences.

Use `diff` to identify the differences.

---

# Part 15: Redirecting `find` Results

Find all Python files:

```bash
find . -type f -name "*.py"
```

Save the results:

```bash
find . -type f -name "*.py" > python-files.txt
```

Display:

```bash
cat python-files.txt
```

---

# Part 16: Counting Files

Count all regular files:

```bash
find . -type f | wc -l
```

Count Python files:

```bash
find . -type f -name "*.py" | wc -l
```

---

# Exercise 7

Determine:

1. total regular files;
2. total directories;
3. total `.py` files;
4. total `.log` files;
5. total `.conf` files.

---

# Part 17: Combining `find` and `grep`

Add some content to the log files:

```bash
echo "Accepted password for alice" > logs/auth.log
echo "Failed password for admin" >> logs/auth.log

echo "GET /index.html 200" > logs/access.log
echo "GET /admin 403" >> logs/access.log

echo "ALLOW 192.168.1.10" > logs/firewall.log
echo "BLOCK 203.0.113.10" >> logs/firewall.log
```

Search all log files for:

```text
admin
```

Using:

```bash
grep "admin" logs/*.log
```

Now try:

```bash
grep -r "admin" logs
```

The `-r` option searches recursively.

---

# Exercise 8

Search recursively for:

1. `admin`;
2. `BLOCK`;
3. `8080`;
4. `Scanning`.

Search from the Lab 4 directory.

---

# Part 18: Introducing `xargs`

Sometimes one command produces a list of filenames that we want another command to process.

Try:

```bash
find scripts -type f
```

Now:

```bash
find scripts -type f | xargs file
```

The first command finds files.

`xargs` passes those filenames to:

```text
file
```

---

# Part 19: Another `xargs` Example

Find all `.conf` files:

```bash
find configs -type f -name "*.conf"
```

Now display their contents:

```bash
find configs -type f -name "*.conf" | xargs cat
```

---

# Exercise 9

Use `find` and `xargs` to:

1. run `file` against all `.py` files;
2. display the contents of all `.log` files;
3. run `wc -l` against all `.conf` files.

---

# Part 20: Safer `xargs`

Filenames may contain spaces.

A safer pattern is:

```bash
find . -type f -print0 | xargs -0 file
```

You do not need to memorise this yet.

The important point is:

> filenames are not always simple strings with no spaces.

This becomes important when scripting.

---

# Part 21: Find by Size

The `find` command can also search based on file size.

Try:

```bash
find . -type f -size 0
```

This should find empty files.

Try:

```bash
find . -type f -size +0c
```

This finds files larger than 0 bytes.

---

# Exercise 10

Determine:

1. which files are empty;
2. which files contain data;
3. how many empty files exist.

---

# Part 22: Find by Modification Time

`find` can search using modification times.

For example:

```bash
find . -type f -mmin -10
```

This finds files modified within approximately the last 10 minutes.

Try:

```bash
find . -type f -mmin -60
```

This is useful when investigating:

> What changed recently?

---

# Part 23: Cybersecurity File Triage Scenario

Imagine you are examining a directory during an investigation.

You want to answer:

* How many files exist?
* Which files are scripts?
* Which files are configuration files?
* Which files are empty?
* Which files were modified recently?
* Which files contain the word `admin`?
* Which files contain the word `BLOCK`?

Use commands from this lab to answer these questions.

---

# Part 24: Create a Triage Report

Create:

```text
triage-report.txt
```

Include:

```text
File Triage Report

Total Files:
Total Directories:
Python Files:
Log Files:
Configuration Files:
Empty Files:

Python Files Found:
```

Generate the values using commands.

Append the list of Python files underneath.

---

# Part 25: Combined Challenge

Create:

```text
suspicious/
```

Inside it create:

```text
notes.txt
scan.py
passwords.txt
config.conf
script.sh
empty.bin
```

Add content to some of them.

For example:

```text
notes.txt
admin password changed

passwords.txt
alice:password123

config.conf
debug=true

scan.py
print("scan")

script.sh
#!/bin/bash
echo "test"
```

Leave:

```text
empty.bin
```

empty.

Now use Linux commands to determine:

1. all files in the directory;
2. which files are empty;
3. which files contain `password`;
4. which files contain `admin`;
5. which files are `.py`;
6. which files are `.sh`;
7. what `file` reports for each file;
8. how many total files exist.

---

# Part 26: Useful Commands from This Lab

You should now have used:

```bash
find
file
basename
dirname
diff
xargs
grep
wc
cat
```

You have also used:

```text
*
?
-name
-iname
-type
-size
-mmin
```

---

# Part 27: Commit Your Work

Return to the repository root.

Confirm that you now have:

```text
scripting-for-cybersecurity/
├── lab01/
├── lab02/
├── lab03/
└── lab04/
```

Stage, commit, and push your work.

Suggested commit message:

```text
Complete Lab 4
```

---

# Optional Extension

Investigate the following:

```bash
find . -maxdepth
find . -mindepth
find . -exec
diff -u
grep -r
grep -l
```

For each command or option:

1. determine what it does;
2. run an example;
3. consider how it could be useful during a cybersecurity investigation.

---

# Preparing for the Next Lab

The next stage will be to move from individual command lines into **Bash scripts**.

Instead of manually entering:

```bash
find . -type f | wc -l
```

every time, we can place commands inside a script and reuse them.

This is where command-line knowledge begins to turn into automation.

---

# End of Lab 4
