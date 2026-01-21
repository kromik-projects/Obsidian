# Forking Projects

## What is a Fork?

A **fork** is a personal copy of someone else's repository on your GitHub account. It allows you to:

- Experiment with changes without affecting the original
- Propose changes to the original project (via pull requests)
- Use someone's project as a starting point for your own

```
Original Repository              Your Fork
(original-owner/project)         (your-username/project)
┌────────────────────┐           ┌────────────────────┐
│  ○ ── ○ ── ○ ── ○ │  fork →  │  ○ ── ○ ── ○ ── ○ │
│                    │           │         ↓          │
│  (read-only for    │           │    Your changes    │
│   most users)      │           │         ↓          │
│                    │           │     ○ ── ○ ── ○   │
└────────────────────┘           └────────────────────┘
           ↑                              │
           └──────────────────────────────┘
                    Pull Request
```

## Fork vs. Clone

| Fork | Clone |
|------|-------|
| Creates copy on GitHub | Creates copy on your computer |
| Lives on GitHub servers | Lives on your machine |
| You own the fork | You have a local copy |
| Can diverge from original | Direct copy |
| First step for contributing | Done after forking |

**Workflow:** Fork on GitHub → Clone to computer → Work locally → Push to fork → Create pull request

## How to Fork

### Step 1: Find the Repository

Go to the project you want to fork on GitHub.

### Step 2: Click Fork

Click the **Fork** button in the top right corner.

### Step 3: Choose Destination

Select your account (or an organization you belong to).

### Step 4: Wait

GitHub creates a copy. This takes a few seconds.

### Step 5: You Have a Fork!

Now at `github.com/your-username/project-name`

## Working with Your Fork

### Clone Your Fork

```bash
git clone git@github.com:your-username/project-name.git
cd project-name
```

### Add the Original as "Upstream"

This lets you get updates from the original project:

```bash
git remote add upstream git@github.com:original-owner/project-name.git
```

### Verify Your Remotes

```bash
git remote -v
```

You should see:
```
origin    git@github.com:your-username/project-name.git (fetch)
origin    git@github.com:your-username/project-name.git (push)
upstream  git@github.com:original-owner/project-name.git (fetch)
upstream  git@github.com:original-owner/project-name.git (push)
```

## Keeping Your Fork Updated

The original project continues to evolve. Stay updated:

### Fetch Upstream Changes

```bash
git fetch upstream
```

### Merge into Your Main Branch

```bash
git switch main
git merge upstream/main
```

### Push Updates to Your Fork

```bash
git push origin main
```

### Complete Update Script

```bash
# Update your fork with latest from original
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

## The Fork Contribution Workflow

### 1. Fork the Repository

Click Fork on GitHub.

### 2. Clone Your Fork

```bash
git clone git@github.com:your-username/project.git
cd project
git remote add upstream git@github.com:original/project.git
```

### 3. Create a Feature Branch

```bash
git switch -c feature/my-contribution
```

### 4. Make Your Changes

```bash
# Edit files, add features, fix bugs
git add .
git commit -m "Add awesome feature"
```

### 5. Push to Your Fork

```bash
git push origin feature/my-contribution
```

### 6. Create a Pull Request

1. Go to your fork on GitHub
2. Click "Compare & pull request" or "Contribute"
3. Fill in details about your changes
4. Submit the pull request

### 7. Respond to Feedback

Maintainers may request changes:
```bash
# Make requested changes
git add .
git commit -m "Address review feedback"
git push origin feature/my-contribution
```

The PR updates automatically.

### 8. Celebrate When Merged!

Once merged, clean up:
```bash
git switch main
git pull upstream main
git push origin main
git branch -d feature/my-contribution
```

## Best Practices for Forking

### Keep Main Clean

Never commit directly to main in your fork. Always use feature branches:

```bash
# Good
git switch -c fix/typo-in-readme

# Bad
git switch main
# (making changes directly)
```

### Sync Before Starting New Work

```bash
git fetch upstream
git switch main
git merge upstream/main
git switch -c new-feature
```

### Write Good Commit Messages

Follow the project's conventions. Common format:
```
type(scope): brief description

Longer explanation if needed.

Fixes #123
```

### Read CONTRIBUTING.md

Most projects have contribution guidelines. Follow them!

## Fork Settings

### Syncing Your Fork (GitHub UI)

GitHub now offers a "Sync fork" button:
1. Go to your fork on GitHub
2. If behind, you'll see "This branch is X commits behind"
3. Click "Sync fork" → "Update branch"

### Changing Fork Visibility

You can't make a fork of a public repo private. But you can:
1. Clone the original
2. Create a new private repo
3. Push to your private repo (but you lose fork connection)

### Deleting a Fork

If you no longer need the fork:
1. Go to fork Settings
2. Scroll to "Danger Zone"
3. Click "Delete this repository"

Deleting a fork doesn't affect the original or any PRs.

## Common Scenarios

### "I Forked, But Now It's Outdated"

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

### "I Want to Start Fresh"

Option 1: Reset to upstream
```bash
git switch main
git fetch upstream
git reset --hard upstream/main
git push --force origin main
```

Option 2: Delete fork and re-fork on GitHub

### "I Made Commits to Main by Accident"

Move them to a branch:
```bash
# Create branch with your commits
git branch my-work

# Reset main to match upstream
git fetch upstream
git reset --hard upstream/main

# Push reset main
git push --force origin main

# Switch to your work
git switch my-work
git push origin my-work
```

## Practice Exercise

Let's practice the fork workflow:

1. **Find a project to fork**
   - Go to https://github.com/octocat/Spoon-Knife
   - This is a practice repo for forking!

2. **Fork it**
   - Click the Fork button

3. **Clone your fork**
   ```bash
   git clone git@github.com:your-username/Spoon-Knife.git
   cd Spoon-Knife
   ```

4. **Add upstream**
   ```bash
   git remote add upstream git@github.com:octocat/Spoon-Knife.git
   git remote -v
   ```

5. **Create a feature branch**
   ```bash
   git switch -c my-contribution
   ```

6. **Make a change**
   ```bash
   echo "Contributed by $(git config user.name)" >> CONTRIBUTORS.md
   git add CONTRIBUTORS.md
   git commit -m "Add myself to contributors"
   ```

7. **Push to your fork**
   ```bash
   git push origin my-contribution
   ```

8. **Create a Pull Request** (optional - Spoon-Knife accepts them!)

---

## Summary

- Forking creates a copy of a repository on your GitHub account
- Fork first, then clone your fork locally
- Add `upstream` remote to track the original project
- Keep your fork updated by fetching from upstream
- Always work in feature branches, not main
- Submit pull requests to propose changes to the original

---

**Next:** [[19 - Pull Requests]]

**Previous:** [[17 - Cloning Repositories]]

**Back to:** [[00 - Welcome to Git & GitHub]]
