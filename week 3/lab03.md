# Lab 3: Text Processing and Log Analysis

## Introduction

In the previous labs, you learned how to:

* use GitHub Codespaces;
* navigate the Linux filesystem;
* create files and directories;
* use variables;
* redirect output;
* combine commands using pipes.

In this lab, we will begin using the Linux command line to **process and analyse text data**.

This is particularly useful in cybersecurity because many important data sources are text-based, including:

* authentication logs;
* web server logs;
* firewall logs;
* application logs;
* lists of IP addresses;
* Indicators of Compromise (IOCs);
* usernames;
* URLs;
* hashes.

The goal is to learn how small Linux tools can be combined to answer useful questions quickly.

---

## Objectives

By the end of this lab, you should be able to:

1. Display different parts of text files.
2. Search text using `grep`.
3. Perform simple pattern matching.
4. Count lines, words, and characters.
5. Extract columns of data.
6. Sort data.
7. Remove duplicate entries.
8. Count repeated values.
9. Combine commands using pipelines.
10. Perform simple cybersecurity log analysis.

---

# Part 1: Set Up Your Lab Directory

Open your existing Codespace for:

```text
scripting-for-cybersecurity
```

Check your current location:

```bash
pwd
```

Return to the root of your repository if necessary.

You should be somewhere similar to:

```text
/workspaces/scripting-for-cybersecurity
```

Create a directory for Lab 3:

```bash
mkdir lab03
cd lab03
```

Confirm your location:

```bash
pwd
```

---

# Part 2: Create a Sample Log File

Create a file called:

```text
auth.log
```

Open it in the editor and add the following sample data:

```text
Sep 20 09:12:01 server sshd[101]: Accepted password for alice from 192.168.1.20
Sep 20 09:13:44 server sshd[102]: Failed password for admin from 203.0.113.10
Sep 20 09:14:02 server sshd[103]: Failed password for root from 203.0.113.10
Sep 20 09:14:20 server sshd[104]: Failed password for admin from 198.51.100.24
Sep 20 09:15:31 server sshd[105]: Accepted password for bob from 192.168.1.35
Sep 20 09:16:02 server sshd[106]: Failed password for root from 203.0.113.10
Sep 20 09:17:55 server sshd[107]: Failed password for test from 198.51.100.24
Sep 20 09:18:10 server sshd[108]: Accepted password for alice from 192.168.1.20
Sep 20 09:19:15 server sshd[109]: Failed password for admin from 203.0.113.15
Sep 20 09:20:22 server sshd[110]: Failed password for guest from 203.0.113.10
Sep 20 09:21:03 server sshd[111]: Accepted password for charlie from 192.168.1.40
Sep 20 09:22:41 server sshd[112]: Failed password for admin from 198.51.100.24
```

Save the file.

Check the contents:

```bash
cat auth.log
```

---

# Part 3: Displaying the Beginning of a File

The `head` command displays the first lines of a file.

Try:

```bash
head auth.log
```

By default, `head` normally displays the first 10 lines.

Display only the first 5 lines:

```bash
head -n 5 auth.log
```

You can also write:

```bash
head -5 auth.log
```

---

# Exercise 1

Use `head` to display:

1. the first 3 lines of `auth.log`;
2. the first 7 lines;
3. the first line only.

---

# Part 4: Displaying the End of a File

The `tail` command displays the final lines of a file.

Try:

```bash
tail auth.log
```

Display only the final 4 lines:

```bash
tail -n 4 auth.log
```

In real cybersecurity work, `tail` is often useful because recent log events normally appear near the end of a log file.

---

# Exercise 2

Use `tail` to display:

1. the final 3 lines;
2. the final 5 lines;
3. the final line only.

---

# Part 5: Following a Log File

One useful option is:

```bash
tail -f auth.log
```

The `-f` option means:

```text
follow
```

This keeps watching the file for new content.

Run:

```bash
tail -f auth.log
```

Then stop it using:

```text
Ctrl + C
```

In a live Linux system, this can be useful for monitoring logs as new events are added.

---

# Part 6: Searching with `grep`

You used `grep` briefly in Lab 2.

The basic syntax is:

```text
grep pattern file
```

Find failed login attempts:

```bash
grep "Failed" auth.log
```

Find successful logins:

```bash
grep "Accepted" auth.log
```

