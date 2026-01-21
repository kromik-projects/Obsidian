# Merging Branches

## What is Merging?

**Merging** combines the changes from one branch into another. It's how you bring completed work back into your main codebase.

```
Before merge:

    main:    ○ ── ○ ── ○

    feature: ○ ── ○ ── ○ ── ○ ── ○

After merge:

    main:    ○ ── ○ ── ○ ────────────── ●
                        \             /
    feature:             ○ ── ○ ── ○
```

The `●` is a merge commit that combines both histories.

## Basic Merge Workflow

### Step 1: Switch to the Target Branch

First, go to the branch you want to merge INTO (usually main):

```bash
git switch main
```

### Step 2: Merge the Feature Branch

```bash
git merge feature-branch
```

### Step 3: That's It!

Git creates a merge commit and your main branch now includes all the feature branch changes.

## Types of Merges

### Fast-Forward Merge

When the target branch hasn't changed since you branched off:

```
Before:
main:    ○ ── ○ ── ○
                    \
feature:             ○ ── ○ ── ○
                              ↑
                            HEAD

After fast-forward:
main:    ○ ── ○ ── ○ ── ○ ── ○ ── ○
                                  ↑
                               HEAD
```

Git just moves the pointer forward. No merge commit needed.

```bash
git merge feature
# Updating abc1234..def5678
# Fast-forward
```

### Three-Way Merge

When both branches have new commits:

```
Before:
main:    ○ ── ○ ── ○ ── ○
                    \
feature:             ○ ── ○

After three-way merge:
main:    ○ ── ○ ── ○ ── ○ ───── ●  (merge commit)
                    \         /
feature:             ○ ── ○ ─┘
```

Git creates a merge commit combining both branches.

```bash
git merge feature
# Merge made by the 'ort' strategy.
```

## Merge Options

### Keep History Linear (Fast-Forward Only)

```bash
git merge --ff-only feature
```

Fails if fast-forward isn't possible.

### Always Create Merge Commit (No Fast-Forward)

```bash
git merge --no-ff feature
```

Creates a merge commit even when fast-forward is possible. This preserves the history of the feature branch.

### Squash Into Single Commit

```bash
git merge --squash feature
```

Combines all feature commits into staged changes. You then commit them as a single commit. The feature branch history is lost.

## Step-by-Step Example

```bash
# Start fresh
mkdir merge-practice && cd merge-practice
git init

# Create initial commit on main
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"

# Create feature branch
git switch -c feature/add-header

# Add feature commits
echo "<header>My Site</header>" > header.html
git add header.html
git commit -m "Add header HTML"

echo "header { background: blue; }" > header.css
git add header.css
git commit -m "Add header styles"

# Check branch graph
git log --oneline --graph --all

# Switch to main
git switch main

# Merge the feature
git merge feature/add-header

# See the result
git log --oneline --graph --all
ls  # header.html and header.css are now on main!

# Clean up - delete the merged branch
git branch -d feature/add-header
```

## Aborting a Merge

If something goes wrong mid-merge:

```bash
git merge --abort
```

This returns everything to the state before you started the merge.

## After Merging

### Delete the Merged Branch

Once merged, you typically delete the feature branch:

```bash
git branch -d feature-branch
```

### Check the Result

```bash
# See the merge commit
git log --oneline

# Visualize the merge
git log --oneline --graph
```

## Merge Strategies

Git automatically chooses a strategy, but you can specify one:

```bash
# Default strategy (ort - faster, better)
git merge -s ort feature

# Recursive strategy (older default)
git merge -s recursive feature
```

For most uses, let Git decide.

## Practice: Multiple Merges

```bash
# Setup
mkdir multi-merge && cd multi-merge
git init
echo "Initial" > file.txt
git add file.txt
git commit -m "Initial commit"

# Create branch A
git switch -c feature-a
echo "Feature A" >> file.txt
git add file.txt
git commit -m "Add feature A"

# Go back to main, create branch B
git switch main
git switch -c feature-b
echo "Feature B" > new-file.txt
git add new-file.txt
git commit -m "Add feature B"

# Merge both into main
git switch main

git merge feature-a
# Fast-forward (main had no new commits)

git merge feature-b
# Three-way merge (main now has feature-a commits)

# View result
git log --oneline --graph --all
```

## When to Merge

- Feature is complete and tested
- Code has been reviewed (if using pull requests)
- All tests pass
- The feature is ready for production

## Merge vs. Other Strategies

| Strategy | When to Use |
|----------|-------------|
| **Merge** | Preserves complete history, team standard |
| **Squash** | Clean up messy branch history |
| **Rebase** | Keep linear history (advanced, covered later) |

## Common Issues

### "Already up to date"

The branch has already been merged:

```bash
git merge feature
# Already up to date.
```

### Merge Conflicts

When both branches edit the same lines, Git can't decide which version to keep. This is covered in detail in [[11 - Merge Conflicts]].

### Merge Won't Fast-Forward

If you use `--ff-only` but fast-forward isn't possible:

```bash
git merge --ff-only feature
# fatal: Not possible to fast-forward, aborting.
```

Either merge normally or rebase first.

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git merge branch` | Merge branch into current |
| `git merge --no-ff branch` | Force merge commit |
| `git merge --ff-only branch` | Only fast-forward |
| `git merge --squash branch` | Combine commits |
| `git merge --abort` | Cancel in-progress merge |
| `git branch -d branch` | Delete merged branch |

---

## Summary

- Merging combines branches together
- Fast-forward: target hasn't changed, just moves pointer
- Three-way: both changed, creates merge commit
- Always merge INTO the target branch (usually main)
- Use `--no-ff` to preserve branch history
- Delete feature branches after merging
- Conflicts happen when same lines are edited (next lesson!)

---

**Next:** [[11 - Merge Conflicts]]

**Previous:** [[09 - Understanding Branches]]

**Back to:** [[00 - Welcome to Git & GitHub]]
