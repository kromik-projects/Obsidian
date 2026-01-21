# Git Commands Cheatsheet

A quick reference for all essential Git commands.

---

## Setup & Configuration

```bash
# Set username
git config --global user.name "Your Name"

# Set email
git config --global user.email "your@email.com"

# Set default editor
git config --global core.editor "code --wait"

# Set default branch name
git config --global init.defaultBranch main

# View all settings
git config --list

# View specific setting
git config user.name
```

---

## Creating Repositories

```bash
# Initialize new repository
git init

# Initialize with specific branch name
git init -b main

# Clone existing repository
git clone <url>

# Clone to specific folder
git clone <url> <folder>

# Clone specific branch
git clone -b <branch> <url>

# Shallow clone (latest commit only)
git clone --depth 1 <url>
```

---

## Basic Workflow

```bash
# Check status
git status

# Short status
git status -s

# Stage file
git add <file>

# Stage all changes
git add .

# Stage interactively
git add -p

# Commit with message
git commit -m "message"

# Commit (opens editor)
git commit

# Stage tracked files and commit
git commit -am "message"

# Amend last commit
git commit --amend
```

---

## Viewing Changes

```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Show changes in commit
git show <commit>

# Show file at specific commit
git show <commit>:<file>
```

---

## History

```bash
# View commit history
git log

# One line per commit
git log --oneline

# With graph
git log --oneline --graph

# All branches
git log --oneline --graph --all

# Last N commits
git log -n <number>

# By author
git log --author="name"

# By date
git log --since="2024-01-01"
git log --until="2024-12-31"

# Search messages
git log --grep="keyword"

# File history
git log -- <file>

# Who changed each line
git blame <file>
```

---

## Branching

```bash
# List branches
git branch

# List all branches (including remote)
git branch -a

# List with details
git branch -v

# Create branch
git branch <name>

# Switch branch
git switch <branch>
git checkout <branch>  # older syntax

# Create and switch
git switch -c <branch>
git checkout -b <branch>  # older syntax

# Rename branch
git branch -m <old> <new>

# Delete branch (merged)
git branch -d <branch>

# Delete branch (force)
git branch -D <branch>

# Set upstream
git branch --set-upstream-to=origin/<branch>
```

---

## Merging

```bash
# Merge branch into current
git merge <branch>

# Merge without fast-forward
git merge --no-ff <branch>

# Merge with squash
git merge --squash <branch>

# Abort merge
git merge --abort
```

---

## Remote Repositories

```bash
# List remotes
git remote

# List with URLs
git remote -v

# Add remote
git remote add <name> <url>

# Remove remote
git remote remove <name>

# Rename remote
git remote rename <old> <new>

# Change URL
git remote set-url <name> <url>

# Show remote details
git remote show <name>
```

---

## Syncing

```bash
# Fetch changes
git fetch

# Fetch specific remote
git fetch <remote>

# Fetch and prune deleted branches
git fetch --prune

# Pull (fetch + merge)
git pull

# Pull with rebase
git pull --rebase

# Push
git push

# Push and set upstream
git push -u origin <branch>

# Push all branches
git push --all

# Push tags
git push --tags

# Force push (dangerous!)
git push --force

# Safer force push
git push --force-with-lease
```

---

## Undoing Changes

```bash
# Discard working directory changes
git restore <file>
git checkout -- <file>  # older syntax

# Unstage file
git restore --staged <file>
git reset HEAD <file>  # older syntax

# Undo last commit (keep changes staged)
git reset --soft HEAD~1

# Undo last commit (keep changes unstaged)
git reset HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a commit (safe for pushed)
git revert <commit>

# View reflog (recovery)
git reflog
```

---

## Stashing

```bash
# Stash changes
git stash

# Stash with message
git stash push -m "message"

# List stashes
git stash list

# Apply most recent stash
git stash pop

# Apply specific stash
git stash pop stash@{n}

# Apply without removing
git stash apply

# Drop stash
git stash drop stash@{n}

# Clear all stashes
git stash clear
```

---

## Tags

```bash
# List tags
git tag

# Create lightweight tag
git tag <name>

# Create annotated tag
git tag -a <name> -m "message"

# Tag specific commit
git tag <name> <commit>

# Push tag
git push origin <tag>

# Push all tags
git push --tags

# Delete local tag
git tag -d <name>

# Delete remote tag
git push origin --delete <tag>
```

---

## Cleaning

```bash
# Show what would be removed
git clean -n

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Remove ignored files too
git clean -fdx
```

---

## Inspection

```bash
# Show commit
git show <commit>

# Show file from commit
git show <commit>:<file>

# Compare branches
git diff <branch1>..<branch2>

# List files in commit
git show --name-only <commit>

# Show file status in commit
git show --name-status <commit>
```

---

## Advanced

```bash
# Interactive rebase
git rebase -i HEAD~n

# Cherry-pick commit
git cherry-pick <commit>

# Bisect (find bad commit)
git bisect start
git bisect bad
git bisect good <commit>

# Create patch
git format-patch -1 <commit>

# Apply patch
git apply <patch-file>

# Archive repository
git archive --format=zip HEAD > archive.zip
```

---

## GitHub CLI (gh)

```bash
# Login
gh auth login

# Create repo
gh repo create <name>

# Clone repo
gh repo clone <owner>/<repo>

# Create issue
gh issue create

# List issues
gh issue list

# Create PR
gh pr create

# List PRs
gh pr list

# Check out PR
gh pr checkout <number>

# View PR
gh pr view <number>
```

---

## Aliases (Shortcuts)

Add to your config:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.last "log -1 HEAD"
git config --global alias.unstage "restore --staged"
```

Then use:
```bash
git st      # status
git co main # checkout main
git br      # branch
git lg      # pretty log
```

---

## Quick Reference Tables

### Daily Commands

| Command | What It Does |
|---------|--------------|
| `git status` | See current state |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Save changes |
| `git push` | Upload to remote |
| `git pull` | Download from remote |
| `git log --oneline` | View history |

### Branch Commands

| Command | What It Does |
|---------|--------------|
| `git branch` | List branches |
| `git switch -c name` | Create & switch |
| `git switch name` | Switch branch |
| `git merge name` | Merge branch |
| `git branch -d name` | Delete branch |

### Undo Commands

| I Want To... | Command |
|--------------|---------|
| Discard changes | `git restore file` |
| Unstage file | `git restore --staged file` |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` |
| Undo last commit (discard) | `git reset --hard HEAD~1` |
| Undo pushed commit | `git revert commit` |

---

**Next:** [[24 - Common Problems and Solutions]]

**Previous:** [[22 - Collaborative Workflows]]

**Back to:** [[00 - Welcome to Git & GitHub]]
