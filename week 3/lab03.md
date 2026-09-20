# Lab 3: Text Processing and Log Analysis

## Introduction

In the previous labs you learned how to navigate Linux, create files and directories, use variables, redirect output, and combine commands with pipes.

In this lab you will use Linux command-line tools to analyse **provided cybersecurity data**.

The supplied `lab03-data` directory contains:

```text
lab03-data/
├── auth.log
├── access.log
├── users.csv
└── iocs.txt
```

All data is synthetic and intended for classroom use.

## Objectives

By the end of this lab, you should be able to:

1. Display selected parts of text files.
2. Search files with `grep`.
3. Use simple regular-expression patterns.
4. Count lines and matches.
5. Extract fields from structured text.
6. Sort data and remove duplicates.
7. Count repeated values.
8. Build useful command pipelines.
9. Perform basic authentication and web-log analysis.
10. Redirect analysis results into report files.

# Part 1: Prepare Your Lab Directory

Open your existing `scripting-for-cybersecurity` Codespace.

Return to the repository root and create:

```bash
mkdir lab03
```

Copy the supplied Lab 3 data into it.

If your lecturer has placed `lab03-data` in the repository root, use:

```bash
cp -r lab03-data/* lab03/
cd lab03
```

Otherwise copy/upload the supplied files into `lab03`.

Check:

```bash
ls -l
```

You should have:

```text
access.log
auth.log
iocs.txt
users.csv
```

# Part 2: Inspect the Dataset

Before analysing a file, get a basic idea of its size and structure.

Try:

```bash
wc -l auth.log
wc -l access.log
head auth.log
head access.log
```

Then:

```bash
tail auth.log
```

## Exercise 1

Determine:

1. how many lines are in `auth.log`;
2. how many lines are in `access.log`;
3. what the first three lines of `auth.log` look like;
4. what the final three lines look like.

# Part 3: `head` and `tail`

Display the first five authentication events:

```bash
head -n 5 auth.log
```

Display the final five:

```bash
tail -n 5 auth.log
```

A useful option for live logs is:

```bash
tail -f auth.log
```

Stop it with:

```text
Ctrl + C
```

`tail -f` is commonly used when monitoring a log that is actively changing.

# Part 4: Searching with `grep`

Find failed logins:

```bash
grep "Failed password" auth.log
```

Find successful logins:

```bash
grep "Accepted password" auth.log
```

Find events involving `admin`:

```bash
grep "admin" auth.log
```

Find events involving a particular IP:

```bash
grep "203.0.113.10" auth.log
```

## Exercise 2

Display:

1. all failed-password events;
2. all accepted-password events;
3. events involving `root`;
4. events involving `203.0.113.10`;
5. events involving an invalid user.

# Part 5: Useful `grep` Options

Ignore case:

```bash
grep -i "failed" auth.log
```

Show line numbers:

```bash
grep -n "Invalid user" auth.log
```

Invert the match:

```bash
grep -v "Failed password" auth.log
```

Count matching lines:

```bash
grep -c "Failed password" auth.log
```

## Exercise 3

Determine:

1. how many failed-password events occurred;
2. how many accepted-password events occurred;
3. how many lines mention `admin`;
4. how many lines mention `203.0.113.10`;
5. how many lines do **not** contain `Failed password`.

# Part 6: Simple Regular Expressions

`grep` supports pattern matching.

`^` means **start of line**:

```bash
grep "^Sep" auth.log
```

`$` means **end of line**.

For example:

```bash
grep "ssh2$" auth.log
```

You can use extended regular expressions with:

```bash
grep -E "admin|root" auth.log
```

This matches either `admin` or `root`.

## Exercise 4

Use `grep` to display:

1. lines beginning with `Sep`;
2. lines ending with `ssh2`;
3. events mentioning either `admin` or `root`;
4. events mentioning either `Invalid user` or `Failed password`.

# Part 7: Counting with `wc`

`wc` can count lines, words and bytes.

```bash
wc -l auth.log
wc -w auth.log
wc -c auth.log
```

It is also useful after another command:

```bash
grep "Failed password" auth.log | wc -l
```

# Part 8: Extracting Fields with `awk`

Linux logs often contain whitespace-separated fields.

Try:

```bash
grep "Failed password" auth.log | awk '{print $1}'
```

Now:

```bash
grep "Failed password" auth.log | awk '{print $NF}'
```

`$NF` means the **last field**.

Because the supplied SSH log contains extra fields after the source IP, inspect a failed-password line carefully:

```bash
grep "Failed password" auth.log | head -1
```

The source IP can be extracted reliably by finding the field after `from`:

