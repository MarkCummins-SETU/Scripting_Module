# Lab 4: Finding Files and Working with Data

## Introduction

In Lab 3 you analysed provided logs and structured text.

In this lab you will work with a supplied directory tree containing a mixture of:

- logs;
- scripts;
- configuration files;
- backups;
- documents;
- an archive;
- an image;
- an empty binary;
- a binary-like file.

Your job is to **discover and classify the files using Linux commands** rather than simply browsing them in the graphical file explorer.

## Objectives

By the end of this lab, you should be able to:

1. Match filenames with wildcards.
2. Locate files using `find`.
3. Search by name, type, size and modification time.
4. Identify files with `file`.
5. Work with paths using `basename` and `dirname`.
6. Compare files using `diff`.
7. Search recursively with `grep`.
8. Use `xargs`.
9. Combine discovery and text-processing commands.
10. Perform basic file triage.

# Part 1: Prepare Lab 4

Return to the root of your repository.

Create:

```bash
mkdir lab04
```

Copy the supplied contents of `lab04-data` into it.

If `lab04-data` is in the repository root:

```bash
cp -r lab04-data/* lab04/
cd lab04
```

Avoid using the graphical Explorer initially.

Run:

```bash
pwd
ls
```

# Part 2: Explore from the Command Line

Start with:

```bash
find .
```

Then:

```bash
find . -type d
```

and:

```bash
find . -type f
```

## Exercise 1

Without using the graphical file browser, determine:

1. how many directories exist below `lab04`;
2. how many regular files exist;
3. which top-level directories are present.

# Part 3: Wildcards

List Python files:

```bash
ls scripts/*.py
```

List configuration files:

```bash
ls configs/*.conf
```

Use `*` to match zero or more characters.

The `?` wildcard matches exactly one character.

## Exercise 2

Use wildcards to display:

1. all `.py` files;
2. all `.log` files directly inside `logs`;
3. all `.conf` files;
4. all `.txt` files directly inside `evidence`;
5. all filenames beginning with `config` in the current directory.

# Part 4: Searching with `find`

Search for every Python file:

```bash
find . -name "*.py"
```

Find every log:

```bash
find . -name "*.log"
```

Case-insensitive search:

```bash
find . -iname "*.PY"
```

Only regular files:

```bash
find . -type f -name "*.log"
```

## Exercise 3

Locate:

1. every `.py` file;
2. every `.conf` file;
3. every `.old` file;
4. every `.log` file, including logs in nested directories;
5. every file whose name contains `config`.

# Part 5: Search Specific Locations

Search only inside `evidence`:

```bash
find evidence -type f
```

Search only scripts:

```bash
find scripts -type f
```

## Exercise 4

Determine:

1. how many files are inside `evidence`;
2. how many files are inside `scripts`;
3. how many files exist under `nested`.

# Part 6: Identify Files with `file`

Do not assume a filename extension tells you what a file really contains.

Run:

```bash
file evidence/*
```

Then:

```bash
file scripts/*
```

Look particularly at:

```text
evidence/image.png
evidence/archive.zip
evidence/empty.bin
evidence/suspicious.dat
```

## Exercise 5

Record what `file` reports for:

1. `image.png`;
2. `archive.zip`;
3. `empty.bin`;
4. `suspicious.dat`;
5. `scan.py`;
6. `check.sh`.

Which result would deserve additional investigation during file triage?

# Part 7: Paths with `basename` and `dirname`

Try:

```bash
basename "$(pwd)/scripts/scan.py"
```

Then:

```bash
dirname "$(pwd)/scripts/scan.py"
```

## Exercise 6

Use `basename` and `dirname` with:

```text
<your-lab04-path>/evidence/suspicious.dat
```

Determine:

1. its filename;
2. its parent directory.

# Part 8: Compare Configuration Files

Two files are provided:

```text
config-old.txt
config-new.txt
```

Inspect:

```bash
cat config-old.txt
cat config-new.txt
```

Compare them:

```bash
diff config-old.txt config-new.txt
```

Try:

```bash
diff -u config-old.txt config-new.txt
```

The unified format is commonly easier to read.

## Exercise 7

Identify every setting that changed between the two files.

Save the unified difference to:

```text
config-changes.txt
```

# Part 9: Recursive `grep`

Search the entire Lab 4 directory:

```bash
grep -r "admin" .
```

Search for:

```bash
grep -r "BLOCK" .
```

Search only filenames containing a match:

```bash
grep -rl "admin" .
```

## Exercise 8

Determine which files contain:

