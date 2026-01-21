# What is Version Control?

## The Problem: Managing Changes

Imagine you're writing a document or building a project. You might find yourself:

- Saving files like `report_v1.docx`, `report_v2.docx`, `report_final.docx`, `report_final_FINAL.docx`
- Losing track of what changed between versions
- Accidentally overwriting work you wanted to keep
- Struggling to collaborate with others who are editing the same files
- Having no way to go back if something breaks

**Sound familiar?** This is exactly the problem version control solves.

## What is Version Control?

**Version control** (also called **source control**) is a system that records changes to files over time so you can:

1. **Track every change** - See exactly what changed, when, and by whom
2. **Go back in time** - Restore any previous version of your project
3. **Work safely** - Experiment without fear of losing your work
4. **Collaborate** - Multiple people can work on the same project simultaneously
5. **Understand history** - Know why changes were made

## A Simple Analogy

Think of version control like a **detailed save game system** for your work:

- Every time you save, it creates a snapshot of your entire project
- You can have unlimited save slots (not just "Save 1", "Save 2", "Save 3")
- Each save includes notes about what you did
- You can jump back to any previous save at any time
- Multiple players can work on different parts and merge their progress

## Types of Version Control

### 1. Local Version Control
- Saves versions on your own computer only
- Simple but risky (if your computer dies, everything is lost)
- Example: Making copies of folders manually

### 2. Centralized Version Control
- One central server holds all versions
- Everyone connects to this server
- Examples: SVN, Perforce
- Problem: If the server goes down, no one can work

### 3. Distributed Version Control (What Git Uses)
- Everyone has a complete copy of the entire history
- Can work offline
- No single point of failure
- Examples: **Git**, Mercurial

```
Centralized:                    Distributed (Git):

    [Server]                    [Server/GitHub]
    /  |  \                      /     |     \
   /   |   \                    /      |      \
[Dev1][Dev2][Dev3]          [Dev1]  [Dev2]  [Dev3]
                            (full   (full   (full
                            copy)   copy)   copy)
```

## What is Git?

**Git** is the most popular version control system in the world. Created in 2005 by Linus Torvalds (the creator of Linux), Git is:

- **Free and open source**
- **Distributed** - Everyone has the full history
- **Fast** - Operations are nearly instantaneous
- **Reliable** - Your data is safe and recoverable
- **Flexible** - Works for any type of project

> [!info] Fun Fact
> The name "Git" is British slang for a silly or unpleasant person. Linus Torvalds said he named it after himself!

## What is GitHub?

**GitHub** is a website/service that hosts Git repositories online. Think of it as:

- **Cloud storage for Git projects**
- **Social network for developers**
- **Collaboration platform for teams**

```
Git = The version control tool (runs on your computer)
GitHub = A website to share and collaborate on Git projects
```

Other similar services include GitLab, Bitbucket, and Azure DevOps.

## Key Concepts Preview

Here are terms you'll learn about:

| Term | Simple Definition |
|------|------------------|
| **Repository (Repo)** | A folder tracked by Git |
| **Commit** | A saved snapshot of your project |
| **Branch** | A parallel version of your project |
| **Clone** | Copy a repository to your computer |
| **Push** | Send your commits to a remote server |
| **Pull** | Get commits from a remote server |
| **Merge** | Combine changes from different branches |

Don't worry about memorizing these now—we'll explore each one in detail!

## Why Learn Git?

### For Individual Developers
- Never lose work again
- Experiment freely with a safety net
- Track what you changed and why
- Show your work history to employers

### For Teams
- Multiple people can work simultaneously
- Review each other's code before merging
- Track who made what changes
- Maintain different versions (development, production)

### For Your Career
- **Git is essential** - Nearly every development job requires it
- **GitHub is your portfolio** - Employers often check GitHub profiles
- **Open source** - Contribute to projects used by millions

## Real-World Example

Let's see how Git helps in practice:

**Without Git:**
```
project/
├── index_old.html
├── index_backup.html
├── index_v2.html
├── index_FINAL.html
├── index_FINAL2.html
└── index_DONT_DELETE.html
```

**With Git:**
```
project/
└── index.html

Git history:
• 2 hours ago: "Add contact form"
• Yesterday: "Update navigation menu"
• 3 days ago: "Fix mobile layout"
• 1 week ago: "Initial homepage design"
• 2 weeks ago: "Project created"

(You can restore ANY of these versions with one command!)
```

## Summary

- **Version control** tracks changes to files over time
- **Git** is the most popular version control system
- **GitHub** is a platform for hosting Git repositories online
- Git lets you save snapshots, go back in time, and collaborate
- Learning Git is essential for modern software development

---

## What's Next?

Now that you understand what version control is and why it matters, let's get Git installed on your computer!

**Next:** [[02 - Installing Git]]

**Back to:** [[00 - Welcome to Git & GitHub]]