Search for the username `admin`:

```bash
grep "admin" auth.log
```

---

# Exercise 3

Use `grep` to find:

1. all failed password attempts;
2. all successful logins;
3. all entries containing `root`;
4. all entries containing `alice`;
5. all entries involving `203.0.113.10`.

---

# Part 7: Case-Insensitive Searching

By default, `grep` is case-sensitive.

Try:

```bash
grep "failed" auth.log
```

You may receive no output because the file contains:

```text
Failed
```

Use:

```bash
grep -i "failed" auth.log
```

The `-i` option means:

```text
ignore case
```

---

# Part 8: Inverting a Search

Sometimes we want all lines that **do not** match a pattern.

Use:

```bash
grep -v "Failed" auth.log
```

The `-v` option means:

```text
invert match
```

This displays lines that do not contain `Failed`.

---

# Exercise 4

Display:

1. all lines that do not contain `Failed`;
2. all lines that do not contain `Accepted`;
3. all lines that do not contain `192.168`.

---

# Part 9: Counting Matches

You can count matching lines using:

```bash
grep -c "Failed" auth.log
```

Alternatively, use a pipe:

```bash
grep "Failed" auth.log | wc -l
```

Both approaches answer:

> How many failed login entries appear in this file?

---

# Exercise 5

Determine:

1. how many failed login attempts appear;
2. how many accepted logins appear;
3. how many entries mention `admin`;
4. how many entries involve `203.0.113.10`.

---

# Part 10: Line Numbers

Use:

```bash
grep -n "Failed" auth.log
```

The `-n` option displays the line number of each match.

This is useful when analysing large files.

---

# Part 11: Basic Pattern Matching

`grep` can also search for simple patterns.

Try:

```bash
grep "^Sep" auth.log
```

The `^` symbol means:

```text
start of line
```

Try:

```bash
grep "10$" auth.log
```

The `$` symbol means:

```text
end of line
```

Patterns like these form part of **regular expressions**.

We will use regular expressions more extensively later.

---

# Exercise 6

Use `grep` to:

1. display lines beginning with `Sep`;
2. display lines ending in `24`;
3. display lines containing either `admin` or `root` using two separate commands.

---

# Part 12: Counting with `wc`

The `wc` command can count:

```text
-l    lines
-w    words
-c    bytes
```

Try:

```bash
wc -l auth.log
```

Then:

```bash
wc -w auth.log
```

And:

```bash
wc -c auth.log
```

---

# Exercise 7

Determine:

1. how many lines are in `auth.log`;
2. how many words are in the file;
3. how many failed login lines are present.

---

# Part 13: Sorting Data

Create a file called:

```text
ips.txt
```

Add:

```text
203.0.113.10
192.168.1.20
198.51.100.24
203.0.113.10
192.168.1.35
203.0.113.15
198.51.100.24
203.0.113.10
192.168.1.40
198.51.100.24
```

Display it:

```bash
cat ips.txt
```

Sort it:

```bash
sort ips.txt
```

Notice that the original file is unchanged.

Store the sorted output:

```bash
sort ips.txt > sorted_ips.txt
```

---

# Part 14: Removing Duplicates

The `uniq` command removes adjacent duplicate lines.

Try:

```bash
sort ips.txt | uniq
```

Why do we sort first?

Because duplicate values must normally be adjacent for `uniq` to identify them.

---

# Exercise 8

Use commands to:

1. display all unique IP addresses;
2. save the unique IP addresses into `unique_ips.txt`;
3. count the number of unique IP addresses.

Hint:

```bash
sort ips.txt | uniq | wc -l
```

---

# Part 15: Counting Repeated Values

Use:

```bash
sort ips.txt | uniq -c
```

The `-c` option counts how many times each line occurs.

You may see something similar to:

```text
      1 192.168.1.20
      1 192.168.1.35
      1 192.168.1.40
      3 198.51.100.24
      3 203.0.113.10
      1 203.0.113.15
```

---

# Part 16: Sorting Counts

Try:

```bash
sort ips.txt | uniq -c | sort -n
```

This sorts the counts numerically.

To reverse the order:

```bash
sort ips.txt | uniq -c | sort -nr
```

Now the most common values appear first.

This is a very common cybersecurity analysis pattern.

---

# Exercise 9

Use a pipeline to determine:

