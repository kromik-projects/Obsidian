# Staging and Committing

## Overview

Now that you understand the Git workflow, let's master the two most important commands:

- `git add` - Stage changes
- `git commit` - Save staged changes

## Staging Changes with git add

### Add a Single File

```bash
git add filename.txt
```

### Add Multiple Specific Files

```bash
git add file1.txt file2.txt file3.txt
```

### Add All Files in a Directory

```bash
git add directory/
```

### Add All Changed Files

```bash
# Add all changes (new, modified, deleted)
git add .

# Or equivalently
git add --all
git add -A
```

### Add All Files of a Certain Type

```bash
# Add all JavaScript files
git add *.js

# Add all files in src folder
git add src/
```

## Understanding What Gets Staged

### Check What's Staged

```bash
# See status
git status

# See exact changes that are staged
git diff --staged
# or
git diff --cached
```

### See Unstaged Changes

```bash
# See changes in working directory not yet staged
git diff
```

## Interactive Staging

### Add Parts of a File

If you made multiple changes to one file but only want to commit some:

```bash
git add -p filename.txt
# or
git add --patch filename.txt
```

Git will show each change and ask what to do:
- `y` - Stage this chunk
- `n` - Don't stage this chunk
- `s` - Split into smaller chunks
- `q` - Quit
- `?` - Show help

## Unstaging Changes

Made a mistake? Remove files from staging:

```bash
# Unstage a specific file
git restore --staged filename.txt

# Unstage all files
git restore --staged .

# Old syntax (still works)
git reset HEAD filename.txt
```

## Committing Changes

### Basic Commit

```bash
git commit -m "Your commit message here"
```

### Commit Without -m (Opens Editor)

```bash
git commit
```

This opens your configured text editor where you can write a longer message.

### Add and Commit in One Step

For already-tracked files that have been modified:

```bash
git commit -am "Your message"
# or
git commit -a -m "Your message"
```

> [!warning] -a Only Works for Tracked Files
> The `-a` flag only stages modified and deleted files. It does NOT add new untracked files!

## Writing Good Commit Messages

Commit messages are important! They explain **why** changes were made.

### Anatomy of a Good Message

```
Short summary (50 chars or less)

Longer description if needed. Wrap at 72 characters.
Explain what and why, not how (the code shows how).

- Bullet points are okay
- Keep it clear and concise
```

### Good Examples

```bash
git commit -m "Add user authentication feature"

git commit -m "Fix login bug when password contains spaces"

git commit -m "Update README with installation instructions"

git commit -m "Refactor database connection for better performance"
```

### Bad Examples

```bash
# Too vague
git commit -m "Fixed stuff"
git commit -m "Updates"
git commit -m "WIP"

# Describes what, not why
git commit -m "Changed line 42"

# Too long for summary line
git commit -m "Added new feature that allows users to reset their password by clicking a link in an email that gets sent to them"
```

### Commit Message Guidelines

| Do | Don't |
|-----|-------|
| Use present tense: "Add feature" | Past tense: "Added feature" |
| Be specific: "Fix login timeout" | Be vague: "Fix bug" |
| Keep summary under 50 chars | Write novels |
| Explain why if not obvious | Only describe what changed |
| Reference issues: "Fix #123" | Leave context out |

## Viewing Your Commits

### See Recent Commits

```bash
# Basic log
git log

# One line per commit
git log --oneline

# With graph showing branches
git log --oneline --graph

# Last 5 commits
git log -5
```

### See a Specific Commit

```bash
git show abc1234
# or
git show HEAD      # Last commit
git show HEAD~1    # Second to last commit
```

## Practical Workflow Example

Let's do a complete workflow:

```bash
# 1. Create some files
echo "# My Project" > README.md
echo "console.log('Hello');" > app.js
echo "body { margin: 0; }" > style.css

# 2. Check status
git status

# 3. Stage all files
git add .

# 4. Check what's staged
git status
git diff --staged

# 5. Commit
git commit -m "Initial project setup with README, JS, and CSS"

# 6. Verify
git status    # Should be clean
git log       # Should show your commit
```

## Amending Commits

Made a typo in your last commit message? Forgot to include a file?

### Fix the Last Commit Message

```bash
git commit --amend -m "New corrected message"
```

### Add Forgotten Files to Last Commit

```bash
# Stage the forgotten file
git add forgotten-file.txt

# Amend the last commit to include it
git commit --amend --no-edit
```

> [!warning] Only Amend Unpushed Commits
> Never amend commits that have been pushed to a shared repository! This rewrites history and causes problems for others.

## The .gitignore File

Some files should never be committed:

```bash
# Create .gitignore
cat > .gitignore << 'EOF'
# Dependencies
node_modules/
vendor/

# Environment files (contain secrets!)
.env
.env.local
*.pem

# Build outputs
dist/
build/
*.min.js

# IDE files
.idea/
.vscode/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Temporary files
tmp/
*.tmp
EOF
```

Then commit the .gitignore:
```bash
git add .gitignore
git commit -m "Add .gitignore file"
```

### .gitignore Patterns

| Pattern | What It Ignores |
|---------|-----------------|
| `file.txt` | Specific file |
| `*.log` | All .log files |
| `build/` | Directory and contents |
| `**/temp` | temp folder anywhere in project |
| `!important.log` | Exception - DON'T ignore this |
| `doc/*.txt` | .txt files in doc/ only |
| `doc/**/*.txt` | .txt files in doc/ and subdirs |

## Complete Practice Exercise

```bash
# 1. Go to your practice repository
cd ~/my-first-repo

# 2. Create a project structure
mkdir src
echo "function main() { console.log('Hello'); }" > src/app.js
echo "body { font-family: Arial; }" > src/style.css
echo "# My Project\n\nA sample project to learn Git." > README.md

# 3. Check status
git status

# 4. Stage everything
git add .

# 5. Check staged changes
git diff --staged

# 6. Commit
git commit -m "Add initial project structure"

# 7. Make changes
echo "// New feature" >> src/app.js
echo "h1 { color: blue; }" >> src/style.css

# 8. Check what changed
git status
git diff

# 9. Stage and commit
git add src/app.js src/style.css
git commit -m "Add styling and new feature placeholder"

# 10. View history
git log --oneline

# 11. Create .gitignore
echo "node_modules/\n.env\n*.log" > .gitignore
git add .gitignore
git commit -m "Add .gitignore"

# 12. View final history
git log --oneline
```

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git add file` | Stage a file |
| `git add .` | Stage all changes |
| `git add -p file` | Stage parts of a file interactively |
| `git restore --staged file` | Unstage a file |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git commit -m "msg"` | Commit with message |
| `git commit -am "msg"` | Stage modified files and commit |
| `git commit --amend` | Modify the last commit |
| `git log` | View commit history |
| `git log --oneline` | Compact history view |

---

## Summary

- `git add` stages changes for the next commit
- Use `git add .` to stage everything or be selective
- `git commit -m "message"` saves staged changes
- Write clear, meaningful commit messages
- Use `.gitignore` to exclude files from tracking
- `git commit --amend` fixes the last commit (before pushing)
- Check your work with `git status`, `git diff`, and `git log`

---

**Next:** [[07 - Viewing History]]

**Previous:** [[05 - The Git Workflow]]

**Back to:** [[00 - Welcome to Git & GitHub]]
