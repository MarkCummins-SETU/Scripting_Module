# Lab 2: Introduction to the Linux Command Line

## Introduction

In the previous lab you created a GitHub repository and launched a GitHub Codespace.

That Codespace provides us with a Linux development environment.

In this lab we will begin working directly with the **Linux command line**.

For cybersecurity work, being comfortable using the command line is an essential skill.

Throughout this module we will build on these commands and eventually use them to:

* process files;
* search logs;
* automate repetitive tasks;
* write Bash scripts;
* manipulate data;
* interact with cybersecurity tools.

---

## Objectives

By the end of this lab, you should be able to:

1. Understand the basic structure of Linux commands.
2. Determine your current location in the filesystem.
3. Navigate between directories.
4. List files and directories.
5. Create files and directories.
6. Use tab completion and command history.
7. Find help for unfamiliar commands.
8. Create and use shell variables.
9. Understand basic quoting and variable expansion.
10. Use command substitution.
11. Redirect command output.
12. Combine commands using pipes.
13. Build simple command pipelines.

---

# Part 1: Open Your Codespace

Open your GitHub repository:

```text
scripting-for-cybersecurity
```

Launch the Codespace you created during Lab 1.

Open a terminal.

You should normally begin inside your Git repository.

Enter:

```bash
pwd
```

You should see something similar to:

```text
/workspaces/scripting-for-cybersecurity
```

The exact path may differ slightly.

The command:

```bash
pwd
```

means:

```text
print working directory
```

It tells us our current location.

---

# Part 2: Your First Linux Commands

Try:

```bash
whoami
```

This displays your current Linux username.

Now try:

```bash
hostname
```

This displays the hostname of the Linux system.

Try:

```bash
date
```

Finally:

```bash
pwd
```

These commands each perform a small, specific task.

This is an important Linux philosophy:

> Small commands can be combined to perform larger tasks.

---

# Exercise 1: Basic Commands

Find commands that display:

1. Your current username.
2. The system hostname.
3. The current date and time.
4. Your current working directory.

Record the commands in your notes.

---

# Part 3: Understanding Command Structure

Many Linux commands follow this general structure:

```text
command option argument
```

For example:

```bash
ls -l /workspaces
```

Here:

```text
ls            command
-l            option
/workspaces   argument
```

The command specifies what we want to do.

The option modifies how the command behaves.

The argument specifies what the command should operate on.

---

# Part 4: Listing Files

The `ls` command lists files and directories.

Try:

```bash
ls
```

You should see something similar to:

```text
README.md
lab01
```

Try:

```bash
ls -l
```

The `-l` option produces a more detailed listing.

Now try:

```bash
ls -a
```

The `-a` option also shows hidden files.

You may now see files or directories beginning with a `.`.

For example:

```text
.git
```

Files beginning with `.` are normally hidden from a standard `ls` listing.

Try combining options:

```bash
ls -la
```

---

# Exercise 2: Exploring `ls`

Find commands that:

1. Display files normally.
2. Display a detailed listing.
3. Display hidden files.
4. Display a detailed listing including hidden files.

---

# Part 5: Create Your Lab 2 Directory

Make sure you are at the root of your Git repository.

Run:

```bash
pwd
```

You should be somewhere similar to:

```text
/workspaces/scripting-for-cybersecurity
```

Create a new directory:

```bash
mkdir lab02
```

Move into it:

```bash
cd lab02
```

Confirm your location:

```bash
pwd
```

You should now see something similar to:

```text
/workspaces/scripting-for-cybersecurity/lab02
```

All files created during this lab should remain somewhere inside this `lab02` directory.

This ensures that Git can track them.

---

# Part 6: Navigating Directories

The command:

```bash
cd
```

means:

```text
change directory
```

Move to the parent directory:

```bash
cd ..
```

Check your location:

```bash
pwd
```

Move back into `lab02`:

```bash
cd lab02
```

---

## Special Path Symbols

Linux provides some useful shortcuts.

```text
.     current directory

..    parent directory

~     your home directory
```

For example:

```bash
cd ..
```

moves up one directory.

Be careful with:

```bash
cd ~
```

This takes you to the Codespaces user's home directory.

That directory is **not necessarily inside your Git repository**.

For this module, most of your work should remain inside:

```text
/workspaces/scripting-for-cybersecurity
```

or one of its subdirectories.

---

# Exercise 3: Navigation

Starting inside `lab02`:

1. Display your current directory.
2. Move to the parent directory.
3. List its contents.
4. Move back into `lab02`.
5. Confirm your location.

---

# Part 7: Tab Completion

Linux shells provide **tab completion**.

This avoids typing long commands and filenames manually.

Move to the repository root:

```bash
cd ..
```

Start typing:

```text
cd lab
```

Press:

```text
TAB
```

