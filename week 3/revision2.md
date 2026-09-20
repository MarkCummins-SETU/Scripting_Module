# Labs 3 and 4 Revision Exercise

## Scripting for Cybersecurity

This revision exercise covers the main commands and concepts introduced in:

* Lab 3 – Text Processing and Log Analysis
* Lab 4 – Finding Files and Working with Data

Complete each task using the Linux terminal in your GitHub Codespace.

Create a directory for your work:

```bash
mkdir revision02
cd revision02
```

---

# Setup

Create a file called:

```text
security.log
```

containing:

```text
Failed login admin 203.0.113.10
Failed login root 203.0.113.10
Accepted login alice 192.168.1.20
Failed login admin 198.51.100.24
Accepted login bob 192.168.1.35
Failed login root 203.0.113.10
Failed login test 198.51.100.24
Accepted login alice 192.168.1.20
Failed login admin 203.0.113.15
Failed login guest 203.0.113.10
```

Create:

```text
accounts.csv
```

containing:

```text
alice,student,active
bob,student,active
charlie,staff,active
david,student,disabled
eve,staff,active
frank,student,disabled
```

Create:

```bash
mkdir logs scripts configs evidence
```

Create:

```bash
touch logs/auth.log
touch logs/access.log
touch scripts/check.py
touch scripts/report.py
touch scripts/run.sh
touch configs/server.conf
touch configs/app.conf
touch evidence/notes.txt
touch evidence/empty.bin
```

---

# Question 1

Display the first 4 lines of:

```text
security.log
```

---

# Question 2

Display the final 3 lines of:

```text
security.log
```

---

# Question 3

Display all failed login attempts.

---

# Question 4

Count how many failed login attempts appear in the log.

---

# Question 5

Display all entries containing:

```text
admin
```

Include line numbers in the output.

---

# Question 6

Display all lines that **do not** contain:

```text
Failed
```

---

# Question 7

Count:

1. the number of lines in `security.log`;
2. the number of words in `security.log`.

---

# Question 8

Extract only the usernames from:

```text
accounts.csv
```

Expected output:

```text
alice
bob
charlie
david
eve
frank
```

---

# Question 9

Display only the usernames of accounts whose status is:

```text
disabled
```

---

# Question 10

Using the IP addresses in `security.log`, determine how many times each IP appears.

Hint:

The IP address is the final field.

You may use:

```bash
awk '{print $NF}'
```

with other commands.

---

# Question 11

Determine which IP address appears most frequently in:

```text
security.log
```

Use a command pipeline.

---

# Question 12

Use wildcards to display:

1. all Python files inside `scripts`;
2. all configuration files inside `configs`;
3. all files beginning with `a` inside `logs`.

---

# Question 13

Use `find` to locate every:

```text
.py
```

file below your current directory.

---

# Question 14

Use `find` to display:

1. every regular file;
2. every directory.

---

# Question 15

Use `find` to count how many `.conf` files exist below the current directory.

---

# Question 16

Use an appropriate command to determine the file type of:

```text
security.log
accounts.csv
scripts/check.py
evidence/empty.bin
```

---

# Question 17

Use:

```text
basename
```

and:

```text
dirname
```

with the path:

```text
/workspaces/scripting-for-cybersecurity/revision02/scripts/check.py
```

Determine:

1. the filename;
2. the directory path.

---

# Question 18

Create:

```text
config-old.txt
```

containing:

```text
port=80
debug=false
timeout=30
```

Create:

```text
config-new.txt
```

containing:

```text
port=443
debug=false
timeout=60
```

Use an appropriate command to display the differences between the two files.

---

# Question 19

Use `find` and `xargs` to run:

```text
file
```

against every file inside:

```text
scripts
```

---

# Question 20

Create:

```text
revision-report.txt
```

containing information similar to:

```text
Labs 3 and 4 Revision Report

Total Security Log Entries: X
Failed Login Attempts: X
Accepted Login Attempts: X
Unique IP Addresses: X

Most Frequent IP:
X

Total Files: X
Total Directories: X
Python Files: X
Configuration Files: X
Empty Files: X
```

All values should be calculated using Linux commands.

Do not manually calculate values that can be generated using:

```text
grep
wc
cut
awk
sort
uniq
find
```

---

# Final GitHub Task

Once all questions are complete:

1. Return to the root of your repository.
2. Confirm that `revision02` exists.
3. Stage your changes.
4. Commit your work.
5. Push to GitHub.

Suggested commit message:

```text
Complete Labs 3 and 4 revision
```

---

# Commands Reviewed

This exercise reviews:

```bash
cat
head
tail
grep
wc
cut
sort
uniq
awk
find
file
basename
dirname
diff
xargs
```

It also reviews:

```text
*
?
pipes
redirection
recursive searching
field extraction
sorting
counting
file discovery
file identification
```

---

# End of Revision Exercise
