# Cloning Repositories

## What is Cloning?

**Cloning** creates a complete local copy of a remote repository, including:

- All files
- Complete commit history
- All branches
- Remote connection (origin)

```
GitHub Repository                Your Computer
┌────────────────┐              ┌────────────────┐
│  ○ ── ○ ── ○  │   clone →   │  ○ ── ○ ── ○  │
│  All branches  │              │  All branches  │
│  All history   │              │  All history   │
└────────────────┘              └────────────────┘
```

## How to Clone

### Step 1: Get the Repository URL

On GitHub:
1. Go to the repository page
2. Click the green **Code** button
3. Copy the URL (HTTPS or SSH)

### Step 2: Clone the Repository

```bash
# HTTPS
git clone https://github.com/username/repository.git

# SSH
git clone git@github.com:username/repository.git
```

This creates a folder named after the repository.

### Clone with a Different Folder Name

```bash
git clone https://github.com/username/repository.git my-custom-folder
```

## What Happens When You Clone

Git automatically:

1. Creates a new directory
2. Initializes a Git repository
3. Downloads all commits and branches
4. Checks out the default branch (usually `main`)
5. Sets up `origin` remote pointing to the source

```bash
# After cloning
cd repository

# Remote is already configured
git remote -v
# origin  https://github.com/username/repository.git (fetch)
# origin  https://github.com/username/repository.git (push)

# You're on the default branch
git branch
# * main
```

## Cloning Options

### Shallow Clone (Latest Only)

For large repos, clone only recent history:

```bash
# Only last commit
git clone --depth 1 https://github.com/username/repository.git

# Last 10 commits
git clone --depth 10 https://github.com/username/repository.git
```

Saves time and disk space. You can get more history later:
```bash
git fetch --unshallow
```

### Clone Specific Branch

```bash
git clone --branch develop https://github.com/username/repository.git

# Or shorter
git clone -b develop https://github.com/username/repository.git
```

### Clone Single Branch

Only download one branch (saves space):

```bash
git clone --single-branch --branch main https://github.com/username/repository.git
```

### Clone with Submodules

If the repo has submodules (other repos inside):

```bash
git clone --recurse-submodules https://github.com/username/repository.git
```

## Working with a Cloned Repository

### View Remote Branches

```bash
# All remote branches
git branch -r

# Output:
# origin/main
# origin/develop
# origin/feature-x
```

### Switch to a Remote Branch

```bash
# Modern way
git switch develop

# Creates local branch tracking origin/develop
```

### Get Latest Changes

```bash
git pull origin main
```

## Cloning Private Repositories

### HTTPS (Password/Token)

```bash
git clone https://github.com/username/private-repo.git
# Enter username and personal access token
```

### SSH (Recommended)

```bash
git clone git@github.com:username/private-repo.git
# Uses your SSH key - no password needed
```

## Clone vs. Fork vs. Download ZIP

| Action | What You Get | Can Push? | Has Git? |
|--------|-------------|-----------|----------|
| **Clone** | Full repo with history | Yes (if permitted) | Yes |
| **Fork** | Copy on your GitHub | Yes (to your fork) | After clone |
| **Download ZIP** | Just the files | No | No |

- **Clone** - You want to work on a project (your own or as a collaborator)
- **Fork** - You want to modify someone else's project
- **Download** - You just want the files without Git

## Common Cloning Scenarios

### Clone Your Own Repository

```bash
git clone git@github.com:yourusername/your-project.git
```

You can push and pull freely.

### Clone as a Collaborator

If you have write access:
```bash
git clone git@github.com:organization/project.git
```

You can push to branches (but may need PRs for main).

### Clone to Contribute (Fork First)

1. Fork the repository on GitHub
2. Clone YOUR fork:
   ```bash
   git clone git@github.com:yourusername/forked-project.git
   ```
3. Add original as upstream:
   ```bash
   git remote add upstream git@github.com:original/project.git
   ```

## Troubleshooting

### "Repository not found"

```
fatal: repository 'https://github.com/user/repo.git/' not found
```

- Check the URL is correct
- Make sure the repo exists
- If private, check you have access

### "Permission denied"

```
Permission denied (publickey)
```

- SSH key not set up correctly
- Try HTTPS instead
- Check your SSH key is added to GitHub

### Clone is Very Slow

Try shallow clone:
```bash
git clone --depth 1 https://github.com/username/repository.git
```

### "Authentication failed"

- HTTPS: Use personal access token, not password
- SSH: Make sure your key is added to ssh-agent

## Practice Exercise

```bash
# 1. Clone a public repository
git clone https://github.com/octocat/Hello-World.git
cd Hello-World

# 2. Explore what was cloned
ls -la                    # See files
git log --oneline -5      # Recent commits
git branch -a             # All branches
git remote -v             # Remote info

# 3. Clone your own repo
cd ..
git clone git@github.com:yourusername/hello-github.git
cd hello-github

# 4. Make a change
echo "Cloned and modified!" >> README.md
git add README.md
git commit -m "Update from cloned repo"
git push origin main

# 5. Shallow clone example
cd ..
git clone --depth 1 https://github.com/facebook/react.git
du -sh react              # See how big it is

# Clean up
cd ..
rm -rf Hello-World hello-github react
```

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git clone <url>` | Clone with default folder name |
| `git clone <url> <folder>` | Clone to specific folder |
| `git clone --depth 1 <url>` | Shallow clone (latest only) |
| `git clone -b <branch> <url>` | Clone specific branch |
| `git clone --recurse-submodules <url>` | Clone with submodules |

---

## Summary

- Cloning creates a complete copy of a repository
- Use HTTPS for simple access, SSH for key-based auth
- Shallow clones save time for large repositories
- After cloning, `origin` remote is automatically configured
- For contributing to others' projects, fork first, then clone

---

**Next:** [[18 - Forking Projects]]

**Previous:** [[16 - Your First GitHub Repository]]

**Back to:** [[00 - Welcome to Git & GitHub]]
