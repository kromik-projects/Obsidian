# The Git Workflow

## Understanding How Git Works

Before diving into commands, it's crucial to understand **how Git thinks about your files**. This mental model will make everything else easier to understand.

## The Three Areas

Git manages your project using three main areas:

```
┌─────────────────┐    git add     ┌─────────────────┐   git commit   ┌─────────────────┐
│                 │ ────────────►  │                 │ ────────────►  │                 │
│  Working        │                │  Staging Area   │                │   Repository    │
│  Directory      │                │  (Index)        │                │   (.git)        │
│                 │ ◄────────────  │                 │                │                 │
└─────────────────┘   (editing)    └─────────────────┘                └─────────────────┘

   Your files           Files ready                    Permanent
   as you see           to be saved                    snapshots
   and edit them        (next commit)                  (history)
```

### 1. Working Directory
- The actual files you see in your folder
- Where you do your work—editing, creating, deleting files
- Changes here are not saved to Git until you tell Git about them

### 2. Staging Area (Index)
- A preparation area for your next commit
- Think of it as a "shopping cart" for changes
- You decide exactly which changes to include in the next save

### 3. Repository (History)
- The `.git` folder containing all your commits
- Permanent record of all saved snapshots
- Can never be accidentally modified

## The Basic Workflow

The everyday Git workflow follows these steps:

```
1. MODIFY files in your working directory
        ↓
2. STAGE the changes you want to include (git add)
        ↓
3. COMMIT the staged changes (git commit)
        ↓
   Changes are now saved permanently!
```

### Real Example

```bash
# You edit a file...
echo "Hello World" > hello.txt

# 1. File is in Working Directory (untracked or modified)
git status
# Shows: Untracked files: hello.txt

# 2. Stage the file
git add hello.txt
git status
# Shows: Changes to be committed: new file: hello.txt

# 3. Commit the staged changes
git commit -m "Add hello.txt file"
# Shows: 1 file changed, 1 insertion(+)

# File is now saved in repository history!
```

## File States in Git

Files in a Git repository can be in one of these states:

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│  UNTRACKED ──────► STAGED ──────► COMMITTED                     │
│       │              ↑                │                         │
│       │              │                │                         │
│       │              │                ↓                         │
│       └──────────────────────── MODIFIED ◄──────────────────┘   │
│                      │                                          │
│                      │                                          │
│                      └───────► STAGED ──────► COMMITTED         │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### State Definitions

| State | Description | How to Recognize |
|-------|-------------|------------------|
| **Untracked** | New file Git doesn't know about | Red in `git status`, under "Untracked files" |
| **Staged** | Changes marked for next commit | Green in `git status`, under "Changes to be committed" |
| **Committed** | Saved in repository history | Clean `git status` with "nothing to commit" |
| **Modified** | Tracked file with unsaved changes | Red in `git status`, under "Changes not staged" |

## Understanding git status Output

```bash
git status
```

Let's decode what you might see:

### Clean Repository
```
On branch main
nothing to commit, working tree clean
```
All changes are committed. Working directory matches last commit.

### Untracked Files
```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        newfile.txt
```
Git sees the file but isn't tracking it.

### Staged Changes
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   newfile.txt
        modified:   existingfile.txt
```
These changes will be included in the next commit.

### Modified But Not Staged
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   myfile.txt
```
File was changed but you haven't staged the changes yet.

### Mixed Status
```
On branch main
Changes to be committed:
        modified:   file1.txt

Changes not staged for commit:
        modified:   file2.txt

Untracked files:
        file3.txt
```
You have staged changes, unstaged changes, AND untracked files.

## The Staging Area: Why Bother?

You might wonder: "Why not just save everything at once?"

The staging area gives you **precise control** over what goes into each commit.

### Example: Working on Multiple Things

Imagine you:
1. Fixed a bug in `login.js`
2. Updated the README
3. Started a new feature in `feature.js` (not finished)

Without staging, you'd have to save everything together. With staging:

