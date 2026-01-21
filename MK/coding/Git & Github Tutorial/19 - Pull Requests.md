# Pull Requests

## What is a Pull Request?

A **Pull Request** (PR) is a way to propose changes to a repository. It:

- Shows what changes you want to make
- Allows discussion and code review
- Lets maintainers merge your changes if approved

Think of it as saying: "I've made these changes. Please review and pull them into the main project."

```
Your Branch                    Main Branch
     │                              │
     │  "Please review              │
     │   and merge my     ────────► │
     │   changes"                   │
     │                              │
```

## Creating a Pull Request

### Prerequisites

1. You've forked the repository (or have write access)
2. You've made commits on a feature branch
3. You've pushed your branch to GitHub

### Step 1: Push Your Branch

```bash
git push origin feature/my-feature
```

### Step 2: Open Pull Request on GitHub

**Option A: Banner**
After pushing, GitHub shows a banner: "Compare & pull request" - Click it!

**Option B: Manual**
1. Go to your repository on GitHub
2. Click "Pull requests" tab
3. Click "New pull request"
4. Select your branch to compare

### Step 3: Fill in PR Details

**Title**
- Clear, concise description
- Use present tense: "Add login feature" not "Added login feature"
- Reference issue if applicable: "Fix #123: Login timeout bug"

**Description**
Explain:
- What changes you made
- Why you made them
- How to test
- Screenshots if visual changes

**Example:**
```markdown
## Summary
Add user authentication with email/password login.

## Changes
- Add login form component
- Create authentication service
- Add session management
- Include form validation

## How to Test
1. Go to /login
2. Enter valid credentials
3. Verify redirect to dashboard

## Screenshots
![Login form](screenshot.png)

## Related Issues
Closes #42
```

### Step 4: Select Reviewers (If Applicable)

- Assign specific people to review
- Add labels (bug, enhancement, etc.)
- Link to project boards

### Step 5: Create Pull Request

Click "Create pull request"

## Draft Pull Requests

For work in progress:

1. When creating PR, click the dropdown on "Create pull request"
2. Select "Create draft pull request"

Draft PRs:
- Can't be merged until marked ready
- Good for getting early feedback
- Show you're working on something

To mark ready: Click "Ready for review"

## The PR Review Process

### What Happens After You Create a PR

1. **Automated checks run** (if configured)
   - Tests
   - Linting
   - Build verification

2. **Reviewers are notified**

3. **Review happens**
   - Code examined
   - Comments added
   - Questions asked

4. **You respond**
   - Answer questions
   - Make requested changes
   - Push new commits

5. **Approval or more revisions**

6. **Merge when approved**

### Responding to Review Feedback

When changes are requested:

```bash
# Make the requested changes locally
git add modified-file.js
git commit -m "Address review: improve error handling"
git push origin feature/my-feature
```

The PR automatically updates with your new commits.

## Merging Options

When a PR is approved, there are three merge options:

### 1. Merge Commit

```
Before:
main:     ○ ── ○ ── ○
feature:        ↘ ○ ── ○

After (merge commit):
main:     ○ ── ○ ── ○ ────── ●  (merge commit)
                     ↘     ↗
feature:               ○ ── ○
```

- Creates a merge commit
- Preserves complete history
- Shows when the branch was merged

### 2. Squash and Merge

```
Before:
feature: ○ ── ○ ── ○  (3 commits)

After (squash):
main:    ○ ── ○ ── ●  (1 commit combining all 3)
```

- Combines all commits into one
- Cleaner main branch history
- Loses individual commit messages

### 3. Rebase and Merge

```
Before:
main:     ○ ── ○ ── ○
feature:        ↘ ○ ── ○

After (rebase):
main:     ○ ── ○ ── ○ ── ○ ── ○
                         (replayed commits)
```

- Replays commits on top of main
- Linear history
- No merge commit

### Which to Choose?

| Method | Best For |
|--------|----------|
| **Merge** | Preserving complete history, complex features |
| **Squash** | Cleaning up messy commit history |
| **Rebase** | Keeping linear history, simple changes |

## After Merge: Cleanup

### Delete the Branch on GitHub

GitHub offers to delete the branch after merging. Click it!

### Update Your Local Repository

```bash
# Switch to main
git switch main

# Get the merged changes
git pull origin main

# Delete your local feature branch
git branch -d feature/my-feature

# Delete the remote tracking branch
git fetch --prune
```

## Handling Conflicts in PRs

If your PR shows "This branch has conflicts":

### Option 1: Resolve on GitHub (Simple Conflicts)

1. Click "Resolve conflicts"
2. Edit the file in the web editor
3. Click "Mark as resolved"
4. Click "Commit merge"

### Option 2: Resolve Locally (Complex Conflicts)

```bash
# Update main
git switch main
git pull origin main

# Go to your branch
git switch feature/my-feature

# Merge main into your branch
git merge main

# Resolve conflicts in your editor
# (Edit files, remove conflict markers)

# Complete the merge
git add .
git commit -m "Merge main and resolve conflicts"

# Push the updated branch
git push origin feature/my-feature
```

The PR automatically updates, conflicts resolved!

## PR Best Practices

### For Authors

1. **Keep PRs small** - Easier to review
2. **One thing per PR** - Don't mix unrelated changes
3. **Write good descriptions** - Help reviewers understand
4. **Test before submitting** - Don't waste reviewer time
5. **Respond promptly** - Keep momentum going

### For Reviewers

1. **Review promptly** - Don't block others
2. **Be constructive** - Suggest improvements, don't just criticize
3. **Ask questions** - If unsure, ask rather than assume
4. **Test if needed** - Pull the branch and try it
5. **Approve when satisfied** - Don't nitpick forever

## PR Templates

Create `.github/PULL_REQUEST_TEMPLATE.md`:

```markdown
## Description
<!-- What does this PR do? -->

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## How Has This Been Tested?
<!-- Describe testing performed -->

## Checklist
- [ ] My code follows the project's style guidelines
- [ ] I have performed a self-review
- [ ] I have added tests that prove my fix/feature works
- [ ] New and existing tests pass locally
- [ ] I have updated the documentation accordingly
```

## Quick Reference

| Action | How |
|--------|-----|
| Create PR | Push branch, click "Compare & pull request" |
| Update PR | Push more commits to the same branch |
| Request review | Use "Reviewers" sidebar |
| Mark ready | Click "Ready for review" |
| Resolve conflicts | Merge main into your branch |
| Close without merging | Click "Close pull request" |

---

## Summary

- Pull Requests propose changes for review before merging
- Write clear titles and descriptions
- Respond to review feedback by pushing new commits
- Choose appropriate merge strategy (merge, squash, rebase)
- Clean up branches after merging
- Use draft PRs for work in progress
- Keep PRs small and focused

---

**Next:** [[20 - Code Reviews]]

**Previous:** [[18 - Forking Projects]]

**Back to:** [[00 - Welcome to Git & GitHub]]
