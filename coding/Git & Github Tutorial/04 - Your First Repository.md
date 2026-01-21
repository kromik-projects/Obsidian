# Your First Repository

## What is a Repository?

A **repository** (or **repo**) is a folder that Git is tracking. It contains:

- Your project files
- A hidden `.git` folder with all the version history
- Configuration for that specific project

Think of it as a regular folder with superpowers—Git remembers every change ever made to files inside it.

## Two Ways to Get a Repository

1. **Initialize a new one** - Turn an existing folder into a Git repository
2. **Clone an existing one** - Download a repository from somewhere else (covered in [[17 - Cloning Repositories]])

## Creating Your First Repository

Let's create a new repository from scratch.

### Step 1: Create a Project Folder

Open your terminal and run:

```bash
# Go to your home directory
cd ~

# Create a new folder for your project
mkdir my-first-repo

# Go into the folder
cd my-first-repo

# Verify you're in the right place
pwd
```

### Step 2: Initialize Git

Turn this folder into a Git repository:

```bash
git init
```

You should see:
```
Initialized empty Git repository in /home/yourname/my-first-repo/.git/
```

That's it! Your folder is now a Git repository.

### Step 3: Explore What Happened

```bash
# List all files including hidden ones
ls -la
```

You'll see:
```
drwxr-xr-x   3 yourname  staff   96 Jan 15 10:00 .
drwxr-xr-x  15 yourname  staff  480 Jan 15 10:00 ..
drwxr-xr-x   9 yourname  staff  288 Jan 15 10:00 .git
```

The `.git` folder is where Git stores everything—all your history, configuration, and tracking data.

> [!warning] Never Delete .git
> If you delete the `.git` folder, you lose all version history! The repository becomes a regular folder again.

## Understanding the .git Folder

You don't need to memorize this, but here's what's inside `.git`:

```
.git/
├── HEAD          # Points to current branch
├── config        # Repository-specific settings
├── description   # Used by GitWeb (usually ignored)
├── hooks/        # Scripts that run on events
├── info/         # Additional info
├── objects/      # All your content (commits, files, etc.)
└── refs/         # Pointers to commits (branches, tags)
```

> [!tip] You'll Never Edit These Directly
> Git manages the `.git` folder automatically. You interact with it through Git commands.

## Checking Repository Status

The most useful command you'll ever learn:

```bash
git status
```

In a fresh repository, you'll see:

```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

This tells you:
- You're on the `main` branch
- No commits have been made yet
- There's nothing to save

## Adding Your First Files

Let's create some files and see how Git responds.

### Create a README File

```bash
# Create a README file
echo "# My First Repository" > README.md

# Check what Git sees
git status
```

Now Git shows:

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

The file is **untracked**—Git sees it but isn't saving its history yet.

### Create More Files

```bash
# Create a simple HTML file
echo "<!DOCTYPE html><html><body><h1>Hello World</h1></body></html>" > index.html

# Create a text file
echo "This is my first Git project!" > notes.txt

# Check status again
git status
```

Output:
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        index.html
        notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```

All three files are untracked. In the next lesson, we'll learn how to track them!

## Repository Best Practices

### Always Have a README

A `README.md` file is the first thing people see when they visit your repository. Include:
- Project name and description
- How to install/use it
- Important information

### Use a .gitignore File

Some files shouldn't be tracked:
- System files (`.DS_Store`, `Thumbs.db`)
- Dependencies (`node_modules/`)
- Secrets (`.env` files with passwords)
- Build outputs (`dist/`, `build/`)

Create a `.gitignore` file:

```bash
echo "# Ignore system files
.DS_Store
Thumbs.db

# Ignore environment files
.env
.env.local

# Ignore dependencies
node_modules/
" > .gitignore
```

We'll cover `.gitignore` in detail later!

## Common Git Init Scenarios

### Initialize in an Existing Project

If you already have a project folder with files:

```bash
cd existing-project
git init
git status    # See all existing files as untracked
```

### Initialize with a Different Branch Name

```bash
git init --initial-branch=main
# or
git init -b main
```

### Check If a Folder is a Repository

```bash
# If you see .git folder, it's a repo
ls -la | grep .git

# Or check git status
git status
```

If it's not a repo, you'll see:
```
fatal: not a git repository (or any of the parent directories): .git
```

## Practice Exercise

Let's reinforce what you've learned:

1. **Create a new practice repository:**
   ```bash
   cd ~
   mkdir practice-repo
   cd practice-repo
   git init
   ```

2. **Check the status:**
   ```bash
   git status
   ```

3. **Create some files:**
   ```bash
   echo "# Practice Repository" > README.md
   echo "Learning Git is fun!" > notes.txt
   echo "console.log('Hello');" > script.js
   ```

4. **Check status again:**
   ```bash
   git status
   ```

5. **Look at the .git folder:**
   ```bash
   ls -la
   ls .git
   ```

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git init` | Initialize a new repository |
| `git status` | Show current state of repository |
| `ls -la` | List all files including hidden |
| `pwd` | Print current directory |

## What You Learned

- A **repository** is a folder tracked by Git
- `git init` creates a new repository
- The `.git` folder contains all Git data
- `git status` shows the current state
- **Untracked files** are files Git sees but isn't tracking yet

---

**Next:** [[05 - The Git Workflow]]

**Previous:** [[03 - Configuring Git]]

**Back to:** [[00 - Welcome to Git & GitHub]]
