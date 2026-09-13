# Lab 2 – Introduction to the Linux Command Line
---

## Learning Outcomes

By the end of this lab you should be able to:

* navigate confidently through the Linux filesystem;
* identify your current location and the contents of directories;
* understand the basic structure of Linux commands;
* use command-line help and documentation;
* create and manipulate files and directories;
* use shell variables and environment variables;
* understand quoting and command expansion;
* use command history and command-line shortcuts;
* redirect command output to files;
* combine commands using pipes;
* construct simple command pipelines useful for cybersecurity tasks.

---

# 1. Opening the Terminal

The Linux command line is accessed through a **terminal**.

Depending on your Linux distribution, you may find the terminal under names such as:

* Terminal
* Console
* Konsole
* GNOME Terminal
* Alacritty
* WezTerm

For our module we'll be using codespaces environment and it's terminal. You are free to use whatever terminal environment you prefer as most of the commands lists should be common across them all.

When you open a terminal you should see a prompt similar to:

```text
student@linux:~$
```

The exact appearance will vary.

The `$` normally indicates that you are operating as a regular user.

For this module you should **not normally need administrator/root privileges**.

---

# 2. Your First Commands

Enter:

```bash
whoami
```

This displays the username of the account you are currently using.

Now enter:

```bash
hostname
```

This displays the name of the computer.

Try:

```bash
date
```

and:

```bash
uptime
```

These commands demonstrate an important feature of Linux:

> Most commands are small programs designed to perform one specific task.

---

## Exercise 1

Find commands that display the following information:

1. Your username.
2. The computer's hostname.
3. The current date and time.
4. How long the computer has been running.

Record the commands below.

```text
Username:

Hostname:

Date:

Uptime:
```

---

# 3. Command Structure

Most Linux commands follow the general format:

```text
command option argument
```

For example:

```bash
ls -l /tmp
```

Here:

```text
ls        command
-l        option
/tmp      argument
```

Options modify how a command behaves.

Arguments normally specify what the command should operate on.

For example:

```bash
ls
```

and:

```bash
ls -l
```

run the same command but produce different output.

Try:

```bash
ls
```

then:

```bash
ls -l
```

and:

```bash
ls -la
```

Notice the difference.

---

# 4. Finding Your Location

Linux files are organised into a hierarchical filesystem.

Your current location is known as the **working directory**.

Display it using:

```bash
pwd
```

`pwd` means:

```text
print working directory
```

You may see something similar to:

```text
/home/student
```

The `/` at the beginning represents the filesystem root.

---

# 5. Listing Directory Contents

The command:

```bash
ls
```

lists files and directories.

Try:

```bash
ls
```

Now try:

```bash
ls -l
```

The `-l` option produces a longer listing.

Try:

```bash
ls -a
```

The `-a` option shows files whose names begin with `.`.

These are often called **hidden files**.

Finally try:

```bash
ls -lah
```

Multiple options can often be combined.

---

## Exercise 2

Use `ls` options to answer the following.

1. How can you display hidden files?

```text
Command:
```

2. How can you display a detailed directory listing?

```text
Command:
```

3. Try the following:

```bash
ls --help
```

Find an option that displays file sizes in a human-readable format.

```text
Option:
```

---

# 6. Navigating the Filesystem

The command used to change directory is:

```bash
cd
```

Try:

```bash
cd /
```

Now check your location:

```bash
pwd
```

Return to your home directory:

```bash
cd ~
```

or simply:

```bash
cd
```

---

## Relative and Absolute Paths

An **absolute path** begins from `/`.

Example:

```bash
cd /tmp
```

A **relative path** begins from your current directory.

For example:

```bash
cd Documents
```

---

## Special Directory Names

Linux provides several useful shortcuts.

```text
.       current directory
..      parent directory
~       your home directory
```

Try:

```bash
cd ~
pwd
```

Now:

```bash
cd ..
pwd
```

Return home:

```bash
cd ~
```

---

## Exercise 3 – Navigation

Starting from your home directory:

```bash
cd ~
```

Complete the following tasks.

1. Move to `/tmp`.

2. Confirm your location.

3. Move to the parent directory.

4. Return to your home directory.

5. List the contents of your home directory.

6. Display hidden files in your home directory.

---

# 7. Tab Completion

Typing long filenames manually is unnecessary.

The Linux shell supports **tab completion**.

Start typing:

```bash
cd /u
```

Now press:

```text
TAB
```

The shell may automatically complete the path.

Try:

```bash
cd /usr/sh
```

and press `TAB`.

