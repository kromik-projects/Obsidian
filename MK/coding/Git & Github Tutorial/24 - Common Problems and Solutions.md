# Common Problems and Solutions

## Quick Fixes for Everyday Git Issues

This guide covers the most common Git problems and how to solve them.

---

## Commit Issues

### I Made a Typo in My Last Commit Message

```bash
git commit --amend -m "Corrected message"
```

> [!warning] Only for Unpushed Commits
> If already pushed, you'll need to force push, which can cause issues for others.

### I Forgot to Add a File to My Last Commit

```bash
git add forgotten-file.txt
git commit --amend --no-edit
```

### I Committed to the Wrong Branch

**If you haven't pushed yet:**
```bash
# Create new branch with your commit
git branch correct-branch

# Remove commit from current branch
git reset --hard HEAD~1

# Switch to correct branch
git switch correct-branch
```

**If you've already pushed:**
```bash
# On wrong branch, note the commit hash
git log --oneline -1

# Switch to correct branch
git switch correct-branch

# Cherry-pick the commit
git cherry-pick <commit-hash>

# Go back and remove from wrong branch
git switch wrong-branch
git revert <commit-hash>
git push
```

### I Need to Undo My Last Commit

**Keep the changes:**
```bash
git reset --soft HEAD~1
# Changes are now staged
```

**Discard the changes:**
```bash
git reset --hard HEAD~1
# Warning: Changes are gone!
```

### I Need to Undo a Commit I Already Pushed

```bash
git revert <commit-hash>
git push
```

This creates a new commit that undoes the changes safely.

---

## Staging Issues

### I Staged the Wrong File

```bash
git restore --staged wrong-file.txt
```

### I Want to Unstage Everything

```bash
git restore --staged .
```

### I Only Want to Stage Part of a File

```bash
git add -p filename.txt
# Answer y/n for each chunk
```

---

## Working Directory Issues

### I Want to Discard All My Changes

```bash
# Discard tracked file changes
git restore .

# Also remove untracked files
git clean -fd
```

### I Accidentally Deleted a File

```bash
# If not committed yet
git restore deleted-file.txt

# If already committed, restore from last commit
git checkout HEAD -- deleted-file.txt
```

### I Want to See a File from a Different Commit

```bash
git show <commit>:path/to/file.txt
```

### I Modified Files But Need to Switch Branches

**Option 1: Stash changes**
```bash
git stash
git switch other-branch
# Do work
git switch original-branch
git stash pop
```

**Option 2: Commit as WIP**
```bash
git add .
git commit -m "WIP: Saving work in progress"
git switch other-branch
# Later, undo the WIP commit:
git reset --soft HEAD~1
```

---

## Branch Issues

### I Want to Delete a Branch But Git Won't Let Me

**Error:** "The branch is not fully merged"

```bash
# Force delete
git branch -D branch-name
```

### I Need to Rename a Branch

```bash
# Rename current branch
git branch -m new-name

# Rename any branch
git branch -m old-name new-name

# If pushed, update remote
git push origin -u new-name
git push origin --delete old-name
```

### My Branch Is Behind Main

```bash
git switch my-branch
git fetch origin
git merge origin/main

# Or with rebase (cleaner history)
git rebase origin/main
```

### I Need to Create a Branch from an Older Commit

```bash
git branch new-branch <commit-hash>
# or
git switch -c new-branch <commit-hash>
```

---

## Merge Issues

### I Have Merge Conflicts

1. See conflicting files:
   ```bash
   git status
   ```

2. Open each file and look for:
   ```
   <<<<<<< HEAD
   Your changes
   =======
   Their changes
   >>>>>>> branch-name
   ```

3. Edit to resolve, remove markers

4. Stage and commit:
   ```bash
   git add .
   git commit -m "Resolve merge conflicts"
   ```

### I Want to Abort a Merge

```bash
git merge --abort
```

