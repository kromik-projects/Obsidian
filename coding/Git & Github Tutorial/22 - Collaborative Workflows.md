# Collaborative Workflows

## Overview

When teams use Git, they need a shared strategy for how code flows from development to production. This lesson covers common team workflows.

## Workflow Types

### 1. Centralized Workflow

The simplest workflow—everyone pushes to main.

```
Developer A ──┐
              │
Developer B ──┼──► main
              │
Developer C ──┘
```

**How It Works:**
```bash
# Everyone works on main
git pull origin main
# Make changes
git add .
git commit -m "My changes"
git push origin main
```

**Pros:**
- Simple to understand
- Good for small teams
- Low overhead

**Cons:**
- No code review
- Easy to break main
- Hard to work on multiple features

**Best For:** Solo projects, very small teams, simple projects

---

### 2. Feature Branch Workflow

Each feature gets its own branch. Most popular workflow.

```
main:     ○ ─────────────────────── ● (merge)
               ↘                  ↗
feature:         ○ ── ○ ── ○ ── ○
```

**How It Works:**
```bash
# Create feature branch
git switch -c feature/user-auth

# Work on feature
git add .
git commit -m "Add login form"
git push origin feature/user-auth

# Create PR, get review, merge
# Then update local main
git switch main
git pull origin main
```

**Rules:**
- Never commit directly to main
- All changes go through pull requests
- Delete branches after merging

**Pros:**
- Enables code review
- Isolated development
- Main stays stable

**Cons:**
- Slight overhead for small changes
- Branches can get stale

**Best For:** Most teams, any project size

---

### 3. Gitflow Workflow

A strict workflow with designated branch types.

```
main:    ○ ─────────────────────────────● (release)
                                       ↗
release:                    ○ ── ○ ── ○
                           ↗
develop: ○ ── ○ ── ○ ── ○ ── ○ ── ○ ── ○
              ↘    ↗    ↘    ↗
features:       ○ ── ○    ○ ── ○
```

**Branch Types:**

| Branch | Purpose | Merges From | Merges To |
|--------|---------|-------------|-----------|
| `main` | Production code | release, hotfix | - |
| `develop` | Integration | feature, release | release |
| `feature/*` | New features | develop | develop |
| `release/*` | Release prep | develop | main, develop |
| `hotfix/*` | Emergency fixes | main | main, develop |

**Flow:**
1. Create `feature/x` from `develop`
2. Merge feature into `develop`
3. Create `release/1.0` from `develop`
4. Test and fix in release branch
5. Merge release into `main` AND `develop`
6. Tag `main` with version

**Pros:**
- Very organized
- Clear release process
- Supports parallel releases

**Cons:**
- Complex
- Overhead for small teams
- Long-lived branches can diverge

**Best For:** Large projects, teams with scheduled releases

---

### 4. GitHub Flow

Simplified workflow GitHub uses and recommends.

```
main:     ○ ────────── ● ────────── ● ────────── ●
               ↘    ↗       ↘    ↗       ↘    ↗
branches:        ○ ── ○       ○            ○ ── ○
```

**Rules:**
1. `main` is always deployable
2. Create descriptive branch from main
3. Push to branch regularly
4. Open PR when ready for review
5. Merge only after approval
6. Deploy immediately after merge

**How It Works:**
```bash
# Always start from updated main
git switch main
git pull origin main

# Create a branch
git switch -c add-search-feature

# Make changes, commit often
git add .
git commit -m "Add search UI"
git push origin add-search-feature

# Open PR on GitHub
# Get reviewed
# Merge
# Deploy
```

**Pros:**
- Simple, low overhead
- Continuous deployment
- Fast feedback

**Cons:**
- Assumes robust testing/CI
- No staging for complex releases

**Best For:** Web apps, continuous deployment, SaaS

---

### 5. Forking Workflow

Each developer has their own server-side repository.

```
Original Repo (upstream)
     ↑
     │ Pull Requests
     │
├────┼────┬────────┐
│    │    │        │
Dev A's  Dev B's  Dev C's
Fork     Fork     Fork
```

**How It Works:**
```bash
# Fork on GitHub
# Clone YOUR fork
git clone git@github.com:you/project.git

# Add upstream
git remote add upstream git@github.com:original/project.git

# Work on branch
git switch -c my-feature
# Make changes
git push origin my-feature

# Create PR from your fork to upstream
```

**Pros:**
- No write access needed to original
- Perfect for open source
- Clear ownership

**Cons:**
- More complex setup
- Must keep fork updated

**Best For:** Open source, untrusted contributors

---

## Choosing a Workflow

| Workflow | Team Size | Release Style | Complexity |
|----------|-----------|---------------|------------|
| Centralized | 1-3 | Any | Very Low |
| Feature Branch | 2-10 | Any | Low |
| GitHub Flow | 2-20 | Continuous | Low |
| Gitflow | 5+ | Scheduled | High |
| Forking | Any | Any | Medium |

### Questions to Ask

1. **How often do you release?**
   - Continuous → GitHub Flow
   - Scheduled → Gitflow

2. **How big is your team?**
   - Small → Feature Branch or GitHub Flow
   - Large → Gitflow or structured approach

3. **Is it open source?**
   - Yes → Forking Workflow

4. **How critical is stability?**
   - Very critical → Gitflow
   - Fast iteration → GitHub Flow

## Branch Protection

Regardless of workflow, protect important branches:

### Setup in GitHub

1. Settings → Branches → Add rule
2. Branch name: `main`
3. Enable:
   - ✅ Require pull request reviews
   - ✅ Require status checks
   - ✅ Require branches be up to date
   - ✅ Include administrators

### Common Rules

| Rule | Purpose |
|------|---------|
| Require PR reviews | Ensure code is reviewed |
| Require status checks | Tests must pass |
| Require up-to-date | Branch must be current |
| Restrict pushes | Only certain people can push |
| Require signed commits | Verify commit author |

## Continuous Integration (CI)

Automate testing with every push:

### GitHub Actions Example

`.github/workflows/ci.yml`:
```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm install
      - run: npm test
```

This runs tests on every PR and push to main.

## Team Communication

### During Development

```bash
# Good commit messages
git commit -m "Add user authentication

- Implement login/logout
- Add session management
- Create auth middleware

Closes #42"
```

### In Pull Requests

- Link related issues
- Describe what changed and why
- Tag relevant reviewers
- Respond to feedback promptly

### Branch Naming Convention

```
feature/add-user-auth
bugfix/login-timeout
hotfix/security-patch
docs/update-readme
refactor/database-layer
```

---

## Summary

- Choose a workflow that fits your team size and release style
- Feature Branch and GitHub Flow work for most teams
- Gitflow adds structure for scheduled releases
- Forking Workflow is ideal for open source
- Protect important branches with rules
- Use CI to automate testing
- Communicate clearly in commits and PRs

---

**Next:** [[23 - Git Commands Cheatsheet]]

**Previous:** [[21 - GitHub Issues]]

**Back to:** [[00 - Welcome to Git & GitHub]]