```bash
grep "Failed password" auth.log | awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}'
```

Do not worry about memorising that loop yet. The important idea is that command output can be transformed before being passed to another command.

# Part 9: Sort and Count Source IPs

Extract failed-login source addresses:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}'
```

Sort them:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' |
sort
```

Remove duplicates:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' |
sort |
uniq
```

Count each address:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' |
sort |
uniq -c
```

Sort highest first:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' |
sort |
uniq -c |
sort -nr
```

## Exercise 5

Determine:

1. the unique IP addresses associated with failed logins;
2. how many failed attempts came from each IP;
3. which IP produced the most failed attempts;
4. how many unique failed-login source IPs exist.

# Part 10: Extract Targeted Usernames

For normal failed-password lines, the username follows the word `for`.

Try:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="for") print $(i+1)}'
```

Some lines may contain `invalid user`, so inspect your results.

Now count repeated usernames:

```bash
grep "Failed password" auth.log |
awk '{for(i=1;i<=NF;i++) if($i=="for") print $(i+1)}' |
sort |
uniq -c |
sort -nr
```

## Exercise 6

Determine:

1. which usernames were targeted;
2. which username was targeted most often;
3. how many distinct usernames were targeted.

# Part 11: Working with CSV Data

Display:

```bash
cat users.csv
```

Extract the first field:

```bash
cut -d',' -f1 users.csv
```

Extract username and status:

```bash
cut -d',' -f1,3 users.csv
```

Find disabled accounts:

```bash
grep "disabled" users.csv
```

Display only their usernames:

```bash
grep "disabled" users.csv | cut -d',' -f1
```

## Exercise 7

Using `users.csv`, display:

1. usernames only;
2. roles only;
3. usernames and account status;
4. disabled usernames;
5. staff usernames;
6. the number of disabled accounts.

# Part 12: Working with the IOC List

Display:

```bash
cat iocs.txt
```

Compare it with authentication activity.

For example:

```bash
grep -Ff iocs.txt auth.log
```

`-F` treats entries as fixed strings and `-f` reads patterns from a file.

## Exercise 8

Determine:

1. which supplied IOCs appear in `auth.log`;
2. how many authentication-log lines match an IOC;
3. whether any IOC appears in `access.log`.

# Part 13: Web Log Analysis

Inspect:

```bash
head access.log
```

The supplied file uses an Apache-style format.

Find requests to `/admin`:

```bash
grep 'GET /admin ' access.log
```

Find `404` responses:

```bash
grep '" 404 ' access.log
```

Find requests using `sqlmap`:

```bash
grep "sqlmap" access.log
```

## Exercise 9

Determine:

1. how many requests were made to `/admin`;
2. how many responses had status `404`;
3. how many had status `403`;
4. how many requests used `sqlmap`;
5. how many requests attempted to access `/.env`;
6. which source IP appears most often in the web log.

Hint for the final question:

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr
```

# Part 14: Build an Authentication Report

Create:

```text
auth-report.txt
```

It should contain information similar to:

```text
Authentication Analysis

Total Events:
Failed Password Events:
Accepted Password Events:
Invalid User Events:

Failed Login Sources:
```

Use commands to calculate the values.

For example:

```bash
echo "Authentication Analysis" > auth-report.txt
echo "" >> auth-report.txt
echo "Total Events: $(wc -l < auth.log)" >> auth-report.txt
```

Append your failed-IP count pipeline to the bottom of the report.

# Part 15: Build a Web Report

Create:

```text
web-report.txt
```

Include:

```text
Web Access Analysis

Total Requests:
403 Responses:
404 Responses:
Requests to /admin:
Requests to /.env:
sqlmap Requests:

Top Source IPs:
```

Generate the values rather than calculating them manually.

# Part 16: Investigation Challenge

Using the supplied data, answer:

1. Which IP generated the most failed SSH logins?
2. Which account was targeted most frequently?
3. Are any source addresses present in the supplied IOC list?
4. Which source IP generated the most web requests?
5. Are there signs of automated web scanning?
6. Which log entries support your answer?

Store your command output in:

```text
investigation.txt
```

# Part 17: Commands Covered

You should now be comfortable using:

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
```

and combining them with:

```text
|
>
>>
$()
```

# Part 18: Commit Your Work

Do **not** modify the original supplied data.

Commit your reports and any notes/scripts you created.

Suggested commit:

```text
Complete Lab 3
```

Push your changes to GitHub.

# Optional Extension

Investigate:

```text
grep -o
grep -l
grep -Ff
sort -u
uniq -d
tail -f
```

Try each option against the supplied logs.

# End of Lab 3