### I Want to Use Their Version for Everything

```bash
git checkout --theirs .
git add .
git commit -m "Resolve conflicts using their version"
```

### I Want to Use My Version for Everything

```bash
git checkout --ours .
git add .
git commit -m "Resolve conflicts using our version"
```

---

## Remote Issues

### I'm Getting "Permission Denied"

**For HTTPS:**
- Use a Personal Access Token, not your password
- Generate at: GitHub Settings → Developer Settings → Personal Access Tokens

**For SSH:**
```bash
# Check if key is added
ssh-add -l

# Add your key
ssh-add ~/.ssh/id_ed25519

# Test connection
ssh -T git@github.com
```

### Push Was Rejected (Non-Fast-Forward)

Remote has commits you don't have:
```bash
git pull origin branch-name
# Resolve any conflicts
git push origin branch-name
```

### I Pushed to the Wrong Branch

```bash
# Remove from wrong branch
git push origin --delete wrong-branch

# Push to correct branch
git push origin correct-branch
```

### I Need to Change the Remote URL

```bash
git remote set-url origin new-url
```

### I Want to Undo a Push

**Safe way (creates revert commit):**
```bash
git revert <commit-hash>
git push
```

**Dangerous way (rewrites history):**
```bash
git reset --hard HEAD~1
git push --force
```

> [!danger] Force Push Warning
> Only force push to branches you alone are using!

---

## Stash Issues

### I Stashed and Now I Can't Find It

```bash
git stash list
```

Shows all stashes. Apply with:
```bash
git stash pop stash@{n}
```

### I Want to See What's in a Stash

```bash
git stash show -p stash@{n}
```

### I Applied the Wrong Stash

If you used `pop`, the stash is gone. Use `apply` next time to keep it.

---

## Recovery

### I Ran reset --hard and Lost My Work

Check the reflog:
```bash
git reflog
```

Find the commit before the reset and:
```bash
git reset --hard HEAD@{n}
```

### I Deleted a Branch and Need It Back

```bash
git reflog
# Find the commit that was the tip of the branch
git branch recovered-branch <commit-hash>
```

### I Need to Find a Deleted File

```bash
# Find commits that deleted files
git log --diff-filter=D --summary | grep delete

# Restore the file
git checkout <commit-before-deletion> -- path/to/file
```

### My Repository Seems Corrupted

```bash
# Check for issues
git fsck

# Attempt repair
git gc
```

---

## Performance Issues

### Git Is Slow

```bash
# Clean up
git gc --aggressive

# Reduce history (if repo is huge)
git clone --depth 1 <url>
```

### .git Folder Is Huge

```bash
# Find large files
git rev-list --objects --all | \
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
  sort -k3 -n | tail -20

# Clean up
git gc --prune=now
```

---

## Common Error Messages

| Error | Meaning | Solution |
|-------|---------|----------|
| `not a git repository` | No .git folder | Run `git init` or cd to right folder |
| `nothing to commit` | No changes to save | Make changes first |
| `diverged` | Both sides have new commits | Pull and merge/rebase |
| `would be overwritten` | Local changes would be lost | Commit or stash first |
| `permission denied` | Auth issue | Check credentials/SSH |
| `rejected non-fast-forward` | Remote has new commits | Pull first, then push |
| `merge conflict` | Same lines changed | Resolve manually |
| `detached HEAD` | Not on a branch | Checkout a branch |

---

## Prevention Tips

1. **Commit often** - Smaller commits are easier to fix
2. **Pull before push** - Avoid conflicts
3. **Use branches** - Don't work directly on main
4. **Check status** - Run `git status` frequently
5. **Read error messages** - Git usually tells you what to do
6. **Use `--dry-run`** - Test commands safely first

---

**Next:** [[25 - Glossary]]

**Previous:** [[23 - Git Commands Cheatsheet]]

**Back to:** [[00 - Welcome to Git & GitHub]]
