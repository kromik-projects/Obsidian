# Merge Conflicts

## What is a Merge Conflict?

A **merge conflict** occurs when Git can't automatically combine changes because both branches modified the same lines in a file. Git stops and asks you to decide which changes to keep.

```
main:     Changed line 5 to "Hello World"
feature:  Changed line 5 to "Hello Universe"

Git: "I can't decide which one you want. Please help!"
```

## When Do Conflicts Happen?

Conflicts occur when:
- Same line edited in both branches
- File deleted in one branch but edited in another
- Same file added in both branches with different content

## Recognizing a Conflict

When you try to merge and there's a conflict:

```bash
git merge feature
# Auto-merging file.txt
# CONFLICT (content): Merge conflict in file.txt
# Automatic merge failed; fix conflicts and then commit the result.
```

Check status:

```bash
git status
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#     both modified:   file.txt
```

## Anatomy of a Conflict

Git marks conflicts in the file:

```
Normal line above the conflict

<<<<<<< HEAD
This is what's in the current branch (main)
=======
This is what's in the feature branch
>>>>>>> feature

Normal line below the conflict
```

| Marker | Meaning |
|--------|---------|
| `<<<<<<< HEAD` | Start of your current branch's version |
| `=======` | Separator between versions |
| `>>>>>>> branch` | End of incoming branch's version |

## Resolving Conflicts Step by Step

### Step 1: Identify Conflicting Files

```bash
git status
```

Look for files under "Unmerged paths" or "both modified".

### Step 2: Open the Conflicting File

Open in your editor and find the conflict markers.

### Step 3: Choose What to Keep

You have options:
- Keep the HEAD version (current branch)
- Keep the incoming version (feature branch)
- Keep both
- Write something completely new

**Example: Keep HEAD version**
```
Normal line above the conflict

This is what's in the current branch (main)

Normal line below the conflict
```

**Example: Keep incoming version**
```
Normal line above the conflict

This is what's in the feature branch

Normal line below the conflict
```

**Example: Keep both**
```
Normal line above the conflict

This is what's in the current branch (main)
This is what's in the feature branch

Normal line below the conflict
```

**Example: Write new**
```
Normal line above the conflict

This is a completely new version I wrote

Normal line below the conflict
```

> [!important] Remove All Markers!
> You MUST remove `<<<<<<<`, `=======`, and `>>>>>>>` markers. They are not valid code/content!

### Step 4: Stage the Resolved File

```bash
git add file.txt
```

### Step 5: Complete the Merge

```bash
git commit -m "Merge feature branch, resolve conflict in file.txt"
```

## Hands-On Practice: Creating a Conflict

Let's intentionally create and resolve a conflict:

```bash
# Setup
mkdir conflict-practice && cd conflict-practice
git init

# Create initial file
echo "Line 1: Hello" > greeting.txt
echo "Line 2: World" >> greeting.txt
git add greeting.txt
git commit -m "Initial greeting"

# Create feature branch
git switch -c feature/update-greeting

# Modify on feature branch
echo "Line 1: Hi there" > greeting.txt
echo "Line 2: World" >> greeting.txt
git add greeting.txt
git commit -m "Change Hello to Hi there"

# Switch to main and make a DIFFERENT change to same line
git switch main
echo "Line 1: Hello everyone" > greeting.txt
echo "Line 2: World" >> greeting.txt
git add greeting.txt
git commit -m "Change Hello to Hello everyone"

# Now try to merge - CONFLICT!
git merge feature/update-greeting
```

You'll see:
```
Auto-merging greeting.txt
CONFLICT (content): Merge conflict in greeting.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Now look at the file:
```bash
cat greeting.txt
```

```
<<<<<<< HEAD
Line 1: Hello everyone
=======
Line 1: Hi there
>>>>>>> feature/update-greeting
Line 2: World
```

Resolve it:
```bash
# Edit the file to resolve (use your editor or:)
echo "Line 1: Hi everyone" > greeting.txt
echo "Line 2: World" >> greeting.txt

# Stage and commit
git add greeting.txt
git commit -m "Merge: combine greetings"
```

## Using VS Code to Resolve Conflicts

VS Code provides a visual interface for conflicts:

1. Open the conflicting file
2. You'll see highlighting and buttons:
   - **Accept Current Change** - Keep HEAD version
   - **Accept Incoming Change** - Keep other branch
   - **Accept Both Changes** - Keep both
   - **Compare Changes** - See side-by-side

3. Click the option you want or manually edit
4. Save the file
5. Stage and commit

## Using Command Line Tools

### See Differences

```bash
# See conflict in detail
git diff

# See what the original looked like
git diff --base

# See your version
git diff --ours

# See their version
git diff --theirs
```

### Choose One Side Completely

```bash
# Keep our version of a file
git checkout --ours filename.txt

# Keep their version of a file
git checkout --theirs filename.txt

# Then stage it
git add filename.txt
```

## Aborting a Merge

Changed your mind? Cancel the merge:

```bash
git merge --abort
```

This restores everything to before the merge started.

## Tips for Avoiding Conflicts

### 1. Pull Often

```bash
git pull origin main
```

Keep your branch up to date with main.

### 2. Make Small, Focused Changes

Large changes spanning many files = more conflict potential.

### 3. Communicate with Your Team

"I'm working on the header" prevents two people editing the same code.

### 4. Merge Main into Feature Regularly

```bash
# While on your feature branch
git merge main
```

Resolve small conflicts as you go rather than one big mess at the end.

## Multiple Conflicts

If multiple files have conflicts:

```bash
git status
# both modified:   file1.txt
# both modified:   file2.txt
# both modified:   file3.txt
```

Resolve each one:
```bash
# Fix file1.txt
git add file1.txt

# Fix file2.txt
git add file2.txt

# Fix file3.txt
git add file3.txt

# Commit all resolutions
git commit -m "Merge feature, resolve conflicts"
```

## Common Conflict Scenarios

### Same Line Edited

Most common. Choose one version or combine manually.

### File Deleted in One Branch

```
CONFLICT (modify/delete): file.txt deleted in feature and modified in HEAD.
```

Decide: Should the file exist or not?
```bash
# Keep the file
git add file.txt

# Delete the file
git rm file.txt
```

### Same New File in Both Branches

```
CONFLICT (add/add): Merge conflict in newfile.txt
```

Both branches created the same file with different content. Combine or choose one.

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git status` | See conflicting files |
| `git diff` | See conflicts in detail |
| `git checkout --ours file` | Keep our version |
| `git checkout --theirs file` | Keep their version |
| `git add file` | Mark as resolved |
| `git commit` | Complete merge |
| `git merge --abort` | Cancel merge |

---

## Summary

- Conflicts happen when Git can't automatically merge changes
- Look for `<<<<<<<`, `=======`, `>>>>>>>` markers in files
- Manually edit to resolve, then remove all markers
- Stage resolved files with `git add`
- Commit to complete the merge
- Use `git merge --abort` to cancel if needed
- Pull often and make small changes to minimize conflicts

---

**Next:** [[12 - Remote Repositories]]

**Previous:** [[10 - Merging Branches]]

**Back to:** [[00 - Welcome to Git & GitHub]]