```bash
# Stage only the completed work
git add login.js README.md

# Commit just those files
git commit -m "Fix login bug and update README"

# feature.js stays as a work in progress
```

### Benefits of Staging

- **Organize your commits** - Group related changes together
- **Review before committing** - Double-check what you're about to save
- **Partial staging** - Commit some changes from a file, leave others
- **Clean history** - Create logical, well-organized commit history

## Short Status View

For a more compact view:

```bash
git status -s
# or
git status --short
```

Output:
```
 M file1.txt      # Modified, not staged
M  file2.txt      # Modified and staged
A  file3.txt      # New file, staged
?? file4.txt      # Untracked
MM file5.txt      # Staged modifications + more unstaged modifications
```

The columns mean:
- **Left column** = Staging area status
- **Right column** = Working directory status

| Code | Meaning |
|------|---------|
| `M` | Modified |
| `A` | Added (new file) |
| `D` | Deleted |
| `R` | Renamed |
| `?` | Untracked |
| ` ` | Unchanged |

## Visualizing the Workflow

```
┌──────────────────────────────────────────────────────────────────────┐
│                           YOUR PROJECT                               │
│                                                                      │
│  ┌────────────────┐     ┌────────────────┐     ┌────────────────┐   │
│  │   app.js       │     │   style.css    │     │   index.html   │   │
│  │   (modified)   │     │   (untracked)  │     │   (unchanged)  │   │
│  └───────┬────────┘     └───────┬────────┘     └────────────────┘   │
│          │                      │                                    │
│          │ git add app.js       │ git add style.css                  │
│          ▼                      ▼                                    │
│  ┌─────────────────────────────────────────┐                        │
│  │            STAGING AREA                  │                        │
│  │  ┌──────────┐     ┌──────────┐          │                        │
│  │  │  app.js  │     │style.css │          │                        │
│  │  └──────────┘     └──────────┘          │                        │
│  └───────────────────────┬─────────────────┘                        │
│                          │                                           │
│                          │ git commit -m "Update styles"             │
│                          ▼                                           │
│  ┌─────────────────────────────────────────┐                        │
│  │            REPOSITORY                    │                        │
│  │                                         │                        │
│  │  commit 3: "Update styles" ◄── HEAD    │                        │
│  │  commit 2: "Add login page"             │                        │
│  │  commit 1: "Initial commit"             │                        │
│  │                                         │                        │
│  └─────────────────────────────────────────┘                        │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

## Practice Exercise

Let's practice the complete workflow:

```bash
# 1. Create or go to your practice repo
cd ~/my-first-repo

# 2. Check current status
git status

# 3. Create a new file
echo "Learning the Git workflow" > workflow.txt

# 4. Check status - file should be untracked
git status

# 5. Stage the file
git add workflow.txt

# 6. Check status - file should be staged
git status

# 7. Modify the file again
echo "This is really helpful!" >> workflow.txt

# 8. Check status - same file appears twice!
git status
# You'll see: staged (old content) AND modified (new content)

# 9. Stage the new changes too
git add workflow.txt

# 10. Check status - all changes staged
git status

# Don't commit yet - we'll do that in the next lesson!
```

## Key Takeaways

| Concept | What It Means |
|---------|---------------|
| **Working Directory** | Your actual files |
| **Staging Area** | Preparation area for commits |
| **Repository** | Saved history of commits |
| **Untracked** | New file Git doesn't know about |
| **Modified** | Changed file not yet staged |
| **Staged** | Ready to be committed |
| **Committed** | Saved to repository history |

---

## Summary

- Git uses three areas: Working Directory, Staging Area, and Repository
- The workflow is: Edit → Stage → Commit
- The staging area lets you choose exactly what to commit
- `git status` shows you the current state of all files
- Understanding this workflow is fundamental to using Git effectively

---

**Next:** [[06 - Staging and Committing]]

**Previous:** [[04 - Your First Repository]]

**Back to:** [[00 - Welcome to Git & GitHub]]