Depending on the files present, the shell may complete the directory name or show possible matches.

Try navigating back into `lab02` using tab completion.

Tab completion is useful for:

* commands;
* filenames;
* directory names;
* long paths.

It also reduces typing errors.

---

# Part 8: Creating Directories

Make sure you are inside `lab02`.

Check:

```bash
pwd
```

Create three directories:

```bash
mkdir logs scripts evidence
```

List them:

```bash
ls
```

Now create three more:

```bash
mkdir reports notes temp
```

Your directory should now contain:

```text
lab02/
├── evidence/
├── logs/
├── notes/
├── reports/
├── scripts/
└── temp/
```

---

# Part 9: Creating Files

The `touch` command can create empty files.

Try:

```bash
touch notes.txt
```

List the directory:

```bash
ls
```

Create several files:

```bash
touch file1.txt file2.txt file3.txt
```

---

# Exercise 4: Create a Workspace

Inside the `logs` directory create:

```text
access.log
auth.log
firewall.log
```

You could first move into the directory:

```bash
cd logs
```

and then create the files.

When finished, return to `lab02`.

Check your location using:

```bash
pwd
```

---

# Part 10: Displaying Text

The `echo` command displays text.

Try:

```bash
echo "Hello Linux"
```

Try:

```bash
echo "Scripting for Cybersecurity"
```

The text is displayed in the terminal.

---

# Part 11: Writing Text to a File

Run:

```bash
echo "Linux command line lab" > notes.txt
```

Now display the contents:

```bash
cat notes.txt
```

You should see:

```text
Linux command line lab
```

The `cat` command can be used to display the contents of a text file.

Now run:

```bash
echo "Scripting for Cybersecurity" >> notes.txt
```

Display the file again:

```bash
cat notes.txt
```

You should now see both lines.

---

# Part 12: Redirection

The symbols:

```text
>
```

and:

```text
>>
```

redirect command output.

### `>`

This writes output to a file.

If the file already exists, its previous contents are replaced.

Example:

```bash
date > timestamp.txt
```

### `>>`

This appends output to the end of a file.

Example:

```bash
date >> timestamp.txt
```

Try running:

```bash
date >> timestamp.txt
```

several times.

Then:

```bash
cat timestamp.txt
```

---

# Exercise 5: Redirection

Create a file called:

```text
system.txt
```

Use commands and redirection to store:

1. your username;
2. the hostname;
3. the current date;
4. your current directory.

Display the finished file using:

```bash
cat system.txt
```

Do not type the values manually.

---

# Part 13: Getting Help

You are not expected to memorise every Linux command or option.

Being able to find help is more important.

Many commands support:

```bash
command --help
```

For example:

```bash
ls --help
```

Try:

```bash
mkdir --help
```

and:

```bash
grep --help
```

---

# Part 14: Manual Pages

Linux also provides documentation called **manual pages**.

Try:

```bash
man ls
```

Useful keys include:

```text
Arrow keys    Scroll

Space         Next page

/word         Search

q             Quit
```

Search the manual for:

```text
human-readable
```

by entering:

```text
/human-readable
```

Press `q` to exit.

---

# Exercise 6: Find the Answer

Using `man` or `--help`, determine:

1. Which `ls` option displays human-readable file sizes?
2. Which `ls` option sorts by modification time?
3. Which `mkdir` option allows creation of parent directories if required?
4. What does `cat` do?

Try to find the answers rather than searching the Internet.

---

# Part 15: Shell Variables

Shell variables allow us to store values.

Create a variable:

```bash
course="Cybersecurity"
```

Display it:

```bash
echo $course
```

Create another:

```bash
year=2
```

Display both:

```bash
echo $course $year
```

---

## Important

There must be no spaces around the `=` sign.

Correct:

```bash
name="Alex"
```

Incorrect:

```bash
name = "Alex"
```

---

# Exercise 7: Variables

Create variables called:

```text
name
course
year
```

Give them suitable values.

Use them to display a sentence similar to:

```text
Alex is studying Cybersecurity in Year 2
```

Do not type the values directly into the final `echo` command.

---

# Part 16: Environment Variables

Linux already provides a number of useful variables.

Try:

```bash
echo $HOME
```

```bash
echo $USER
```

```bash
echo $SHELL
```

```bash
echo $PATH
```

These are examples of **environment variables**.

Display environment variables using:

```bash
env
```

---

# Exercise 8: Environment Variables

Display the values of:

```text
USER
HOME
SHELL
PATH
```

Which variable contains multiple directory paths?

---

# Part 17: Understanding `$PATH`

When you type:

```bash
ls
```

you do not specify where the `ls` program is located.

The shell searches directories listed in:

```bash
$PATH
```

Try:

```bash
which ls
```

You may see:

