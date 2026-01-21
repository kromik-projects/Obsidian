# Glossary

A comprehensive list of Git and GitHub terminology.

---

## A

### Add
The `git add` command stages changes for the next commit. It tells Git which changes you want to include.

### Amend
Modify the most recent commit. Used to fix commit messages or add forgotten files.
```bash
git commit --amend
```

---

## B

### Bare Repository
A repository without a working directory, containing only the `.git` folder. Used for sharing (like on servers).

### Blame
Show who last modified each line of a file.
```bash
git blame filename
```

### Branch
An independent line of development. Branches allow you to work on features without affecting the main code.

### Branch Protection
Rules that prevent direct pushes to important branches, requiring pull requests and reviews.

---

## C

### Checkout
Switch branches or restore files. Being replaced by `git switch` and `git restore`.
```bash
git checkout branch-name
git checkout -- filename  # restore file
```

### Cherry-Pick
Apply a specific commit from one branch to another.
```bash
git cherry-pick <commit-hash>
```

### Clone
Create a local copy of a remote repository.
```bash
git clone <url>
```

### Collaborator
Someone with write access to a repository.

### Commit
A snapshot of your project at a point in time. Includes all staged changes, a message, author info, and timestamp.

### Commit Hash (SHA)
A unique 40-character identifier for each commit (e.g., `a1b2c3d4e5f6...`). Short form uses first 7 characters.

### Conflict
When Git cannot automatically merge changes because the same lines were modified differently in two branches.

### Contributor
Someone who has made contributions to a project (commits, issues, PRs).

---

## D

### Detached HEAD
When HEAD points directly to a commit instead of a branch. Changes won't belong to any branch.

### Diff
The difference between two versions. Shows added, removed, and modified lines.
```bash
git diff
```

### Distributed Version Control
A version control system where every user has a complete copy of the repository, including full history. Git is distributed.

---

## F

### Fast-Forward
A merge where the target branch can simply move forward to include the source branch because no divergent commits exist.

### Fetch
Download commits and refs from a remote without merging.
```bash
git fetch origin
```

### Fork
A personal copy of someone else's repository on GitHub. Used for contributing to projects you don't have write access to.

---

## G

### Git
A distributed version control system created by Linus Torvalds in 2005.

### GitHub
A web platform for hosting Git repositories, with collaboration features like pull requests, issues, and actions.

### .gitignore
A file specifying which files Git should ignore and not track.

### Gitflow
A branching workflow with specific branch types (main, develop, feature, release, hotfix).

---

## H

### HEAD
A pointer to the current commit (usually the tip of the current branch). Represented in commands as `HEAD`.

### Hook
A script that runs automatically at certain Git events (pre-commit, post-push, etc.).

### Hotfix
An urgent fix applied directly to production, typically on its own branch.

---

## I

### Index
Another name for the staging area. The set of changes ready to be committed.

### Initialize (Init)
Create a new Git repository in a directory.
```bash
git init
```

### Issue
A GitHub feature for tracking bugs, feature requests, tasks, or discussions.

---

## L

### Local
Your computer, as opposed to a remote server. Your local repository is your working copy.

### Log
View the commit history.
```bash
git log
```

---

## M

### Main (Master)
The default primary branch. `main` is now the preferred name (previously `master`).

### Markdown
A text formatting syntax used in README files, issues, and PRs. `.md` files.

### Merge
Combine changes from one branch into another.
```bash
git merge branch-name
```

### Merge Commit
A commit created when merging two branches that have diverged.

### Milestone
A GitHub feature for grouping issues toward a goal or release.

---

## O

### Origin
The conventional name for the primary remote repository. Usually where you cloned from.

### Orphan Branch
A branch with no commit history, starting completely fresh.

---

## P

### Patch
A file containing changes that can be applied to another repository.

### Personal Access Token (PAT)
A token used instead of a password for GitHub authentication, especially with HTTPS.

### Pull
Fetch and merge remote changes in one step.
```bash
git pull origin main
```

### Pull Request (PR)
A GitHub feature for proposing changes. Allows review and discussion before merging.

### Push
Upload local commits to a remote repository.
```bash
git push origin main
```

