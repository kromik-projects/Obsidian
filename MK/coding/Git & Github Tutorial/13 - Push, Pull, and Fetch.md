# Push, Pull, and Fetch

## Overview

These three commands sync your local repository with remotes:

| Command | Direction | What It Does |
|---------|-----------|--------------|
| `push` | Local → Remote | Upload your commits |
| `fetch` | Remote → Local | Download commits (don't merge) |
| `pull` | Remote → Local | Download AND merge commits |

```
         ┌──────────────────┐
         │  Remote (GitHub) │
         └────────┬─────────┘
                  │
         push ↑   │   ↓ fetch/pull
                  │
         ┌────────┴─────────┐
         │  Local (Your PC) │
         └──────────────────┘
```

## Git Push

### Basic Push

Upload your commits to a remote:

```bash
git push origin main
```

- `origin` = the remote name
- `main` = the branch to push

### First Push (Set Upstream)

When pushing a new branch for the first time:

```bash
git push -u origin main
```

The `-u` flag sets up tracking. After this, you can just use:

```bash
git push
```

### Push All Branches

```bash
git push --all origin
```

### Push Tags

```bash
# Push a specific tag
git push origin v1.0.0

# Push all tags
git push --tags
```

### Force Push (Dangerous!)

```bash
git push --force origin main
# or
git push -f origin main
```

> [!danger] Force Push Overwrites History!
> Only use force push when you know what you're doing. It can delete other people's work on shared branches.

### Safer Force Push

```bash
git push --force-with-lease origin main
```

This fails if someone else has pushed since you last fetched. Safer than `--force`.

## Git Fetch

### Fetch All Remotes

```bash
git fetch
```

### Fetch Specific Remote

```bash
git fetch origin
```

### Fetch Specific Branch

```bash
git fetch origin main
```

### What Fetch Does

1. Downloads new commits from remote
2. Updates remote tracking branches (`origin/main`, etc.)
3. Does NOT change your local branches
4. Does NOT modify your working directory

```
Before fetch:
Local:   ○ ── ○ ── ○ (main)
Remote:  ○ ── ○ ── ○ ── ○ ── ○

After fetch:
Local:   ○ ── ○ ── ○ (main)
         origin/main: ○ ── ○ ── ○ ── ○ ── ○  (downloaded but separate)
```

### Why Fetch First?

Fetch lets you:
- See what's new before merging
- Review changes before incorporating
- Avoid unexpected merge conflicts

```bash
# Fetch changes
git fetch origin

# See what's different
git log main..origin/main

# Then merge if you want
git merge origin/main
```

## Git Pull

### Basic Pull

```bash
git pull origin main
```

This is equivalent to:
```bash
git fetch origin main
git merge origin/main
```

### Pull Current Branch

When tracking is set up:

```bash
git pull
```

### Pull with Rebase

Instead of merging, replay your commits on top:

```bash
git pull --rebase origin main
```

Keeps history linear. Good for feature branches.

### Pull All Branches

```bash
git pull --all
```

## Fetch vs. Pull

| Fetch | Pull |
|-------|------|
| Downloads only | Downloads AND merges |
| Safe, no changes to working directory | May cause merge conflicts |
| Review first, merge later | Quick update |
| `git fetch` then `git merge` | `git pull` = fetch + merge |

### When to Use Each

**Use Fetch When:**
- You want to see what's changed first
- You're on a shared branch with others
- You want to review before merging
- You're paranoid (that's okay!)

**Use Pull When:**
- You trust the changes
- You want a quick update
- You're working alone
- You're on your own feature branch

## Handling Conflicts During Pull

If your local changes conflict with remote:

```bash
git pull origin main
# CONFLICT: Merge conflict in file.txt
```

Resolve the conflict (see [[11 - Merge Conflicts]]):
```bash
# Edit file to resolve
git add file.txt
git commit -m "Merge remote changes"
```

Or abort:
```bash
git merge --abort
```

## Common Workflows

### Start of Day

```bash
# Update your main branch
git switch main
git pull origin main

# Update your feature branch with latest main
git switch my-feature
git merge main
```

### Before Pushing

```bash
# Make sure you have latest changes
git fetch origin

# See if you're behind
git status

# If behind, pull first
git pull origin main

# Then push
git push origin main
```

### Keeping Feature Branch Updated

```bash
# On your feature branch
git fetch origin
git merge origin/main
# Or: git rebase origin/main
```

## Tracking Branches

### See Tracking Status

```bash
git status
```

Shows if you're ahead, behind, or diverged:
```
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
```

```
Your branch is behind 'origin/main' by 3 commits.
```

```
Your branch and 'origin/main' have diverged,
and have 2 and 3 different commits each.
```

### Set Upstream

```bash
git branch --set-upstream-to=origin/main main
```

## Practice Exercise

```bash
# This exercise assumes you have a GitHub repo set up

# Clone a repo (if you haven't)
git clone https://github.com/yourusername/test-repo.git
cd test-repo

# Make a change
echo "New line" >> README.md
git add README.md
git commit -m "Add new line"

# Fetch to see if remote has changed
git fetch origin

# Check status
git status

# Push your change
git push origin main

# Simulate someone else's change (edit file on GitHub website)

# Fetch to download their change
git fetch origin

# See what's different
git log main..origin/main

# Merge the changes
git merge origin/main
# Or: git pull origin main
```

## Common Errors

### "Updates were rejected"

```
! [rejected]        main -> main (non-fast-forward)
```

Remote has commits you don't have locally. Fix:
```bash
git pull origin main
# Resolve any conflicts
git push origin main
```

### "No upstream branch"

```
fatal: The current branch feature has no upstream branch.
```

Fix:
```bash
git push -u origin feature
```

### "Permission denied"

Check your authentication (SSH keys or access token).

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git push origin branch` | Upload commits |
| `git push -u origin branch` | Push and set tracking |
| `git push --force` | Overwrite remote (dangerous!) |
| `git fetch origin` | Download without merging |
| `git fetch --all` | Fetch all remotes |
| `git pull origin branch` | Fetch and merge |
| `git pull --rebase` | Fetch and rebase |
| `git status` | See ahead/behind status |

---

## Summary

- **Push** uploads your commits to the remote
- **Fetch** downloads commits without merging
- **Pull** downloads and immediately merges
- Fetch first to review changes safely
- Use `-u` on first push to set up tracking
- Never force push to shared branches
- Pull before pushing to avoid rejection errors

---

**Next:** [[14 - Introduction to GitHub]]

**Previous:** [[12 - Remote Repositories]]

**Back to:** [[00 - Welcome to Git & GitHub]]
