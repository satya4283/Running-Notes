# DevOps Notes: Git, GitHub & Shell Scripting

## 1. Problems in Manual Deployment

Manual deployment has several challenges:

1. **Documentation Dependency:** Documentation is the primary source of deployment instructions.
2. **Time-Consuming Process:** Executing commands manually takes more time.
3. **Human Errors:** Incorrect commands or missed steps can cause failures.
4. **Difficult Rollback:** Restoring the previous working version is difficult when something goes wrong.
5. **Poor Change Identification:** Identifying who made a change and what was changed is difficult.

### Solution: Scripting

**Scripting** means storing a sequence of commands in a single file and executing that file to automate a process.

We use scripting to automate deployment and reduce the problems associated with manual execution.

---

## 2. Where Should We Store Deployment Scripts?

### Option 1: Store Scripts on a Laptop

Storing scripts only on a local laptop has the following disadvantages:

1. **Security Risks:** Unauthorized access or accidental exposure.
2. **No Reliable Backup:** Scripts may be lost if the laptop fails.
3. **No Version Control:** Difficult to manage versions such as `1.0.0`, `1.1.0`, and `2.0.0`.
4. **No Collaboration:** Difficult for multiple team members to work together.
5. **No Review Mechanism:** Changes may be used without approval.
6. **No Change Tracking:** Difficult to identify who changed what and when.

### Solution: Version Control System (VCS)

We need a reliable **Version Control System (VCS)**, also known as **Source Code Management (SCM)**, to manage scripts and programs.

---

## 3. What Is a Repository?

A **repository (repo)** is a place where files, source code, and their version history are stored and managed.

### Types of Storage

| Tool / Repository | Purpose |
|---|---|
| Git repository | Tracks source code and its changes |
| Google Drive | Stores and shares files |
| Artifact repository | Stores build artifacts, packages, and binaries |
| GitHub repository | Hosts Git repositories remotely |

### Important Terms

- **Git:** A distributed version control system.
- **GitHub:** An online platform for hosting Git repositories and collaborating on code.
- **Local Repository:** A Git repository on your laptop.
- **Remote Repository:** A Git repository hosted on a platform such as GitHub.

---

## 4. Create a Repository in GitHub

### Step 1: Create a Remote Repository