---

## R

### README
A file (usually `README.md`) that explains a project. Displayed on the repository homepage.

### Rebase
Reapply commits on top of another base. Creates linear history.
```bash
git rebase main
```

### Reflog
A log of all reference updates (branch changes, resets). Useful for recovery.
```bash
git reflog
```

### Remote
A version of your repository hosted elsewhere (e.g., GitHub).

### Repository (Repo)
A folder tracked by Git, containing your project files and the `.git` directory with all history.

### Reset
Move HEAD and optionally change staging area and working directory.
```bash
git reset --soft HEAD~1   # undo commit, keep changes staged
git reset --hard HEAD~1   # undo commit, discard changes
```

### Restore
Discard changes or unstage files (newer alternative to checkout for files).
```bash
git restore filename
git restore --staged filename
```

### Revert
Create a new commit that undoes a previous commit. Safe for pushed commits.
```bash
git revert <commit-hash>
```

### Review
Examining code changes, typically in a pull request, before merging.

---

## S

### SHA
Secure Hash Algorithm. The method Git uses to create commit identifiers.

### Shallow Clone
A clone with limited history (e.g., only the most recent commit).
```bash
git clone --depth 1 <url>
```

### Squash
Combine multiple commits into a single commit.

### SSH Key
A cryptographic key pair used for secure authentication with remote repositories.

### Stage
Add changes to the staging area in preparation for a commit.
```bash
git add filename
```

### Staging Area (Index)
A preparation area where you collect changes before committing.

### Stash
Temporarily save uncommitted changes to work on something else.
```bash
git stash
git stash pop
```

### Status
Show the current state of the working directory and staging area.
```bash
git status
```

### Switch
Change branches (newer alternative to checkout for branches).
```bash
git switch branch-name
git switch -c new-branch  # create and switch
```

---

## T

### Tag
A named reference to a specific commit, often used for release versions.
```bash
git tag v1.0.0
```

### Three-Way Merge
A merge that creates a merge commit because both branches have new commits.

### Tracked Files
Files that Git is monitoring for changes.

### Tree
Git's representation of a directory structure.

---

## U

### Unstage
Remove files from the staging area (but keep changes in working directory).
```bash
git restore --staged filename
```

### Untracked Files
Files in your working directory that Git isn't monitoring.

### Upstream
1. The original repository that a fork was created from
2. The remote branch that a local branch tracks

---

## V

### Version Control
A system for tracking changes to files over time, allowing you to revisit previous versions.

---

## W

### Working Directory
The actual files you see and edit in your project folder, as opposed to what's in staging or committed.

### Working Tree
Another term for working directory.

### Workflow
A strategy for how a team uses branches and manages code changes.

---

## Visual Summary

```
┌─────────────────────────────────────────────────────────────────┐
│                         REMOTE                                   │
│                      (origin/GitHub)                             │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Commits  ←── Push ─── │ ─── Fetch/Pull ──→  Commits    │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ↓
┌─────────────────────────────────────────────────────────────────┐
│                          LOCAL                                   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                    Repository (.git)                       │   │
│  │  ○ ── ○ ── ○ ── ○ ── ○  (commit history)                 │   │
│  │        ↑                                                    │   │
│  │     Commit                                                  │   │
│  └────────┬─────────────────────────────────────────────────┘   │
│           │                                                      │
│  ┌────────┴─────────────────────────────────────────────────┐   │
│  │              Staging Area (Index)                          │   │
│  │  [file1.txt] [file2.txt]  (ready to commit)               │   │
│  │        ↑                                                    │   │
│  │       Add                                                   │   │
│  └────────┬─────────────────────────────────────────────────┘   │
│           │                                                      │
│  ┌────────┴─────────────────────────────────────────────────┐   │
│  │              Working Directory                              │   │
│  │  file1.txt  file2.txt  file3.txt  (your actual files)     │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

**Previous:** [[24 - Common Problems and Solutions]]

**Back to:** [[00 - Welcome to Git & GitHub]]

---

> [!success] Congratulations!
> You've completed the Git & GitHub tutorial series! Practice these concepts regularly, and they'll become second nature.
