# Remote Repositories

## What is a Remote Repository?

A **remote repository** is a version of your project hosted on a server (like GitHub, GitLab, or Bitbucket). It allows you to:

- **Backup** your code in the cloud
- **Share** your work with others
- **Collaborate** with team members
- **Deploy** from a central location

## Local vs. Remote

```
┌─────────────────────┐         ┌─────────────────────┐
│   Your Computer     │         │   Remote Server     │
│   (Local Repo)      │         │   (GitHub, etc.)    │
│                     │  push   │                     │
│   ○ ── ○ ── ○      │ ──────► │   ○ ── ○ ── ○      │
│                     │         │                     │
│                     │  pull   │                     │
│   ○ ── ○ ── ○      │ ◄────── │   ○ ── ○ ── ○      │
│                     │         │                     │
└─────────────────────┘         └─────────────────────┘
```

- **Push**: Send your commits to the remote
- **Pull**: Get commits from the remote
- **Fetch**: Download changes but don't merge them

## Viewing Remotes

### List Configured Remotes

```bash
git remote
```

Output:
```
origin
```

### See Remote URLs

```bash
git remote -v
```

Output:
```
origin  https://github.com/username/repo.git (fetch)
origin  https://github.com/username/repo.git (push)
```

### See Detailed Info

```bash
git remote show origin
```

## Adding a Remote

If you have a local repository and want to connect it to GitHub:

```bash
git remote add origin https://github.com/username/repo.git
```

- `origin` is the conventional name for your primary remote
- You can use any name, but `origin` is standard

### Using SSH Instead of HTTPS

```bash
git remote add origin git@github.com:username/repo.git
```

SSH is more secure and doesn't require entering passwords.

## Working with Remotes

### See Remote Branches

```bash
# All remote branches
git branch -r

# All branches (local and remote)
git branch -a
```

Output:
```
  origin/main
  origin/feature-login
  origin/develop
```

### Get Information About Remote

```bash
git remote show origin
```

Shows:
- Remote URL
- Tracked branches
- Local branches configured for pull/push

## Changing Remote URL

### Update the URL

```bash
git remote set-url origin https://github.com/username/new-repo.git
```

### Switch from HTTPS to SSH

```bash
git remote set-url origin git@github.com:username/repo.git
```

## Renaming a Remote

```bash
git remote rename origin upstream
```

## Removing a Remote

```bash
git remote remove origin
```

## Multiple Remotes

You can have multiple remotes. Common when:
- You fork a project and need to track the original
- You deploy to different servers
- You have mirrors of your repository

```bash
# Your fork
git remote add origin https://github.com/you/repo.git

# Original project
git remote add upstream https://github.com/original/repo.git

# Deployment server
git remote add production https://git.production.com/repo.git
```

View all:
```bash
git remote -v
```

```
origin      https://github.com/you/repo.git (fetch)
origin      https://github.com/you/repo.git (push)
upstream    https://github.com/original/repo.git (fetch)
upstream    https://github.com/original/repo.git (push)
production  https://git.production.com/repo.git (fetch)
production  https://git.production.com/repo.git (push)
```

## Remote Tracking Branches

When you clone or fetch, Git creates **remote tracking branches**:

```
origin/main       <- Tracks the remote main branch
origin/develop    <- Tracks the remote develop branch
```

These are read-only references showing where the remote branches were last time you fetched.

### View Remote Tracking Branches

```bash
git branch -r
```

### See Tracking Relationships

```bash
git branch -vv
```

Output:
```
* main    a1b2c3d [origin/main] Latest commit message
  feature b2c3d4e [origin/feature] Working on feature
```

## Setting Up Tracking

### Automatic (When Pushing)

```bash
git push -u origin main
```

The `-u` (or `--set-upstream`) creates the tracking relationship.

### Manual Setup

```bash
git branch --set-upstream-to=origin/main main
```

## Practice: Adding a Remote

```bash
# Create a local repo
mkdir remote-practice && cd remote-practice
git init
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"

# Check remotes (none yet)
git remote -v

# Add a remote (use your GitHub repo URL)
git remote add origin https://github.com/yourusername/test-repo.git

# Verify
git remote -v

# See details
git remote show origin
```

## Authentication

### HTTPS (with Credential Manager)

When using HTTPS, you'll be asked for credentials:
- Username
- Password or Personal Access Token

Git can store credentials:
```bash
# Cache for 15 minutes
git config --global credential.helper cache

# Store permanently (less secure)
git config --global credential.helper store

# Use system keychain (macOS)
git config --global credential.helper osxkeychain

# Use Windows Credential Manager
git config --global credential.helper manager
```

### SSH (Recommended)

SSH uses key pairs - more secure and convenient:

1. Generate SSH key:
   ```bash
   ssh-keygen -t ed25519 -C "your.email@example.com"
   ```

2. Add to SSH agent:
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

3. Add public key to GitHub (Settings → SSH Keys)

4. Test connection:
   ```bash
   ssh -T git@github.com
   ```

## Remote Repository Services

| Service | URL | Features |
|---------|-----|----------|
| **GitHub** | github.com | Most popular, great for open source |
| **GitLab** | gitlab.com | Built-in CI/CD, self-hosting option |
| **Bitbucket** | bitbucket.org | Atlassian integration, free private repos |
| **Azure DevOps** | dev.azure.com | Microsoft ecosystem integration |

## Quick Reference

| Command | What It Does |
|---------|--------------|
| `git remote` | List remotes |
| `git remote -v` | List remotes with URLs |
| `git remote add name url` | Add a remote |
| `git remote remove name` | Remove a remote |
| `git remote rename old new` | Rename a remote |
| `git remote set-url name url` | Change remote URL |
| `git remote show name` | Detailed remote info |
| `git branch -r` | List remote branches |
| `git branch -vv` | Show tracking branches |

---

## Summary

- Remote repositories are hosted versions of your project
- `origin` is the conventional name for your primary remote
- Use `git remote add` to connect a local repo to a remote
- You can have multiple remotes for different purposes
- HTTPS is simpler; SSH is more secure
- Remote tracking branches show the state of remote branches

---

**Next:** [[13 - Push, Pull, and Fetch]]

**Previous:** [[11 - Merge Conflicts]]

**Back to:** [[00 - Welcome to Git & GitHub]]