```text
/usr/bin/ls
```

Try:

```bash
which python3
```

```bash
which grep
```

```bash
which bash
```

---

# Exercise 9: Finding Commands

Find the location of:

```text
bash
python3
grep
cat
```

---

# Part 18: Quoting

Quoting becomes very important when working with shell commands and scripts.

Create:

```bash
animal="fox"
```

Try:

```bash
echo "The $animal is running"
```

Now try:

```bash
echo 'The $animal is running'
```

Notice the difference.

Double quotes:

```text
" "
```

allow variable expansion.

Single quotes:

```text
' '
```

normally treat the contents literally.

---

# Exercise 10: Predict the Output

Create:

```bash
module="Scripting"
```

Before running the following commands, predict their output.

```bash
echo "Module: $module"
```

Prediction:

```text
```

Now:

```bash
echo 'Module: $module'
```

Prediction:

```text
```

Run both commands and check your answers.

---

# Part 19: Command Substitution

The output from a command can be stored in a variable.

Try:

```bash
today=$(date)
```

Display it:

```bash
echo "$today"
```

Create another variable:

```bash
current_directory=$(pwd)
```

Now:

```bash
echo "I am currently in $current_directory"
```

The syntax:

```text
$(command)
```

means:

> Run the command and substitute its output here.

---

# Exercise 11: Command Substitution

Create variables containing:

* your username;
* the hostname;
* your current directory.

Use commands to obtain each value.

For example:

```bash
username=$(whoami)
```

Produce output similar to:

```text
User Alex is logged into codespaces and is currently in /workspaces/scripting-for-cybersecurity/lab02
```

---

# Part 20: Command History

The Linux shell remembers commands you have entered.

Press:

```text
Up Arrow
```

several times.

You should see previous commands.

Display your command history:

```bash
history
```

You can also search your history.

Press:

```text
Ctrl + R
```

Start typing part of an earlier command.

The shell will search backwards through your history.

---

# Part 21: Useful Keyboard Shortcuts

Practise the following shortcuts.

| Shortcut   | Purpose                          |
| ---------- | -------------------------------- |
| `Tab`      | Complete commands and filenames  |
| `Up Arrow` | Previous command                 |
| `Ctrl + R` | Search command history           |
| `Ctrl + A` | Beginning of line                |
| `Ctrl + E` | End of line                      |
| `Ctrl + U` | Delete towards beginning of line |
| `Ctrl + K` | Delete towards end of line       |
| `Ctrl + C` | Stop the current command         |
| `Ctrl + L` | Clear the terminal               |

These shortcuts become very useful once you start spending significant time at the command line.

---

# Exercise 12: Command-Line Editing

Type, but do not immediately execute:

```text
echo this is a very long cybersecurity command
```

Practise:

```text
Ctrl + A
Ctrl + E
Ctrl + U
Ctrl + K
```

Then use:

```text
Ctrl + R
```

to locate one of your earlier `mkdir` commands.

---

# Part 22: Pipes

One of the most useful Linux features is the ability to send the output of one command into another.

The pipe symbol is:

```text
|
```

Example:

```bash
ls -la | less
```

The output from:

```bash
ls -la
```

is sent into:

```bash
less
```

Press:

```text
q
```

to exit `less`.

Conceptually:

```text
command 1
    |
    v
command 2
```

---

# Part 23: Counting Output with `wc`

The `wc` command can count:

* lines;
* words;
* characters.

Try:

```bash
ls
```

Now:

```bash
ls | wc -l
```

The output from `ls` is sent into:

```bash
wc -l
```

which counts lines.

---

# Exercise 13: Counting

Use pipelines to determine:

1. How many items are displayed by:

```bash
ls
```

2. How many lines are produced by:

```bash
ls -la
```

3. How many environment variables are displayed by:

```bash
env
```

Hint:

```bash
command | wc -l
```

---

# Part 24: Introducing `grep`

`grep` searches text.

We will study `grep` in much more detail in a later lab.

For now, try:

```bash
env | grep USER
```

Try:

```bash
env | grep PATH
```

Now:

```bash
ls /usr/bin | grep python
```

This pipeline performs two steps:

```text
ls /usr/bin
      |
      v
grep python
```

The first command generates output.

The second command keeps only lines containing:

```text
python
```

---

# Exercise 14: Searching Command Output

Use commands and `grep` to:

1. Find environment variables containing `USER`.
2. Find filenames in `/usr/bin` containing `python`.
3. Find filenames in `/usr/bin` containing `ssh`.
4. Count filenames in `/usr/bin` containing `python`.

Hint:

```bash
command | grep something | wc -l
```

---

# Part 25: Building Pipelines

Linux commands become particularly powerful when several commands are combined.

For example:

```bash
ls /usr/bin | grep python | wc -l
```

