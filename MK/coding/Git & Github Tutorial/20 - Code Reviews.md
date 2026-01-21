# Code Reviews

## What is a Code Review?

A **code review** is the process of examining someone's code changes before they're merged. It helps:

- Catch bugs and issues early
- Improve code quality
- Share knowledge across the team
- Ensure consistency with project standards
- Provide mentorship opportunities

## Reviewing a Pull Request

### Step 1: Open the Pull Request

On GitHub, go to the "Pull requests" tab and click on the PR.

### Step 2: Read the Description

Understand:
- What changes are being made
- Why they're being made
- How to test them

### Step 3: View the Changes

Click the "Files changed" tab to see all modified files.

```
┌─────────────────────────────────────────────────────────────────┐
│ Files changed (3)                              + 45  - 12      │
├─────────────────────────────────────────────────────────────────┤
│ ▼ src/login.js                                                  │
│   - const oldCode = "removed";                                  │
│   + const newCode = "added";                                    │
│                                                                 │
│ ▼ src/auth.js                                                   │
│   + function newFunction() {                                    │
│   +     // new code                                             │
│   + }                                                           │
└─────────────────────────────────────────────────────────────────┘
```

- **Green (+)** = Added lines
- **Red (-)** = Removed lines
- **White** = Unchanged context

### Step 4: Review View Options

**Unified View**
Shows old and new code together (default).

**Split View**
Side-by-side comparison (click "Split" button).

**Filtering**
- Show only certain file types
- Hide viewed files
- Collapse unchanged sections

## Adding Review Comments

### Single Line Comment

1. Hover over a line number
2. Click the **+** icon
3. Write your comment
4. Choose:
   - **Add single comment** - Immediate post
   - **Start a review** - Collect comments, submit together

### Multi-Line Comment

1. Click the first line number
2. Drag to last line (or hold Shift and click)
3. Write comment for the whole block

### Suggesting Changes

Propose specific code changes:

1. Click **+** on a line
2. Click the **suggestion** button (file with +/-)
3. Edit the code in the suggestion block

```suggestion
const improvedCode = "better";
```

The author can accept with one click!

## Comment Best Practices

### Be Constructive

```
❌ "This is wrong."
✅ "Consider using async/await here for better error handling."

❌ "Bad naming."
✅ "What about naming this `userAuthToken` for clarity?"

❌ "This doesn't work."
✅ "This might cause issues when X is null. Consider adding a check."
```

### Ask Questions

```
"Why did you choose this approach over X?"
"Could you explain what this function is doing?"
"Is this intentional, or should it be...?"
```

### Praise Good Work

```
"Nice refactor! This is much cleaner."
"Great test coverage!"
"I learned something new from this approach."
```

### Indicate Priority

```
🔴 BLOCKER: This will cause a security issue.
🟠 Major: This should be addressed before merge.
🟡 Minor: Nice to have, but not critical.
💬 Nit: Tiny suggestion, feel free to ignore.
❓ Question: Just curious about this approach.
```

## Submitting Your Review

After adding all comments:

1. Click **"Review changes"** button (top right)
2. Write a summary
3. Choose review type:

### Review Types

| Type | Meaning | When to Use |
|------|---------|-------------|
| **Comment** | General feedback | Questions, minor notes |
| **Approve** | Ready to merge | Looks good! |
| **Request changes** | Needs work | Must be addressed before merge |

### Example Summary Comments

**Approve:**
```
LGTM (Looks Good To Me)! Nice work on the refactor.
Just one minor suggestion on line 42, but feel free to address in a follow-up.
```

**Request changes:**
```
Great start! A few things need addressing:
1. The auth check on line 23 could be bypassed
2. Missing error handling in the API call
3. Tests needed for the new function

Happy to re-review once these are addressed!
```

## Responding to Reviews (As Author)

### Read All Comments

GitHub shows unresolved conversations. Address each one.

### Respond to Comments

Options:
- Reply with explanation
- Make the change and push
- Discuss disagreements professionally

### Make Requested Changes

```bash
# Make changes locally
git add .
git commit -m "Address review feedback"
git push origin feature-branch
```

The PR updates automatically.

### Resolve Conversations

After addressing a comment, click "Resolve conversation" to mark it done.

### Re-Request Review

If changes were requested, after addressing them:
1. Click the **🔄** icon next to the reviewer's name
2. Or @mention them in a comment

## Code Review Checklist

When reviewing, consider:

### Functionality
- [ ] Does the code do what it's supposed to?
- [ ] Are edge cases handled?
- [ ] Is error handling appropriate?

### Code Quality
- [ ] Is the code readable and maintainable?
- [ ] Are variable/function names clear?
- [ ] Is there code duplication?
- [ ] Are there any code smells?

### Testing
- [ ] Are there adequate tests?
- [ ] Do tests cover edge cases?
- [ ] Are tests meaningful (not just for coverage)?

### Security
- [ ] Is user input validated/sanitized?
- [ ] Are there potential security vulnerabilities?
- [ ] Are secrets/credentials protected?

### Performance
- [ ] Are there obvious performance issues?
- [ ] Are database queries efficient?
- [ ] Are there unnecessary operations?

### Documentation
- [ ] Are complex sections commented?
- [ ] Is the README updated if needed?
- [ ] Are API changes documented?

## Handling Disagreements

### Stay Professional

```
❌ "That's a stupid way to do it."
✅ "I'd suggest considering X because of benefits A, B, C.
    What do you think?"
```

### Explain Your Reasoning

```
"I prefer X approach because:
1. It's more readable
2. It handles edge case Y
3. It follows pattern Z we use elsewhere

But I'm open to other perspectives!"
```

### Know When to Compromise

- Not every suggestion needs to be implemented
- Focus on what truly matters
- "Agree to disagree" is okay for minor things

### Escalate if Needed

If you truly can't agree:
1. Involve a third team member
2. Check with a senior developer
3. Document the decision

## Review Culture Tips

### For Teams

- Set expectations for review turnaround time
- Rotate reviewers to share knowledge
- Make reviews a priority, not an afterthought
- Celebrate good reviews, not just fast ones

### For Individuals

- Review others' code as you'd want yours reviewed
- Learn from reviewing others' code
- Accept feedback gracefully
- Say thank you!

---

## Summary

- Code reviews improve quality and share knowledge
- Be constructive and respectful in comments
- Use suggestions for specific changes
- Indicate priority/severity of issues
- Authors should address all feedback
- Approve, request changes, or just comment
- Professional disagreement is okay

---

**Next:** [[21 - GitHub Issues]]

**Previous:** [[19 - Pull Requests]]

**Back to:** [[00 - Welcome to Git & GitHub]]
