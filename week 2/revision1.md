# Labs 1 and 2 Revision Exercises

## Scripting for Cybersecurity

Complete the following 20 short tasks using your existing GitHub Codespace and `scripting-for-cybersecurity` repository.

Where possible, complete each task using the terminal rather than the graphical interface.

Create a new directory for this exercise:

```bash
mkdir revision01
cd revision01
```

---

## Question 1

Display your current working directory.

---

## Question 2

List all files and directories in your current location, including hidden files, using a detailed listing.

---

## Question 3

Display:

* your Linux username;
* the hostname;
* the current date and time.

Use three separate commands.

---

## Question 4

Create the following directory structure:

```text
revision01/
├── evidence/
├── logs/
├── notes/
└── scripts/
```

---

## Question 5

Inside the `logs` directory, create the following empty files:

```text
access.log
auth.log
firewall.log
```

---

## Question 6

Without typing the full directory name manually, use **tab completion** to move from `revision01` into the `evidence` directory.

Then return to `revision01`.

---

## Question 7

Create a file called:

```text
student.txt
```

Use `echo` and output redirection to store your username in the file.

Display the contents of the file using another command.

---

## Question 8

Append your current hostname and current date to `student.txt`.

Do not overwrite the existing username.

Display the finished file.

---

## Question 9

Use the built-in help system to find the option for `ls` that displays file sizes in a human-readable format.

Then run `ls` using that option together with a detailed listing.

---

## Question 10

Use either `man` or `--help` to determine which `mkdir` option can create parent directories when required.

Use that option to create:

```text
reports/weekly/week01
```

with a single command.

---

## Question 11

Create three shell variables called:

```text
name
course
year
```

Give them suitable values.

Use one `echo` command to produce output similar to:

```text
Alex is studying Cybersecurity in Year 2
```

The final `echo` command must use the variables.

---

## Question 12

Display the values of the following environment variables:

```text
USER
HOME
SHELL
PATH
```

Which of these contains multiple directory paths?

---

## Question 13

Use an appropriate command to find the location of:

```text
python3
bash
grep
cat
```

---

## Question 14

Create the following variable:

```bash
module="Scripting"
```

Run two commands so that the first produces:

```text
Module: Scripting
```

and the second produces:

```text
Module: $module
```

Use quoting correctly to achieve the different results.

---

## Question 15

Use command substitution to create variables containing:

* your username;
* your hostname;
* your current working directory.

Use them to display a sentence similar to:

```text
User Alex is logged into codespaces and is currently in /workspaces/scripting-for-cybersecurity/revision01
```

---

## Question 16

Use your command history to locate and re-run one of the `mkdir` commands you used earlier.

Then use:

```text
Ctrl + R
```

to search for one of your previous `echo` commands.

---

## Question 17

Use a pipe and `wc` to determine:

1. how many items are displayed by `ls`;
2. how many environment variables are displayed by `env`.

---

## Question 18

Use `grep` and pipes to:

1. display environment variables containing `PATH`;
2. display filenames in `/usr/bin` containing `python`;
3. count how many filenames in `/usr/bin` contain `ssh`.

---

## Question 19

Create a variable called:

```text
python_count
```

Its value should be the number of filenames in `/usr/bin` containing `python`.

Then display:

```text
Python-related filenames found: X
```

where `X` comes from the variable.

---

## Question 20

Create a file called:

```text
revision-report.txt
```

The finished file should contain information similar to:

```text
Linux CLI Revision Report
User: Alex
Host: codespaces
Directory: /workspaces/scripting-for-cybersecurity/revision01
Shell: /bin/bash
Python: /usr/bin/python3
Environment variables: 42
Python-related filenames: 14
```

All system-specific values must be obtained using commands.

Where appropriate, use:

```text
variables
command substitution
pipes
redirection
```

Do not manually type values that Linux can determine for you.

---

# Final GitHub Task

Once you have completed all 20 questions:

1. Return to the root of your `scripting-for-cybersecurity` repository.
2. Check that the `revision01` directory is present.
3. Open the Source Control panel in Codespaces.
4. Stage your work.
5. Commit it using a message such as:

```text
Complete Labs 1 and 2 revision
```

6. Push your commit to GitHub.
7. Open your GitHub repository in the browser and confirm that the `revision01` directory and files are visible.

---

# Commands and Features Covered

This revision exercise uses or reviews:

```text
pwd
ls
cd
mkdir
touch
cat
echo
whoami
hostname
date
env
which
history
man
grep
wc
```

It also reviews:

```text
Tab completion
Ctrl + R
variables
environment variables
single quotes
double quotes
command substitution
>
>>
|
Git commits
GitHub pushes
Codespaces
```