Read this from left to right:

```text
List /usr/bin
      |
      v
Keep entries containing "python"
      |
      v
Count the remaining lines
```

---

# Exercise 15: Pipeline Challenge

Using a **single command line** for each answer, determine:

1. How many filenames in `/usr/bin` contain `ssh`?
2. How many contain `python`?
3. How many environment variables contain `PATH`?
4. How many items are visible in your current `lab02` directory?

Do not count anything manually.

---

# Part 26: Variables and Command Pipelines

A variable can store the result of an entire pipeline.

Try:

```bash
file_count=$(ls | wc -l)
```

Now:

```bash
echo "There are $file_count items in this directory"
```

Try:

```bash
python_count=$(ls /usr/bin | grep python | wc -l)
```

Then:

```bash
echo "I found $python_count filenames containing python"
```

---

# Exercise 16: Build a Simple Report

Create variables containing:

* username;
* hostname;
* current directory;
* number of items in the current directory.

Display:

```text
User: Alex
Computer: codespaces
Directory: /workspaces/scripting-for-cybersecurity/lab02
Items: 10
```

All values should be obtained using commands.

---

# Part 27: Cybersecurity Scenario

Imagine you have opened a terminal during a basic investigation of a Linux environment.

Determine:

```text
Current user
Hostname
Current directory
Current shell
User home directory
Location of python3
Location of bash
Number of environment variables
Number of filenames in /usr/bin containing ssh
```

Create a file:

```text
investigation.txt
```

containing the results.

You may use:

```text
echo
whoami
hostname
pwd
which
env
grep
wc
>
>>
$
$()
|
```

Display the finished report:

```bash
cat investigation.txt
```

---

# Part 28: Final Challenge

Inside `lab02`, create:

```text
challenge/
```

Move into it.

Create:

```text
user.txt
system.txt
summary.txt
```

## `user.txt`

Store your current username.

## `system.txt`

Store:

* hostname;
* shell;
* home directory.

## `summary.txt`

Produce something similar to:

```text
Cybersecurity CLI Report
User: Alex
Host: codespaces
Directory: /workspaces/scripting-for-cybersecurity/lab02/challenge
Python: /usr/bin/python3
Python filenames found: 14
```

Your values may differ.

Where possible, use:

* variables;
* command substitution;
* pipes;
* output redirection.

Avoid manually typing information that Linux can obtain for you.

---

# Part 29: Quick Knowledge Check

Answer the following.

### Question 1

What command displays your current working directory?

```text
Answer:
```

### Question 2

What does:

```text
..
```

represent?

```text
Answer:
```

### Question 3

What is the difference between:

```text
>
```

and:

```text
>>
```

```text
Answer:
```

### Question 4

What does:

```text
|
```

do?

```text
Answer:
```

### Question 5

What is the difference between:

```bash
echo "$USER"
```

and:

```bash
echo '$USER'
```

```text
Answer:
```

### Question 6

Explain:

```bash
ls /usr/bin | grep python | wc -l
```

```text
Answer:
```

### Question 7

Why is:

```bash
cd ~
```

not necessarily a good place to create your coursework inside Codespaces?

```text
Answer:
```

---

# Part 30: Check Your Repository

Return to the repository root.

If you are currently inside:

```text
lab02/challenge
```

you could move upwards:

```bash
cd ../..
```

Check your location:

```bash
pwd
```

Your repository should now contain approximately:

```text
scripting-for-cybersecurity/
├── README.md
├── lab01/
└── lab02/
```

List the contents:

```bash
ls
```

---

# Part 31: Commit Your Work

For now, use the Visual Studio Code **Source Control** interface.

Stage your Lab 2 files.

Use a commit message such as:

```text
Complete Lab 2
```

Commit and push your work.

Return to GitHub and verify that `lab02` appears in your repository.

---

# Part 32: Update Your README

Add Lab 2 to your repository README.

For example:

```markdown
## Labs

- Lab 01 - Development Environment
- Lab 02 - Linux Command Line
```

Commit and push the change.

---

# Commands Introduced in This Lab

You should now have used:

```bash
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
less
```

You should also understand:

```text
.
..
~
$
$()
>
>>
|
" "
' '
```

---

# Optional Extension

If you finish early, investigate the following commands using `man` or `--help`:

```bash
head
tail
sort
uniq
cut
file
```

For each command:

1. determine what it does;
2. run at least one example;
3. consider how it might be useful when analysing cybersecurity data.

Do not worry if you do not fully understand them yet.

We will use several of these commands in the next lab.

---

# Preparing for the Next Lab

In the next command-line lab we will work with text and log data using commands such as:

```text
grep
head
tail
sort
uniq
cut
wc
```

We will start combining these tools into more useful cybersecurity-focused pipelines.

---

# End of Lab 2
