# Lab 1: Setting Up Your Development Environment

## Introduction

Throughout this module, we will use **GitHub**, **Git**, and **GitHub Codespaces** to write, run, and store our work.

You will use the same GitHub repository throughout the semester.

By the end of the module, this repository will provide a record of your work and can form part of your cybersecurity portfolio.

---

## Objectives

By the end of this lab, you should be able to:

1. Create and secure a GitHub account.
2. Apply for GitHub Education student benefits.
3. Create a GitHub repository for this module.
4. Launch a GitHub Codespace.
5. Understand the difference between GitHub, Git, and Codespaces.
6. Create and run a simple Python program.
7. Save, commit, and push your work to GitHub.
8. Organise your work into folders for each lab.

---

# Part 1: GitHub, Git and Codespaces

Before getting started, it is useful to understand the three main technologies we will be using.

### GitHub

**GitHub** is an online platform used to store and share software projects.

Your work for this module will be stored in a GitHub repository.

### Git

**Git** is a version-control system.

It allows us to:

* track changes to files;
* create snapshots of our work;
* return to earlier versions;
* collaborate with other developers.

### GitHub Codespaces

**GitHub Codespaces** provides a development environment running in the cloud.

It gives us:

* a Linux environment;
* Visual Studio Code;
* a terminal;
* Python;
* Git;
* common development tools.

This means that we can use the same development environment from almost any computer with a web browser.

---

# Part 2: Create Your GitHub Account

If you already have a suitable GitHub account, you can skip this section.

1. Visit:

   https://github.com

2. Select **Sign up**.

3. Create an account.

4. Use an email address that you will continue to have access to.

5. Choose a professional username that you are comfortable using throughout your degree.

Avoid usernames that you would not be happy to show to:

* a lecturer;
* an employer;
* a placement supervisor;
* a recruiter.

6. Use a strong, unique password.

Using a password manager is recommended.

7. Verify your email address when GitHub sends you the verification message.

---

# Part 3: Secure Your Account

As cybersecurity students, account security is important.

Enable **two-factor authentication (2FA)** on your GitHub account.

Navigate to your GitHub account security settings and follow the instructions to enable 2FA.

Where possible, use:

* an authenticator application; or
* another secure authentication method.

Store any recovery codes somewhere safe.

> Never store passwords, authentication codes, API keys, tokens, or other secrets in a public GitHub repository.

---

# Part 4: GitHub Education

GitHub provides additional benefits to verified students through **GitHub Education**.

Visit:

https://education.github.com

Look for the option to apply for student benefits.

You may be asked to provide evidence that you are currently enrolled as a student.

This might include:

* your university email address;
* student identification;
* proof of enrolment;
* other documentation requested by GitHub.

Submit your application.

> Approval may not be immediate. You do not need to wait for approval before continuing with this lab.

GitHub Education is useful, but it is **not required to complete today's exercises**.

---

# Part 5: Create Your Module Repository

We will use **one repository for the entire module**.

Log into GitHub.

Create a new repository.

Use the repository name:

```text
scripting-for-cybersecurity
```

Select **Public**, remember:

> Anything committed to the repository may be visible to other people.

Never commit:

* passwords;
* API keys;
* access tokens;
* private keys;
* personal information;
* confidential information.

When creating the repository:

1. Name it:

```text
scripting-for-cybersecurity
```

2. Select **Add a README file**.

3. Create the repository.

You should now have a repository containing:

```text
scripting-for-cybersecurity/
└── README.md
```

---

# Part 6: Launch Your Codespace

Open your new repository on GitHub.

Select the green **Code** button.

Choose the **Codespaces** option.

Create a new Codespace.

After a short period, Visual Studio Code should open in your browser.

Your screen should contain:

* an Explorer panel on the left;
* an editor in the centre;
* a terminal at the bottom.

This is the development environment we will use throughout the module.

---

# Part 7: Explore the Codespace

Locate the **Explorer** panel.

You should see your repository and its files.

Your repository currently contains:

```text
README.md
```

Locate the terminal at the bottom of the screen.

If the terminal is not visible, you can normally open one from:

```text
Terminal → New Terminal
```

In the terminal, type:

```bash
pwd
```

Do not worry about what this command means yet.

You should see a path similar to:

```text
/workspaces/scripting-for-cybersecurity
```

Now type:

```bash
ls
```

You should see:

```text
README.md
```

We will learn what both commands mean in the next lab.

---

# Part 8: Create Your First Lab Folder

We will organise our work into folders.

In the Explorer panel, create a folder called:

```text
lab01
```

Your repository should now look similar to:

```text
scripting-for-cybersecurity/
├── README.md
└── lab01/
```

All work from today's lab should be placed inside `lab01`.