1. `admin`;
2. `BLOCK`;
3. `8080`;
4. `Scanning`;
5. `password123`.

For each search, identify the filename as well as the matching content.

# Part 10: Find Empty Files

Use:

```bash
find . -type f -size 0
```

Count them:

```bash
find . -type f -size 0 | wc -l
```

Find non-empty files:

```bash
find . -type f -size +0c
```

## Exercise 9

Determine:

1. which files are empty;
2. how many empty files exist;
3. how many non-empty files exist.

# Part 11: Recently Modified Files

Use:

```bash
find . -type f -mmin -60
```

This finds files modified in approximately the last 60 minutes.

Depending on when the dataset was copied into your Codespace, most files may match.

Try narrower and wider values:

```bash
find . -type f -mmin -10
find . -type f -mmin -1440
```

The important skill is understanding how modification-time searches work.

# Part 12: Counting File Types

Count Python files:

```bash
find . -type f -name "*.py" | wc -l
```

Count logs:

```bash
find . -type f -name "*.log" | wc -l
```

## Exercise 10

Determine the number of:

1. Python files;
2. shell scripts;
3. log files;
4. configuration files;
5. text files;
6. ZIP archives.

# Part 13: Introducing `xargs`

Find all scripts:

```bash
find scripts -type f
```

Pass them into `file`:

```bash
find scripts -type f | xargs file
```

Run `wc -l` against configuration files:

```bash
find configs -type f -name "*.conf" | xargs wc -l
```

## Exercise 11

Use `find` and `xargs` to:

1. run `file` against all files inside `evidence`;
2. run `wc -l` against all `.log` files;
3. display the contents of all `.conf` files.

# Part 14: Safer Filename Handling

Simple `xargs` commands can fail with filenames containing spaces.

A safer pattern is:

```bash
find . -type f -print0 | xargs -0 file
```

You do not need to memorise this immediately, but you should understand why it exists.

# Part 15: Combine `find` and `grep`

One way to search all configuration files is:

```bash
find . -type f -name "*.conf" | xargs grep "port"
```

A simpler alternative in many cases is recursive `grep`.

Compare:

```bash
grep -r "port" configs
```

with:

```bash
find configs -type f -name "*.conf" | xargs grep "port"
```

## Exercise 12

Use suitable commands to determine:

1. which configuration files contain `port`;
2. which logs contain `203.0.113.10`;
3. which files anywhere in the dataset contain `admin`;
4. which files contain the string `debug`.

# Part 16: Archive Discovery

Locate ZIP archives:

```bash
find . -type f -name "*.zip"
```

Identify them:

```bash
find . -type f -name "*.zip" | xargs file
```

You can inspect the supplied ZIP without extracting it using:

```bash
unzip -l evidence/archive.zip
```

## Exercise 13

Determine:

1. the ZIP archive's location;
2. its file type;
3. what file is stored inside it.

# Part 17: File Triage Challenge

Imagine this directory was collected from a workstation during an investigation.

Without opening everything manually, determine:

1. total number of files;
2. total number of directories;
3. all scripts;
4. all log files;
5. all configuration files;
6. all empty files;
7. all archive files;
8. files containing `admin`;
9. files containing passwords;
10. anything whose detected file type looks more interesting than its filename suggests.

# Part 18: Create a Triage Report

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
Shell Scripts:
Log Files:
Configuration Files:
Empty Files:
Archives:

Files Containing "admin":

Detected File Types in Evidence:
```

Generate as much of the report as possible using commands.

Example:

```bash
echo "File Triage Report" > triage-report.txt
echo "" >> triage-report.txt
echo "Total Files: $(find . -type f | wc -l)" >> triage-report.txt
```

Append appropriate command output to the report.

# Part 19: Commands Covered

You should now have used:

```text
find
file
basename
dirname
diff
xargs
grep
wc
cat
unzip
```

and search criteria including:

```text
-name
-iname
-type
-size
-mmin
```

plus wildcards:

```text
*
?
```

# Part 20: Commit Your Work

Do not alter the original supplied dataset unnecessarily.

Commit:

- `triage-report.txt`;
- `config-changes.txt`;
- any notes or command files you created.

Suggested commit:

```text
Complete Lab 4
```

Push your work to GitHub.

# Optional Extension

Investigate:

```text
find . -maxdepth
find . -mindepth
find . -exec
grep -rl
diff -u
du -h
```

# Preparing for the Next Lab

You have now built command pipelines that solve repeatable tasks.

The next step is to place those commands inside **Bash scripts** so the tasks can be automated and reused.

# End of Lab 4