1. which IP address occurs most frequently;
2. which IP addresses occur only once;
3. how many times `198.51.100.24` appears.

---

# Part 17: Extracting Columns with `cut`

The `cut` command can extract fields from structured text.

Create:

```text
users.csv
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

Display it:

```bash
cat users.csv
```

The separator is a comma.

Use:

```bash
cut -d',' -f1 users.csv
```

Here:

```text
-d','    use comma as the delimiter
-f1      display field 1
```

Display the second field:

```bash
cut -d',' -f2 users.csv
```

---

# Exercise 10

Use `cut` to display:

1. usernames only;
2. account types only;
3. account status only;
4. username and account status.

Hint:

```bash
cut -d',' -f1,3 users.csv
```

---

# Part 18: Combining `grep` and `cut`

Find disabled accounts:

```bash
grep "disabled" users.csv
```

Now display only the usernames:

```bash
grep "disabled" users.csv | cut -d',' -f1
```

---

# Exercise 11

Use pipelines to display:

1. all student usernames;
2. all staff usernames;
3. usernames of disabled accounts;
4. the number of disabled accounts.

---

# Part 19: Extracting IP Addresses from the Log

Look again at:

```bash
cat auth.log
```

The IP address appears as the final field.

The command:

```bash
grep "Failed" auth.log | rev | cut -d' ' -f1 | rev
```

would work, but there is a simpler option using `awk`, which we will cover in a later lab.

For now, because the IP address is the last whitespace-separated field, we can use:

```bash
grep "Failed" auth.log | awk '{print $NF}'
```

You do not need to understand `awk` fully yet.

`$NF` means:

```text
the last field
```

Try:

```bash
grep "Failed" auth.log | awk '{print $NF}'
```

---

# Part 20: Build a Failed Login Report

Now combine several commands:

```bash
grep "Failed" auth.log | awk '{print $NF}' | sort | uniq -c | sort -nr
```

This pipeline:

```text
finds failed logins
        |
extracts IP addresses
        |
sorts them
        |
counts duplicates
        |
sorts by highest count
```

This is the type of compact command-line analysis that is useful in cybersecurity.

---

# Exercise 12: Log Analysis Challenge

Use command pipelines to determine:

1. the total number of failed login attempts;
2. the total number of successful logins;
3. the unique IP addresses involved in failed login attempts;
4. how many failed logins came from each IP address;
5. which IP generated the most failed login attempts;
6. which usernames were targeted by failed login attempts.

For the username field, experiment with:

```bash
grep "Failed" auth.log | awk '{print $9}'
```

---

# Part 21: Redirecting Analysis Results

Create:

```text
failed-logins.txt
```

containing all failed login entries.

Use:

```bash
grep "Failed" auth.log > failed-logins.txt
```

Create:

```text
failed-ip-counts.txt
```

containing the number of failed attempts from each IP.

Use a suitable pipeline and output redirection.

---

# Part 22: Mini Cybersecurity Investigation

You are investigating repeated SSH login failures.

Create a file:

```text
investigation-report.txt
```

It should contain:

```text
SSH Authentication Analysis

Total Log Entries:
Total Failed Logins:
Total Successful Logins:
Unique Failed Login IPs:

Failed Attempts by IP:
```

Use commands and pipelines to calculate the values.

Append the failed-IP counts to the bottom of the report.

Where possible, avoid manually calculating values.

---

# Part 23: Useful Commands from This Lab

You should now have used:

```bash
cat
head
tail
grep
wc
sort
uniq
cut
awk
```

You have also practised:

```text
pipes
redirection
pattern matching
counting
filtering
sorting
extracting fields
```

---

# Part 24: Commit Your Work

Return to the repository root.

Check your location:

```bash
pwd
```

Your repository should contain:

```text
scripting-for-cybersecurity/
├── README.md
├── lab01/
├── lab02/
└── lab03/
```

Use the Source Control interface to:

1. stage your changes;
2. commit them;
3. push them to GitHub.

Suggested commit message:

```text
Complete Lab 3
```

---

# Optional Extension

Investigate the following options:

```bash
grep -r
grep -E
grep -o
sort -u
uniq -d
tail -f
```

For each one:

1. find out what it does;
2. try an example;
3. consider how it might help during log analysis.

---

# End of Lab 3