Depending on your system it may complete to something such as:

```text
/usr/share/
```

Tab completion is extremely useful when:

* navigating directories;
* working with long filenames;
* entering commands;
* avoiding typing errors.

---

## Exercise 4 – Tab Completion

Navigate to:

```text
/usr/share
```

but use tab completion rather than typing the full path.

Return to your home directory when finished.

---

# 8. Creating a Lab Workspace

Create a directory for today's work.

```bash
cd ~
mkdir cli-lab
```

Move into it:

```bash
cd cli-lab
```

Confirm your location:

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

You can also create several directories with one command:

```bash
mkdir reports notes temp
```

---

# 9. Creating Files

The `touch` command can create empty files.

Try:

```bash
touch notes.txt
```

Confirm that it exists:

```bash
ls -l
```

Create several files:

```bash
touch log1.txt log2.txt log3.txt
```

---

## Exercise 5 – Build a Workspace

Inside `cli-lab`, create the following structure:

```text
cli-lab
├── evidence
├── logs
├── notes
├── reports
├── scripts
└── temp
```

Inside the `logs` directory create:

```text
access.log
auth.log
firewall.log
```

Verify your structure using `ls`.

---

# 10. Displaying File Contents

Create some text:

```bash
echo "Linux command line lab" > notes.txt
```

Display the file:

```bash
cat notes.txt
```

The `cat` command displays file contents.

Try:

```bash
echo "Cybersecurity" >> notes.txt
```

Now:

```bash
cat notes.txt
```

Notice the difference between:

```text
>
```

and:

```text
>>
```

We will examine these in more detail later.

---

# 11. Getting Help

You are **not expected to memorise every Linux command or option**.

Knowing how to find information is much more important.

There are several ways to obtain help.

---

## `--help`

Many commands support:

```bash
command --help
```

For example:

```bash
ls --help
```

or:

```bash
grep --help
```

---

## Manual Pages

Linux contains built-in documentation called **manual pages**.

Try:

```bash
man ls
```

Use:

```text
Arrow Keys     scroll
Space          next page
/word          search
q              quit
```

Search the `ls` manual page for:

```text
human-readable
```

by typing:

```text
/human-readable
```

---

## Searching Manual Pages

Try:

```bash
man -k directory
```

This searches manual page descriptions.

Another useful command is:

```bash
apropos directory
```

---

## Exercise 6 – Learn to Find the Answer

Using `man`, `--help`, or `apropos`, determine:

1. Which option for `ls` sorts files by modification time?

```text
Answer:
```

2. Which command displays the first lines of a file?

```text
Answer:
```

3. Which command displays the final lines of a file?

```text
Answer:
```

4. Which option for `mkdir` allows creation of nested directories?

```text
Answer:
```

---

# 12. Shell Variables

The shell allows information to be stored in variables.

Create a variable:

```bash
course="Cybersecurity"
```

Display it:

```bash
echo $course
```

You should see:

```text
Cybersecurity
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

There must be **no spaces around the `=` sign**.

Correct:

```bash
name="Alice"
```

Incorrect:

```bash
name = "Alice"
```

---

# 13. Using Variables Inside Text

Variables can be inserted into strings.

```bash
student="Alice"
```

Now:

```bash
echo "Hello $student"
```

Output:

```text
Hello Alice
```

Curly brackets can make the variable name clearer:

```bash
echo "Hello ${student}"
```

---

## Exercise 7 – Variables

Create the following variables:

```text
name
course
year
```

Give them suitable values.

Produce a single line of output similar to:

```text
Alice is studying Cybersecurity in Year 2
```

using variables.

Do not type the values directly into the final `echo` command.

---

# 14. Environment Variables

Linux already contains many predefined variables.

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

These are called **environment variables**.

Display all environment variables:

```bash
env
```

---

## Exercise 8

Find the value of the following variables:

```text
USER
HOME
SHELL
PATH
```

Which one contains a list of directories rather than a single value?

```text
Answer:
```

---

# 15. Understanding `$PATH`

When you enter:

```bash
ls
```

you did not specify where the `ls` program was located.

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
which python
```

or:

```bash
which python3
```

Also try:

```bash
which grep
```

---

## Exercise 9

Find the locations of:

```text
bash
python3
grep
cat
```

Record your answers.

```text
bash:

python3:

grep:

cat:
```

---

# 16. Quoting

Quoting is extremely important when writing shell commands and scripts.

Create a variable:

```bash
name="Alice"
```

Try:

```bash
echo "Hello $name"
```

Now:

```bash
echo 'Hello $name'
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

usually treat the text literally.

---

## Exercise 10 – Predict the Output

Before running the commands, predict the output.

```bash
animal="fox"
```

### Command 1

```bash
echo "The $animal is running"
```

Prediction:

```text
```

### Command 2

```bash
echo 'The $animal is running'
```

Prediction:

```text
```

Run both commands and check your answers.

---

# 17. Command Substitution

The output from one command can be stored or inserted into another command.

Try:

```bash
today=$(date)
```

Now:

```bash
echo $today
```

Another example:

```bash
current_directory=$(pwd)
```

Then:

```bash
echo "I am currently in $current_directory"
```

---

## Exercise 11

Create variables containing:

* your username;
* your hostname;
* your current directory.

Use command substitution rather than entering the values manually.

Then produce output similar to:

```text
User alice is logged into workstation01 and is currently in /home/alice/cli-lab
```

---

# 18. Command History

The shell remembers commands you previously entered.

Press:

```text
Up Arrow
```

several times.

You can also display command history using:

```bash
history
```

Try:

```bash
history | tail
```

We will examine the `|` symbol shortly.

---

## Useful History Features

Run your previous command:

```bash
!!
```

For example:

```bash
echo "testing"
!!
```

You can also search command history interactively.

Press:

```text
CTRL + R
```

and type part of a previous command.

Press:

```text
Enter
```

to execute the selected command.

---

# 19. Useful Keyboard Shortcuts

The following shortcuts can make command-line work much faster.

| Shortcut   | Purpose                         |
| ---------- | ------------------------------- |
| `Ctrl+C`   | Stop the current command        |
| `Ctrl+L`   | Clear the screen                |
| `Ctrl+A`   | Move to beginning of line       |
| `Ctrl+E`   | Move to end of line             |
| `Ctrl+U`   | Delete from cursor to beginning |
| `Ctrl+K`   | Delete from cursor to end       |
| `Ctrl+R`   | Search command history          |
| `Tab`      | Command/file completion         |
| `Up Arrow` | Previous command                |

---

## Exercise 12 – Command-Line Editing

Type, but do not execute:

```text
echo this is a very long cybersecurity command
```

Practise:

1. `Ctrl+A`
2. `Ctrl+E`
3. `Ctrl+U`
4. `Ctrl+K`

Then use `Ctrl+R` to locate one of your earlier `mkdir` commands.

---

# 20. Redirecting Output

Normally command output appears on the screen.

We can redirect it into a file.

Run:

```bash
date
```

Now:

```bash
date > timestamp.txt
```

Display the file:

```bash
cat timestamp.txt
```

The `>` symbol means:

```text
send output to a file
```

---

## Warning

Running:

```bash
date > timestamp.txt
```

again **replaces the previous contents**.

To append instead, use:

```bash
date >> timestamp.txt
```

Try several times:

```bash
date >> timestamp.txt
```

Then:

```bash
cat timestamp.txt
```

---

# 21. Redirecting Command Results

You can store almost any command output.

Try:

```bash
ls -la > directory-listing.txt
```

Then:

```bash
cat directory-listing.txt
```

Try:

```bash
whoami > user.txt
hostname > host.txt
```

---

## Exercise 13 – Create a System Snapshot

Create a file called:

```text
snapshot.txt
```

containing:

```text
username
hostname
current date
current directory
```

Use commands and output redirection.

Your file might eventually look similar to:

```text
alice
workstation01
Sun Sep 13 14:31:12 IST 2026
/home/alice/cli-lab
```

Try to complete this using only commands, without manually typing the values.

---

# 22. Pipes

One of the most powerful features of Linux is the ability to connect commands together.

The pipe symbol is:

```text
|
```

A pipe sends the **output of one command into another command**.

Example:

```bash
ls -la | less
```

Instead of displaying everything at once, the output is sent into `less`.

Quit using:

```text
q
```

---

# 23. Counting Output

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

This counts the number of lines produced by `ls`.

Effectively:

```text
ls
 |
 v