1. Open [GitHub](https://github.com/).
2. Sign in to your account.
3. Click **New repository**.
4. Enter a repository name, for example, `my_first_repo`.
5. Select the required visibility: Public or Private.
6. Click **Create repository**.

### Step 2: Clone the Repository

Cloning creates a local copy of a remote repository, including its Git history.

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/USERNAME/my_first_repo.git
```

### Step 3: Open the Repository in VS Code

1. Open VS Code.
2. Select **File → Open Folder**.
3. Choose the cloned repository folder.
4. Create and edit your scripts inside that folder.

---

## 5. What Is an IDE?

**IDE stands for Integrated Development Environment.**

An IDE provides tools that make software development easier, such as:

- Code editor
- Syntax highlighting
- Debugging tools
- Extensions
- Terminal integration

**Example:** VS Code is a popular code editor that can be extended into a powerful development environment.

---

## 6. Shell Scripting vs. Python

Shell scripting and Python can both automate tasks, but they are commonly used for different purposes.

| Shell Scripting | Python |
|---|---|
| Commonly used for Linux system administration | Used for general-purpose programming and automation |
| Works naturally with Linux commands and utilities | Provides extensive libraries and programming capabilities |
| Suitable for file operations, service management, and deployment commands | Suitable for APIs, data processing, cloud automation, and complex workflows |
| Example: Restarting a service | Example: Processing API responses |

**Rule of thumb:** For command-oriented tasks directly on a Linux server, shell scripting is often convenient. For complex automation, APIs, and data processing, Python is often a better choice.

Note: Python is not limited to external systems; it can also automate tasks directly on Linux servers.

---

## 7. What Is a Shebang?

A **shebang** tells Linux which interpreter should execute a script.

Example:

```bash
#!/bin/bash
```

It is normally placed on the first line of a Bash script.

### Example: Hello World

File: `01-hello-world.sh`

```bash
#!/bin/bash

echo "Hello World"
```

### Execute the Script

```bash
bash 01-hello-world.sh
```

Or, if the file has execute permission:

```bash
chmod +x 01-hello-world.sh
./01-hello-world.sh
```

**Important clarification:** The shebang is needed when executing a script directly as `./script.sh`. When you explicitly run `bash script.sh`, Bash is already specified, so the shebang is not required for interpreter selection.

**Bash is a shell.** A Bash script is a script written for Bash; not every shell script is necessarily a Bash script.

---

## 8. How to Store a Script in GitHub

Suppose you developed a shell script on your laptop and want to upload it to GitHub.

The basic Git workflow has three stages:

<escape>
Working Directory → Staging Area → Local Repository → Remote Repository
</escape>

### Step 1: Add the File to the Staging Area

```bash
git add 01-hello-world.sh
```

This stages the file so it can be included in the next commit.

To stage all changes in the current directory:

```bash
git add .
```

### Step 2: Commit the Changes

```bash
git commit -m "Add my first shell script"
```

A **commit** saves a snapshot of staged changes in your local Git repository.

### Step 3: Push to GitHub

```bash
git push origin main
```

This uploads your local commits to the remote repository's `main` branch.

### Summary of Git Commands

| Command | Purpose |
|---|---|
| `git status` | Shows the current state of files |
| `git add` | Stages changes |
| `git commit` | Saves staged changes locally |
| `git push` | Uploads commits to a remote repository |
| `git pull` | Fetches and integrates remote changes |
| `git log` | Displays commit history |
| `git clone` | Copies a remote repository locally |

---

## 9. Configure Git for the First Time

When you make your first commit, Git may display this error:

```text
Author identity unknown

*** Please tell me who you are.

fatal: unable to auto-detect email address
```

### Solution

Configure your name and email address:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Replace the example values with your preferred commit name and email.

Verify the configuration:

```bash
git config --global --list
```

**Important:** These settings identify the author recorded in Git commits. They do not authenticate you to GitHub.

---

## 10. GitHub Authentication

When pushing code to GitHub, authentication may be required.

You may be prompted to sign in through your browser.

### Common Authentication Methods

- Browser-based sign-in through Git Credential Manager.
- Personal access tokens when appropriate.
- SSH keys configured for GitHub.

For beginners, browser-based authentication is often the simplest option when Git Credential Manager is configured.

**Important:** Git commit identity and GitHub authentication are two different things.

---

## 11. Folder vs. Git Repository

A normal folder becomes a Git repository when Git initializes it.

| Normal Folder | Git Repository |
|---|---|
| Contains files and folders | Contains files and a `.git` directory |
| Does not track file history through Git | Tracks commits, branches, and file history |
| Cannot use Git version history until initialized | Supports Git version-control commands |

To check whether a folder is a Git repository:

```bash
git status
```

If Git reports that the directory is not a repository, it may be a normal folder or you may be in the wrong directory.

The `.git` directory stores Git's repository metadata and history.

---

## 12. Working with an Existing Repository

Suppose an important file needs changes.

A typical team workflow is:

1. Obtain the current source code from the repository.
2. Create a branch or a separate working copy.
3. Make the required changes.
4. Test the changes.
5. Share them with the Team Lead (TL).
6. Get the changes reviewed and approved.
7. Merge the changes into the main branch.

This workflow helps prevent unreviewed changes from affecting the main codebase.

---

## 13. Push an Existing Local Project to GitHub

If you already have a project on your laptop and want to connect it to a new GitHub repository, follow these steps.

### Step 1: Initialize Git

Run these commands inside your project folder:

```bash
git init
```

### Step 2: Set the Main Branch

```bash
git branch -M main
```

### Step 3: Stage the Files

```bash
git add .
```

### Step 4: Commit the Files

```bash
git commit -m "Initial commit"
```

### Step 5: Add the Remote Repository

```bash
git remote add origin <repository-url>
```

### Step 6: Push to GitHub

```bash
git push -u origin main
```

Replace `<repository-url>` with the URL of your GitHub repository.

**Note:** Create the remote repository first. If the remote repository already contains commits, such as a README, you may need to pull or reconcile the histories before pushing.

---

## 14. How to Execute a Shell Script on Linux

There are several ways to execute a shell script.

### Method 1: Execute Using Bash

```bash
bash script.sh
```

### Method 2: Execute Using Sh

```bash
sh script.sh
```

Use `sh` only when the script is compatible with the shell used by your system's `sh` command. Bash-specific scripts should generally be run using `bash`.

### Method 3: Execute Directly

```bash
chmod +x script.sh
./script.sh
```

---

## 15. Shell Script Example: Conversation

File: `conversation.sh`

```bash
#!/bin/bash

echo "Ramesh: Hi, Suresh. How are you?"
echo "Suresh: Hello, Ramesh. I am good. How about you?"
echo "Ramesh: I am good too, Suresh. Thanks for asking."
```

Execute it:

```bash
bash conversation.sh
```

Output:

```text
Ramesh: Hi, Suresh. How are you?
Suresh: Hello, Ramesh. I am good. How about you?
Ramesh: I am good too, Suresh. Thanks for asking.
```

The `echo` command prints text to the terminal.

---

## 16. DRY Principle

**DRY stands for Don't Repeat Yourself.**

The principle encourages us to avoid repeating the same logic or values unnecessarily.

### Example

Without a variable:

```bash
echo "Hello John"
echo "Welcome John"
echo "Have a nice day, John"
```

With a variable:

```bash
#!/bin/bash

NAME="John"

echo "Hello $NAME"
echo "Welcome $NAME"
echo "Have a nice day, $NAME"
```

If the name changes, we only need to update the variable once.

---

## 17. Variables in Shell Scripting

A **variable** stores a value under a name so that the value can be reused.

### Example

```bash
#!/bin/bash

X=0
Y=1

echo "X = $X"
echo "Y = $Y"
```

### Benefits of Variables

1. Store and reuse values.
2. Make changes easier by updating values in one place.
3. Improve readability and reduce duplication.
4. Reduce accidental inconsistencies.

### Important Rules

```bash
NAME="John"       # Correct
AGE=28            # Correct
```

Do not put spaces around `=` during assignment.

```bash
NAME = "John"     # Incorrect
```

To use a variable's value, prefix its name with `$`:

```bash
echo "$NAME"
```

---

## 18. Common Programming and Scripting Concepts

Most programming and scripting languages provide concepts such as:

1. **Variables** – Store values.
2. **Data Types** – Represent different kinds of values.
3. **Conditions** – Make decisions using `if`, `else`, and similar constructs.
4. **Functions** – Group reusable logic.
5. **Loops** – Repeat a sequence of operations.
6. **Error Handling** – Detect and handle failures.

These concepts help us develop reusable, maintainable scripts.

---

## 19. Command-Line Arguments

We can pass values to a shell script when executing it.

Example:

```bash
bash 04-variables.sh John Raheem
```

Inside the script:

- `$1` represents the first argument: `John`.
- `$2` represents the second argument: `Raheem`.
- `$0` represents the script name.
- `$#` represents the number of arguments.
- `$@` represents all positional arguments.

### Example Script

File: `04-variables.sh`

```bash
#!/bin/bash

FIRST_NAME="$1"
LAST_NAME="$2"

echo "First Name: $FIRST_NAME"
echo "Last Name: $LAST_NAME"
```

Execute:

```bash
bash 04-variables.sh John Raheem
```

Output:

```text
First Name: John
Last Name: Raheem
```

These values are commonly called **command-line arguments** or **positional parameters**. They are supplied by the caller rather than declared as parameters in a function definition.

---

## 20. Capture Command Output in a Variable

To execute a command and store its output in a variable, use **command substitution**.

Syntax:

```bash
VARIABLE=$(command)
```

### Example: Capture the Current Time

```bash
CURRENT_TIME=$(date +%H:%M:%S)

echo "Current time: $CURRENT_TIME"
```

### Example: Capture the Current Date

```bash
CURRENT_DATE=$(date +%Y-%m-%d)

echo "Current date: $CURRENT_DATE"
```

### Example: Capture a Unix Timestamp

```bash
START_TIME=$(date +%s)

echo "Start timestamp: $START_TIME"
```

The `date +%s` command returns the number of seconds since the Unix epoch.

---

## 21. Calculate Script Execution Time

We can record the start and end timestamps to calculate how long a script takes to execute.

File: `06-script.sh`

```bash
#!/bin/bash

START_TIME=$(date +%s)

echo "Script started at: $(date +%H:%M:%S)"

# Your commands go here
sleep 2

END_TIME=$(date +%s)

echo "Script completed at: $(date +%H:%M:%S)"

TOTAL_TIME=$((END_TIME - START_TIME))

echo "Total execution time: $TOTAL_TIME seconds"
```

Execute:

```bash
bash 06-script.sh
```

Example output:

```text
Script started at: 08:34:00
Script completed at: 08:34:02
Total execution time: 2 seconds
```

The displayed times are examples. Actual values depend on when the script runs.

**How it works:**

1. `START_TIME` stores the starting Unix timestamp.
2. The script executes its commands.
3. `END_TIME` stores the ending Unix timestamp.
4. `$((END_TIME - START_TIME))` calculates the elapsed time in seconds.

---

## 22. Quick Revision: Git and Shell Scripting

| Concept | Key Point |
|---|---|
| Repository | Stores files and, in Git, their version history |
| Git | Distributed version control system |
| GitHub | Hosts remote Git repositories |
| IDE | Provides tools to develop and debug code |
| Shell script | A file containing shell commands |
| Shebang | Specifies the interpreter for direct script execution |
| `echo` | Prints text |
| Variable | Stores a reusable value |
| `git add` | Stages changes |
| `git commit` | Saves a local snapshot |
| `git push` | Uploads commits to a remote repository |
| `$1`, `$2` | Access positional arguments |
| `$(command)` | Captures command output |
| `date +%s` | Returns a Unix timestamp |
| DRY | Don't Repeat Yourself |

### Final Learning Flow

**Manual Deployment → Shell Scripting → Git → GitHub → Version Control → Automated Deployment**

The objective is to automate repetitive deployment tasks and manage the scripts securely, collaboratively, and with a complete history of changes.