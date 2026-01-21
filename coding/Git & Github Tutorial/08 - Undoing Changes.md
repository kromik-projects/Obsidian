# Undoing Changes

## Don't Panic!

Everyone makes mistakes. Git provides many ways to undo changes safely. The key is knowing which command to use depending on what you want to undo.

## Understanding What to Undo

Ask yourself: **Where is the change I want to undo?**

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   Working           Staging           Repository                    │
│   Directory  ───►   Area      ───►    (Commits)                    │
│                                                                     │
│   [Changes         [Changes           [Saved                       │
│    you made]        staged]            commits]                    │
│                                                                     │
│   Undo with:       Undo with:         Undo with:                   │
│   git restore      git restore        git revert                   │
│                    --staged           git reset                    │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

## Scenario 1: Undo Changes in Working Directory

You modified a file but want to discard those changes and go back to how it was in the last commit.

### Discard Changes to a Specific File

```bash
git restore filename.txt
```

### Discard Changes to All Files

```bash
git restore .
```

> [!warning] Cannot Be Undone!
> This permanently discards your uncommitted changes. Make sure you really want to lose them!

### Old Syntax (Still Works)

```bash
git checkout -- filename.txt
git checkout -- .
```

## Scenario 2: Unstage Changes

You staged a file with `git add` but want to remove it from staging (keep the changes, just don't commit them yet).

### Unstage a Specific File

```bash
git restore --staged filename.txt
```

### Unstage All Files

```bash
git restore --staged .
```

### Old Syntax (Still Works)

```bash
git reset HEAD filename.txt
git reset HEAD .
```

## Scenario 3: Undo the Last Commit

### Keep Changes, Just Undo the Commit

```bash
git reset --soft HEAD~1
```

- Commit is undone
- Changes move back to staging area
- Your files are unchanged

### Undo Commit and Unstage Changes

```bash
git reset HEAD~1
# or
git reset --mixed HEAD~1
```

- Commit is undone
- Changes move to working directory (unstaged)
- Your files are unchanged

### Completely Undo Commit and Discard Changes

```bash
git reset --hard HEAD~1
```

> [!danger] Destructive!
> `--hard` permanently deletes uncommitted changes and the commit. Use with caution!

### Visual Summary of Reset Types

```
Before: A -- B -- C (HEAD)

git reset --soft HEAD~1
Result: A -- B (HEAD)
        Staging: Changes from C
        Working: Unchanged

git reset --mixed HEAD~1
Result: A -- B (HEAD)
        Staging: Empty
        Working: Changes from C (unstaged)

git reset --hard HEAD~1
Result: A -- B (HEAD)
        Staging: Empty
        Working: Clean (C's changes are GONE)
```

## Scenario 4: Fix the Last Commit

### Change the Commit Message

```bash
git commit --amend -m "New corrected message"
```

### Add Forgotten Files

```bash
git add forgotten-file.txt
git commit --amend --no-edit
```

### Remove a File from Last Commit

```bash
git reset --soft HEAD~1
git restore --staged file-to-remove.txt
git commit -m "Same message without the file"
```

> [!warning] Only Amend Unpushed Commits
> Never amend commits that have been pushed to a shared repository!

## Scenario 5: Undo a Commit That's Been Pushed

When a commit is already pushed, you can't just delete it. Use `git revert` instead:

### Create a New Commit That Undoes Changes

```bash
git revert a1b2c3d
```

This creates a new commit that is the exact opposite of the specified commit.

```
Before: A -- B -- C (HEAD)

git revert C

After:  A -- B -- C -- C' (HEAD)
                       ↑
                    Undoes C's changes
```

### Revert Without Immediately Committing

```bash
git revert --no-commit a1b2c3d
```

Changes are staged but not committed. Useful for reviewing or making additional changes first.

### Revert Multiple Commits

```bash
# Revert a range (oldest..newest)
git revert --no-commit HEAD~3..HEAD
git commit -m "Revert last 3 commits"
```

## Scenario 6: Recover Deleted/Lost Commits

Git rarely truly deletes anything. The reflog tracks all HEAD movements.

### View the Reflog

```bash
git reflog
```

Output:
```
a1b2c3d HEAD@{0}: reset: moving to HEAD~1
b2c3d4e HEAD@{1}: commit: Add feature
c3d4e5f HEAD@{2}: commit: Fix bug
```

### Recover a "Lost" Commit

```bash
# Find the commit hash in reflog
git reflog

# Restore to that point
git reset --hard b2c3d4e
```

### Recover a Deleted Branch

```bash
# Find where the branch was
git reflog

# Recreate the branch
git branch recovered-branch a1b2c3d
```

## Scenario 7: Discard All Local Changes

### Reset to Last Commit (Keep Untracked Files)

```bash
git reset --hard HEAD
```

### Reset and Remove Untracked Files

```bash
# See what would be deleted
git clean -nd

# Delete untracked files
git clean -fd
```

### Nuclear Option: Reset to Remote

```bash
git fetch origin
git reset --hard origin/main
```

> [!danger] Very Destructive
> This loses ALL local changes and commits not on the remote!

## Scenario 8: Temporarily Save Changes

Not exactly "undoing," but useful when you need to switch tasks:

### Stash Your Changes

```bash
# Save current changes
git stash

# Your working directory is now clean

# Later, restore the changes
git stash pop
```

We'll cover stashing in detail later!

## Decision Guide

| I Want To... | Command |
|--------------|---------|
| Discard uncommitted changes in a file | `git restore file` |
| Unstage a file | `git restore --staged file` |
| Undo last commit, keep changes staged | `git reset --soft HEAD~1` |
| Undo last commit, keep changes unstaged | `git reset HEAD~1` |
| Undo last commit completely | `git reset --hard HEAD~1` |
| Fix last commit message | `git commit --amend -m "new msg"` |
| Add file to last commit | `git add file && git commit --amend` |
| Undo a pushed commit | `git revert commit-hash` |
| Recover lost commit | `git reflog` then `git reset` |

## Practice Exercise

```bash
# Create test repo
mkdir undo-practice && cd undo-practice
git init

# Create and commit a file
echo "Original content" > file.txt
git add file.txt
git commit -m "Initial commit"

# --- Practice Scenario 1: Discard working changes ---
echo "Bad changes" > file.txt
cat file.txt                    # See the bad changes
git restore file.txt
cat file.txt                    # Original content restored!

# --- Practice Scenario 2: Unstage a file ---
echo "New content" > file.txt
git add file.txt
git status                      # File is staged
git restore --staged file.txt
git status                      # File is modified but unstaged

# --- Practice Scenario 3: Undo a commit ---
git add file.txt
git commit -m "Change content"
git log --oneline               # See 2 commits
git reset --soft HEAD~1
git status                      # Changes are staged
git log --oneline               # Back to 1 commit

# --- Practice Scenario 4: Amend a commit ---
git commit -m "Commit with typo"
git commit --amend -m "Commit with fixed message"
git log --oneline               # Message is fixed

# --- Practice Scenario 5: View reflog ---
git reflog                      # See all HEAD movements
```

## Common Mistakes and Fixes

### "I ran reset --hard and lost my work!"

Check the reflog:
```bash
git reflog
git reset --hard HEAD@{1}   # Go back one step
```

### "I committed to the wrong branch!"

```bash
# Move commit to correct branch
git branch correct-branch     # Create new branch with commit
git reset --hard HEAD~1       # Remove from current branch
git checkout correct-branch   # Go to correct branch
```

### "I need to undo a merge!"

```bash
# If not pushed
git reset --hard HEAD~1

# If pushed
git revert -m 1 HEAD
```

---

## Summary

- `git restore file` discards working directory changes
- `git restore --staged file` unstages changes
- `git reset --soft/--mixed/--hard` undoes commits at different levels
- `git commit --amend` fixes the last commit
- `git revert` safely undoes pushed commits
- `git reflog` helps recover "lost" commits
- Always be careful with `--hard` and `git clean`

---

**Next:** [[09 - Understanding Branches]]

**Previous:** [[07 - Viewing History]]

**Back to:** [[00 - Welcome to Git & GitHub]]
