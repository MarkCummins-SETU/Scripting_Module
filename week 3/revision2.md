# Labs 3 and 4 Revision Exercise

## Scripting for Cybersecurity

This exercise uses the **same supplied datasets** from Labs 3 and 4.

Create:

```bash
mkdir revision02
```

You may either work against the original `lab03` and `lab04` folders or copy the supplied data into `revision02`.

Complete each task from the command line.

## Question 1

Display the first 5 lines and final 5 lines of `auth.log`.

## Question 2

Count the total number of lines in `auth.log`.

## Question 3

Display all failed-password events and count them.

## Question 4

Display all accepted-password events and count them.

## Question 5

Display all authentication events involving either `admin` or `root`.

## Question 6

Extract the source IP addresses from failed-password events, remove duplicates, and display the unique addresses.

## Question 7

Produce a count of failed-password events per source IP, sorted highest first.

## Question 8

Use `users.csv` to display the usernames of all disabled accounts.

## Question 9

Use `users.csv` to display only staff accounts.

## Question 10

Determine which entries in `iocs.txt` appear in `auth.log`.

## Question 11

Using `access.log`, count the number of `403` and `404` responses.

## Question 12

Find all requests to `/admin` and all requests involving `sqlmap`.

## Question 13

Using the Lab 4 dataset, find every `.py`, `.sh`, `.log`, and `.conf` file.

## Question 14

Count the total number of regular files and directories in Lab 4.

## Question 15

Find all empty files.

## Question 16

Run `file` against every file in the `evidence` directory.

## Question 17

Use `basename` and `dirname` on the full path to `evidence/suspicious.dat`.

## Question 18

Use `diff -u` to compare `config-old.txt` and `config-new.txt` and save the result to `config-changes.txt`.

## Question 19

Use recursive searching to identify every file containing `admin`, `BLOCK`, or `password123`.

## Question 20

Create `revision-report.txt` containing:

```text
Labs 3 and 4 Revision Report

Authentication Log Entries:
Failed Password Events:
Accepted Password Events:
Unique Failed Login IPs:
Most Frequent Failed Login IP:

Web Requests:
403 Responses:
404 Responses:

Lab 4 Files:
Lab 4 Directories:
Python Files:
Shell Scripts:
Log Files:
Configuration Files:
Empty Files:
```

All values must be generated using commands and pipelines rather than manually calculated.

## Final Task

Commit and push:

```text
revision-report.txt
config-changes.txt
```

Suggested commit message:

```text
Complete Labs 3 and 4 revision
```

## Commands Reviewed

```text
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
unzip
```

# End of Revision Exercise
