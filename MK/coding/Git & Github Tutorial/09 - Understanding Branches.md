# Understanding Branches

## What is a Branch?

A **branch** is an independent line of development. Think of it as a parallel universe for your code where you can:

- Work on new features without affecting the main code
- Experiment safely
- Have multiple people work on different things simultaneously
- Keep your main code always working

## The Branch Analogy

Imagine a tree:

```
                    ┌── feature-login (branch)
                    │
    ────────────────┼──────────────── main (trunk)
                    │
                    └── bugfix-header (branch)
```

- **main** is the trunk - the primary, stable version
- **Branches** grow from the trunk for specific work
- When work is done, branches merge back into the trunk

## Why Use Branches?

### Without Branches (Bad)

```
Developer A: Working on login
Developer B: Working on checkout
Both editing the same files...

Result: Conflicts, broken code, chaos!
```

### With Branches (Good)

```
main: Always working, deployable code

feature-login: Developer A's work
feature-checkout: Developer B's work

Both work independently, merge when ready!
```

## How Branches Work

Branches are just pointers to commits:

```
                          feature
                             ↓
    ○ ── ○ ── ○ ── ○ ── ○ ── ○
              ↑
            main
              ↑
            HEAD
```

- Each `○` is a commit
- `main` points to a commit
- `feature` points to a newer commit
- `HEAD` shows where you are currently working

## Creating Branches

### Create a New Branch

```bash
git branch feature-name
```

This creates the branch but doesn't switch to it.

### Create and Switch in One Command

```bash
git checkout -b feature-name

# Or (newer syntax)
git switch -c feature-name
```

### List All Branches

```bash
# Local branches
git branch

# All branches (including remote)
git branch -a

# With last commit info
git branch -v
```

Output:
```
  feature-login
* main
  bugfix-header
```

The `*` indicates your current branch.

## Switching Branches

### Switch to an Existing Branch

```bash
git checkout branch-name

# Or (newer syntax)
git switch branch-name
```

### What Happens When You Switch

1. Git updates your working directory to match that branch's latest commit
2. HEAD moves to point to the new branch
3. Your files change to reflect that branch's state

```
Before (on main):           After (switch to feature):

    ○ ── ○ ── ○              ○ ── ○ ── ○
              ↑                        ↑
            main                     main
              ↑
            HEAD                       ○ ── ○
                                             ↑
                                          feature
                                             ↑
                                           HEAD
```

> [!warning] Commit or Stash First!
> You can't switch branches with uncommitted changes (unless they don't conflict). Either commit your work or stash it first.

## Branch Naming Conventions

Good branch names describe what they're for:

| Type | Pattern | Example |
|------|---------|---------|
| Feature | `feature/description` | `feature/user-authentication` |
| Bug fix | `bugfix/description` | `bugfix/login-error` |
| Hot fix | `hotfix/description` | `hotfix/security-patch` |
| Release | `release/version` | `release/v1.2.0` |
| Experiment | `experiment/description` | `experiment/new-ui` |

### Branch Naming Rules

- No spaces (use hyphens or underscores)
- Lowercase is conventional
- Be descriptive but concise
- Don't use special characters (except `/`, `-`, `_`)

## Working on a Branch

### Typical Workflow

```bash
# 1. Create and switch to new branch
git switch -c feature/add-search

# 2. Do your work - edit files, add features
echo "search code" > search.js

# 3. Stage and commit
git add search.js
git commit -m "Add search functionality"

# 4. Make more commits as needed
echo "more code" >> search.js
git add search.js
git commit -m "Improve search results"

# 5. When done, you'll merge back to main (next lesson!)
```

### See Which Branch You're On

```bash
# Method 1: git branch
git branch

# Method 2: git status
git status

# Method 3: git log (see the HEAD indicator)
git log --oneline -1
```

## Deleting Branches

### Delete a Merged Branch

```bash
git branch -d branch-name
```

### Force Delete (Unmerged Branch)

```bash
git branch -D branch-name
```

> [!tip] Clean Up Regularly
> Delete branches after they're merged to keep your repository tidy.

## Renaming Branches

### Rename Current Branch

```bash
git branch -m new-name
```

### Rename Any Branch

```bash
git branch -m old-name new-name
```

## Viewing Branch Differences

### See Commits in One Branch But Not Another

```bash
# Commits in feature that aren't in main
git log main..feature

# Commits in main that aren't in feature
git log feature..main
```

### Compare Files Between Branches

```bash
git diff main..feature

# Specific file
git diff main..feature -- filename.txt
```

## Visualizing Branches

### Text-based Graph

```bash
git log --oneline --graph --all
```

Output:
```
* a1b2c3d (HEAD -> feature) Add new feature
* b2c3d4e Continue feature work
| * c3d4e5f (main) Fix typo in readme
|/
* d4e5f6g Initial commit
```

### GUI Tools

- **gitk**: Built-in graphical viewer (`gitk --all`)
- **VS Code**: Git Graph extension
- **GitHub**: Network graph on repository page

## Practice Exercise

```bash
# Create a practice repo
mkdir branch-practice && cd branch-practice
git init

# Create initial content on main
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"

# Create and switch to a feature branch
git switch -c feature/greeting

# Add a new file on the feature branch
echo "console.log('Hello!');" > greeting.js
git add greeting.js
git commit -m "Add greeting feature"

# Check branches
git branch -v

# Switch back to main
git switch main

# Notice greeting.js is gone! (it only exists on feature branch)
ls

# Switch back to feature
git switch feature/greeting

# Now greeting.js is back!
ls

# View branch history
git log --oneline --graph --all
```

## Common Scenarios

### "I Started Work on Main by Accident!"

Move your work to a new branch:

```bash
# Create new branch (includes your changes)
git switch -c feature/my-work

# Your uncommitted changes are now on the new branch
git add .
git commit -m "Add my work"

# Main is clean again
git switch main
# Your changes are not here
```

### "I Need to Switch But Have Uncommitted Work!"

Use stash (temporary storage):

```bash
# Save current work temporarily
git stash

# Switch branches
git switch other-branch

# Do work, come back
git switch original-branch

# Restore your work
git stash pop
```

### "I Want to See a Branch Without Switching"

View files without switching:

```bash
# See a file on another branch
git show other-branch:filename.txt

# Compare file between branches
git diff main:file.txt feature:file.txt
```

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git branch` | List local branches |
| `git branch name` | Create a branch |
| `git switch name` | Switch to a branch |
| `git switch -c name` | Create and switch |
| `git branch -d name` | Delete merged branch |
| `git branch -D name` | Force delete branch |
| `git branch -m new` | Rename current branch |
| `git log --graph --all` | Visualize branches |

---

## Summary

- Branches are independent lines of development
- Create branches to work on features or fixes
- Each branch is a pointer to a commit
- Use `git switch -c name` to create and switch
- Delete branches after merging to stay organized
- Branches let teams work in parallel safely

---

**Next:** [[10 - Merging Branches]]

**Previous:** [[08 - Undoing Changes]]

**Back to:** [[00 - Welcome to Git & GitHub]]
