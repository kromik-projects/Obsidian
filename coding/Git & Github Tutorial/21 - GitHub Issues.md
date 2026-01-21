# GitHub Issues

## What are Issues?

**Issues** are GitHub's built-in tracking system for:

- 🐛 **Bug reports** - Something is broken
- ✨ **Feature requests** - Something new wanted
- 📋 **Tasks** - Things to do
- ❓ **Questions** - Need help or clarification
- 💬 **Discussions** - General conversation

Think of issues as a to-do list and conversation hub for your project.

## Creating an Issue

### Step 1: Go to Issues Tab

Click "Issues" on the repository page.

### Step 2: Click "New Issue"

If the repo has templates, choose one. Otherwise, start blank.

### Step 3: Write a Good Issue

**Title**
- Clear and specific
- Summarize the problem/request

**Description**
Depends on issue type:

**Bug Report:**
```markdown
## Description
Brief description of the bug.

## Steps to Reproduce
1. Go to...
2. Click on...
3. See error

## Expected Behavior
What should happen.

## Actual Behavior
What actually happens.

## Screenshots
If applicable, add screenshots.

## Environment
- OS: Windows 11
- Browser: Chrome 120
- Version: v1.2.3
```

**Feature Request:**
```markdown
## Is this related to a problem?
A clear description of the problem. Ex: I'm frustrated when...

## Proposed Solution
What you'd like to happen.

## Alternatives Considered
Other solutions you've thought about.

## Additional Context
Any other context or screenshots.
```

### Step 4: Add Metadata (Optional)

On the right sidebar:
- **Assignees** - Who should work on this
- **Labels** - Categorize the issue
- **Projects** - Link to project board
- **Milestone** - Group with a release/goal

### Step 5: Submit

Click "Submit new issue"

## Issue Labels

Labels categorize and prioritize issues.

### Default Labels

| Label | Use For |
|-------|---------|
| `bug` | Something isn't working |
| `documentation` | Docs need improvement |
| `duplicate` | Already exists |
| `enhancement` | New feature |
| `good first issue` | Beginner-friendly |
| `help wanted` | Extra attention needed |
| `invalid` | Not valid |
| `question` | Needs more info |
| `wontfix` | Won't be worked on |

### Custom Labels

Create your own:
1. Go to Issues → Labels
2. Click "New label"
3. Name, description, color

**Common Custom Labels:**
```
priority: high     (red)
priority: medium   (yellow)
priority: low      (green)
status: in progress
status: blocked
area: frontend
area: backend
type: security
```

## Working with Issues

### Referencing Issues

Use `#` followed by issue number:

```markdown
This relates to #42
See issue #123 for context
```

GitHub automatically links them.

### Referencing in Commits

```bash
git commit -m "Fix login bug

Fixes #42"
```

Keywords that auto-close issues:
- `Closes #42`
- `Fixes #42`
- `Resolves #42`

### Cross-Repository References

```markdown
owner/repo#42
```

### Mentioning Users

```markdown
@username can you look at this?
```

They'll be notified.

## Issue Templates

Create `.github/ISSUE_TEMPLATE/`:

**Bug Report Template** (`bug_report.md`):
```markdown
---
name: Bug Report
about: Create a report to help us improve
title: '[BUG] '
labels: bug
assignees: ''
---

## Description
A clear description of the bug.

## Steps To Reproduce
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

## Expected Behavior
What you expected to happen.

## Screenshots
If applicable, add screenshots.

## Environment
- OS: [e.g., Windows 11]
- Browser: [e.g., Chrome 120]
- Version: [e.g., 1.2.3]
```

**Feature Request Template** (`feature_request.md`):
```markdown
---
name: Feature Request
about: Suggest an idea for this project
title: '[FEATURE] '
labels: enhancement
assignees: ''
---

## Problem
Is your feature request related to a problem?

## Proposed Solution
Describe the solution you'd like.

## Alternatives
Describe alternatives you've considered.

## Additional Context
Add any other context or screenshots.
```

## Issue Management

### Filtering Issues

```
is:issue is:open label:bug
is:issue is:closed author:username
is:issue assignee:username
is:issue milestone:"v1.0"
```

### Sorting

- Newest / Oldest
- Most commented
- Recently updated

### Pinning Issues

Important issues can be pinned (up to 3) to stay at the top.

### Locking Issues

Prevent further comments on resolved/heated issues.

### Transferring Issues

Move an issue to a different repository.

## Milestones

Group issues by goal or release:

1. Go to Issues → Milestones
2. Create milestone (e.g., "v1.0 Release")
3. Set due date (optional)
4. Assign issues to milestone

Track progress:
```
v1.0 Release
████████░░░░░░░░ 50% complete
4 open, 4 closed
Due: January 31
```

## Projects Integration

Link issues to project boards:

1. Create a Project (repo or org level)
2. Add issues to the project
3. Move through columns (To Do → In Progress → Done)

## Issue Best Practices

### For Reporters

1. **Search first** - Avoid duplicates
2. **Be specific** - Vague issues are hard to address
3. **Include details** - Environment, steps, screenshots
4. **One issue per issue** - Don't bundle multiple problems
5. **Be patient** - Maintainers are often volunteers

### For Maintainers

1. **Respond promptly** - Even just to acknowledge
2. **Label appropriately** - Helps organize and prioritize
3. **Ask for details** - If something's unclear
4. **Close stale issues** - Keep the list manageable
5. **Thank contributors** - Encourage participation

### Stale Issue Management

Use stale bot or GitHub Actions to:
- Label old issues as "stale"
- Comment asking for updates
- Close if no response

## Quick Reference

| Action | How |
|--------|-----|
| Create issue | Issues → New Issue |
| Reference issue | `#42` |
| Close via commit | `Fixes #42` in commit message |
| Assign user | Sidebar → Assignees |
| Add label | Sidebar → Labels |
| Filter issues | Use search syntax |
| Create template | `.github/ISSUE_TEMPLATE/` |

---

## Summary

- Issues track bugs, features, tasks, and discussions
- Use labels to categorize and prioritize
- Reference issues in commits and PRs with #number
- Auto-close issues with keywords (Fixes, Closes, Resolves)
- Create templates for consistent issue reporting
- Use milestones to group issues by release/goal
- Link issues to project boards for workflow tracking

---

**Next:** [[22 - Collaborative Workflows]]

**Previous:** [[20 - Code Reviews]]

**Back to:** [[00 - Welcome to Git & GitHub]]