wc -l
```

---

## Exercise 14

Use command pipelines to determine:

1. How many items are displayed by:

```bash
ls
```

2. How many lines are displayed by:

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

# 24. Introducing `grep`

`grep` searches text for matching patterns.

Although we will study `grep` in much more detail later, it is extremely useful even for simple command-line work.

Try:

```bash
env | grep USER
```

Now:

```bash
env | grep PATH
```

Try:

```bash
ls /usr/bin | grep python
```

Here:

```text
ls /usr/bin
```

generates a list.

The pipe:

```text
|
```

passes the list to `grep`.

Then:

```text
grep python
```

keeps lines containing `python`.

---

## Exercise 15 – Search Command Output

Use commands and `grep` to:

1. Find environment variables containing the word `USER`.

2. Find files in `/usr/bin` containing `python`.

3. Find files in `/usr/bin` containing `ssh`.

4. Count how many filenames in `/usr/bin` contain the word `python`.

Hint:

```bash
command | grep something | wc -l
```

---

# 25. Building Command Pipelines

Linux commands become particularly powerful when several small commands are combined.

For example:

```bash
ls /usr/bin | grep python | wc -l
```

Read this from left to right.

```text
List /usr/bin
      |
      v
keep entries containing "python"
      |
      v
count the remaining lines
```

---

## Exercise 16 – Pipeline Challenge

Without manually counting anything, determine:

1. How many commands in `/usr/bin` contain `ssh` in their name?

2. How many contain `python`?

3. How many environment variables contain the text `PATH`?

4. How many files are currently visible in your `cli-lab` directory?

Try to solve each problem using a **single command line**.

---

# 26. Combining Variables and Commands

Variables can also contain command results.

Try:

```bash
file_count=$(ls | wc -l)
```

Now:

```bash
echo "There are $file_count items in this directory"
```

Create another:

```bash
python_count=$(ls /usr/bin | grep python | wc -l)
```

Then:

```bash
echo "I found $python_count commands containing python"
```

---

## Exercise 17 – Mini Script Without a Script

Create variables containing:

```text
username
hostname
current directory
number of items in the current directory
```

Then produce output similar to:

```text
User: alice
Computer: workstation01
Directory: /home/alice/cli-lab
Items: 7
```

You should obtain every value using commands rather than typing the values manually.

---

# 27. Cybersecurity Scenario

You have been given access to a Linux workstation during an investigation.

You want to quickly understand the environment without using graphical tools.

Using commands covered in this lab, determine:

```text
Current user
Hostname
Current directory
Shell being used
User's home directory
Location of python3
Location of bash
Number of environment variables
Number of commands in /usr/bin containing "ssh"
```

Store the results in a file called:

```text
investigation.txt
```

You may use:

```bash
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

Your final file should be readable with:

```bash
cat investigation.txt
```

---

# 28. Final Challenge

Complete the following challenge **without using a graphical file manager**.

Create the directory:

```text
~/cli-lab/challenge
```

Inside it create:

```text
users.txt
system.txt
summary.txt
```

### `users.txt`

Store the current username.

### `system.txt`

Store:

```text
hostname
current shell
home directory
```

### `summary.txt`

Produce output similar to:

```text
Cybersecurity CLI Report
User: alice
Host: workstation01
Directory: /home/alice/cli-lab/challenge
Python: /usr/bin/python3
Python commands found: 14
```

Your values will be different.

Where possible:

* use variables;
* use command substitution;
* use pipes;
* use output redirection;
* avoid manually typing values that Linux can determine for you.

---

# 29. Things You Should Now Know

You should now be comfortable using:

```bash
pwd
cd
ls
mkdir
touch
cat
echo
which
env
history
man
grep
wc
```

You should also understand:

```text
~
..
.
$
$()
>
>>
|
" "
' '
```

And you should be using:

```text
Tab
Up Arrow
Ctrl+R
Ctrl+A
Ctrl+E
Ctrl+C
Ctrl+L
```

regularly.

---

# 30. Quick Knowledge Check

Answer the following without looking back through the lab if possible.

### Question 1

What command displays your current working directory?

```text
Answer:
```

### Question 2

What does `..` represent?

```text
Answer:
```

### Question 3

What is the difference between:

```bash
>
```

and:

```bash
>>
```

```text
Answer:
```

### Question 4

What does the pipe character do?

```bash
|
```

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

What does this command do?

```bash
ls /usr/bin | grep python | wc -l
```

```text
Answer:
```

### Question 7

What is the purpose of:

```bash
man
```

```text
Answer:
```

---

# Optional Extension

If you finish early, investigate the following commands using `man` or `--help`.

```bash
head
tail
sort
uniq
cut
file
find
```

For each command:

1. determine what it does;
2. run at least one example;
3. write down one way it could be useful during a cybersecurity investigation.

---

# End of Lab

Before finishing, ensure that your `cli-lab` directory contains the files and directories created during the exercises.

Run:

```bash
cd ~/cli-lab
ls -la
```

You should now have the basic command-line skills required for the scripting exercises later in this module.