---

# Part 9: Your First Python Program

Inside the `lab01` folder, create a new file called:

```text
hello.py
```

Add the following code:

```python
print("Hello, world!")
```

Save the file.

Your repository should now contain:

```text
scripting-for-cybersecurity/
├── README.md
└── lab01/
    └── hello.py
```

---

# Part 10: Run Your Program

Use the terminal.

If necessary, move into the `lab01` directory:

```bash
cd lab01
```

Run your program:

```bash
python3 hello.py
```

You should see:

```text
Hello, world!
```

You have now created and executed your first Python program inside GitHub Codespaces.

---

# Part 11: Using `input()` and `print()`

Replace the contents of `hello.py` with:

```python
name = input("What is your name? ")

print("Hello, " + name + "!")
```

Run the program again:

```bash
python3 hello.py
```

Enter your name when prompted.

Example:

```text
What is your name? Mark
Hello, Mark!
```

Run the program several times using different values.

---

# Exercise 1: Personal Introduction

Modify your program so that it asks the user for:

* their name;
* their course;
* their favourite area of cybersecurity.

Example interaction:

```text
What is your name? Mark
What course are you studying? Cybersecurity
What area of cybersecurity interests you? Cryptography
```

The program should then display something similar to:

```text
Hello Mark
You are studying Cybersecurity
You are interested in Cryptography
```

---

# Exercise 2: Create Another Python File

Inside `lab01`, create:

```text
student.py
```

Write a program that asks the user for:

* their name;
* their student number;
* their year of study.

Display the information back to the user.

Example:

```text
Name: Alex Smith
Student Number: C00123456
Year: 2
```

---

# Part 12: Saving vs Version Control

There is an important difference between **saving a file** and **committing a file**.

## Saving

Saving updates the file inside your Codespace.

For example:

```text
Ctrl + S
```

saves changes to the current file.

## Committing

A **Git commit** records a snapshot of your work.

Think of it as creating a named checkpoint.

## Pushing

A **push** sends your Git commits from your Codespace to GitHub.

The process is therefore:

```text
Edit
  ↓
Save
  ↓
Stage
  ↓
Commit
  ↓
Push
```

---

# Part 13: Commit and Push Your Work

Open the **Source Control** panel in Visual Studio Code.

The icon normally resembles branching or connected lines.

You should see the files you changed.

Stage your changes.

Depending on the current interface, you can either stage individual files or stage all changes.

Enter a commit message such as:

```text
Complete Lab 1
```

Commit your changes.

Push or synchronise your changes with GitHub.

Now return to your GitHub repository in another browser tab.

Refresh the page.

You should see your `lab01` directory and files.

Your repository should look similar to:

```text
scripting-for-cybersecurity/
├── README.md
└── lab01/
    ├── hello.py
    └── student.py
```

---

# Exercise 3: Verify Your Repository

Check that:

* `lab01` exists;
* `hello.py` exists;
* `student.py` exists;
* your most recent commit appears on GitHub.

If your files only exist inside the Codespace but do not appear on GitHub, you probably have not pushed your latest commit.

---

# Part 14: Update Your README

Open:

```text
README.md
```

Add something similar to:

```markdown
# Scripting for Cybersecurity

This repository contains my practical work for the Scripting for Cybersecurity module.

## Labs

- Lab 01 - Development Environment
```

Save the file.

Commit and push the change.

---

# Part 15: Your Repository Structure

By the end of the semester, your repository may look similar to:

```text
scripting-for-cybersecurity/
├── README.md
├── lab01/
├── lab02/
├── lab03/
├── lab04/
├── lab05/
└── ...
```

Each week's work should be placed inside the appropriate folder.

---

# Deliverables

By the end of this lab you should have:

* a GitHub account;
* two-factor authentication enabled;
* a repository called `scripting-for-cybersecurity`;
* a working GitHub Codespace;
* a `lab01` directory;
* at least two Python files;
* your work committed and pushed to GitHub.

---

# Preparing for Lab 2

In the next lab we will work mainly inside the **Linux terminal** in your Codespace.

We will learn how to:

* navigate directories;
* create files and directories;
* understand Linux commands;
* use command-line help;
* work with shell variables;
* redirect output;
* combine commands using pipes.

Before finishing, open the terminal and run:

```bash
pwd
```

and:

```bash
ls
```

You do not need to understand these commands yet.

You will in the next lab.

---

# Further Work

If you finish early, explore:

* GitHub Markdown;
* your repository history;
* Visual Studio Code;
* GitHub Codespaces.

You can also try editing your `README.md` to include:

* a short description of the module;
* a list of completed labs;
* Markdown headings;
* code blocks;
* links.

---

# End of Lab 1
