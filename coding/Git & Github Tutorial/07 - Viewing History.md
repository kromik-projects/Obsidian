# Viewing History

## Why View History?

Git's superpower is its complete record of every change. You can:

- See what changed and when
- Understand why changes were made
- Find when a bug was introduced
- See who made specific changes
- Go back to any point in time

## The git log Command

### Basic Log

```bash
git log
```

Output:
```
commit a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0 (HEAD -> main)
Author: Your Name <your.email@example.com>
Date:   Mon Jan 15 10:30:00 2024 -0500

    Add user authentication

commit b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0u1
Author: Your Name <your.email@example.com>
Date:   Sun Jan 14 15:20:00 2024 -0500

    Initial commit
```

Press `q` to exit the log view.

### Understanding the Output

Each commit shows:
- **Commit hash** - Unique identifier (SHA-1)
- **Author** - Who made the commit
- **Date** - When it was committed
- **Message** - Description of changes
- **HEAD -> main** - Current position indicator

## Formatting Log Output

### One Line Per Commit

```bash
git log --oneline
```

Output:
```
a1b2c3d Add user authentication
b2c3d4e Fix login bug
c3d4e5f Update README
d4e5f6g Initial commit
```

### Show Graph of Branches

```bash
git log --oneline --graph
```

Output:
```
* a1b2c3d (HEAD -> main) Merge feature branch
|\
| * e5f6g7h Add new feature
| * f6g7h8i Start feature work
|/
* b2c3d4e Fix login bug
* c3d4e5f Update README
```

### With More Details

```bash
git log --oneline --graph --all --decorate
```

- `--all` - Show all branches
- `--decorate` - Show branch/tag names

### Custom Format

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Output:
```
a1b2c3d - Alice, 2 hours ago : Add user authentication
b2c3d4e - Bob, 1 day ago : Fix login bug
```

**Format placeholders:**
| Code | Meaning |
|------|---------|
| `%H` | Full commit hash |
| `%h` | Short commit hash |
| `%an` | Author name |
| `%ae` | Author email |
| `%ar` | Relative date |
| `%ad` | Absolute date |
| `%s` | Subject (message) |

## Limiting Log Output

### Last N Commits

```bash
git log -5           # Last 5 commits
git log -1           # Only the last commit
```

### By Date

```bash
# Commits from the last week
git log --since="1 week ago"

# Commits before a date
git log --until="2024-01-01"

# Date range
git log --since="2024-01-01" --until="2024-01-31"
```

### By Author

```bash
git log --author="Alice"
git log --author="alice@example.com"
```

### By Message Content

```bash
# Find commits mentioning "bug"
git log --grep="bug"

# Case insensitive
git log --grep="bug" -i
```

### By File

```bash
# Commits that touched a specific file
git log -- filename.txt

# Commits that touched files in a directory
git log -- src/
```

## Viewing Specific Commits

### Show Commit Details

```bash
# Show a specific commit
git show a1b2c3d

# Show the last commit
git show HEAD

# Show second-to-last commit
git show HEAD~1
```

### What Does HEAD Mean?

**HEAD** is a pointer to your current position in the repository.

```
HEAD~1  = 1 commit before HEAD (parent)
HEAD~2  = 2 commits before HEAD (grandparent)
HEAD~3  = 3 commits before HEAD
```

```
a1b2c3d  ← HEAD (current commit)
   ↑
b2c3d4e  ← HEAD~1
   ↑
c3d4e5f  ← HEAD~2
   ↑
d4e5f6g  ← HEAD~3
```

## Viewing Changes

### See What Changed in a Commit

```bash
git show a1b2c3d
```

Shows the commit message AND the actual changes (diff).

### See Just the Files That Changed

```bash
git show --name-only a1b2c3d

# Or with status (added/modified/deleted)
git show --name-status a1b2c3d
```

Output:
```
A       newfile.txt       # Added
M       modified.txt      # Modified
D       deleted.txt       # Deleted
R       old.txt -> new.txt # Renamed
```

### Compare Two Commits

```bash
# Difference between two commits
git diff a1b2c3d..b2c3d4e

# What changed between HEAD and 3 commits ago
git diff HEAD~3..HEAD
```

## Viewing File History

### History of a Specific File

```bash
git log -- filename.txt

# With the actual changes
git log -p -- filename.txt
```

### Who Changed Each Line?

```bash
git blame filename.txt
```

Output:
```
a1b2c3d4 (Alice 2024-01-15 10:30:00) function hello() {
b2c3d4e5 (Bob   2024-01-14 15:20:00)     console.log("Hello");
a1b2c3d4 (Alice 2024-01-15 10:30:00) }
```

### Show Version of File at a Commit

```bash
# Show file as it was at a specific commit
git show a1b2c3d:filename.txt

# Show file as it was 5 commits ago
git show HEAD~5:filename.txt
```

## Searching History

### Find When a String Was Added/Removed

```bash
# Find commits that added or removed "TODO"
git log -S "TODO"

# Find commits that changed lines containing "function"
git log -G "function"
```

### Find Commits That Changed a Function

```bash
git log -L :functionName:filename.js
```

## Log Shortcuts with Aliases

Add these to your global config:

```bash
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
git config --global alias.last "log -1 HEAD"
```

Now use:
```bash
git lg      # Pretty graph log
git hist    # Formatted history
git last    # Last commit details
```

## Visual Log Tools

### Built-in GUI

```bash
gitk           # Git's built-in graphical viewer
gitk --all     # Show all branches
```

### In VS Code

- Install "Git Graph" extension
- Or use built-in Source Control panel

## Practice Exercise

```bash
# Go to your practice repo
cd ~/my-first-repo

# Make sure you have some commits
git log --oneline

# Try different log formats
git log                          # Full log
git log --oneline               # Compact
git log --oneline --graph       # With graph
git log -3                      # Last 3

# View specific commit
git show HEAD                   # Last commit
git show HEAD~1                 # Previous commit

# See what files changed
git log --name-status -3

# Find commits by you
git log --author="Your Name"

# Search messages
git log --grep="Add"

# If you have a file with history
git log -- README.md
git blame README.md
```

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git log` | Full commit history |
| `git log --oneline` | Compact one-line view |
| `git log --graph` | Show branch structure |
| `git log -n` | Last n commits |
| `git log --author="name"` | Filter by author |
| `git log --grep="text"` | Search commit messages |
| `git log -- file` | History of specific file |
| `git show commit` | Details of a commit |
| `git diff a..b` | Compare two commits |
| `git blame file` | Show who changed each line |
| `git log -p` | Show changes with log |

---

## Summary

- `git log` shows your project's commit history
- Use `--oneline` and `--graph` for cleaner views
- Filter by date, author, file, or message content
- `git show` displays details of specific commits
- `git blame` shows who last modified each line
- HEAD points to your current commit; HEAD~n is n commits back
- `git diff` compares different commits

---

**Next:** [[08 - Undoing Changes]]

**Previous:** [[06 - Staging and Committing]]

**Back to:** [[00 - Welcome to Git & GitHub]]
