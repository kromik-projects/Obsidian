# Introduction to GitHub

## What is GitHub?

**GitHub** is a web platform for hosting Git repositories. Think of it as:

- **Cloud storage** for your Git projects
- **Social network** for developers
- **Collaboration platform** for teams
- **Portfolio** showcasing your work

While Git is the version control tool that runs on your computer, GitHub is a service that hosts your Git repositories online.

## Git vs. GitHub

| Git | GitHub |
|-----|--------|
| Version control software | Web hosting platform |
| Runs on your computer | Runs in the cloud |
| Command-line tool | Website with GUI |
| Free, open source | Free tier + paid plans |
| Created by Linus Torvalds | Created by Tom Preston-Werner |
| Works offline | Requires internet |

You can use Git without GitHub, but GitHub requires Git.

## Key GitHub Features

### 1. Repository Hosting

Store your projects online:
- Public repositories (free, visible to everyone)
- Private repositories (free, only you/team can see)
- Unlimited repositories on free plan

### 2. Collaboration Tools

**Pull Requests**
- Propose changes to a repository
- Review code before merging
- Discuss improvements
- Track change history

**Issues**
- Report bugs
- Request features
- Track tasks
- Discuss problems

**Discussions**
- Community Q&A
- Announcements
- General conversation

### 3. Project Management

**Projects**
- Kanban-style boards
- Track work progress
- Link to issues and PRs

**Milestones**
- Group issues by goal
- Track progress toward releases

### 4. Documentation

**README**
- First thing visitors see
- Explain your project
- Installation instructions

**Wiki**
- Extended documentation
- Multiple pages
- Collaborative editing

**GitHub Pages**
- Host static websites
- Free hosting
- Custom domains

### 5. Automation

**GitHub Actions**
- Automate workflows
- Run tests on every push
- Deploy automatically
- Free for public repos

### 6. Security

**Dependabot**
- Automatic dependency updates
- Security vulnerability alerts

**Code Scanning**
- Find security issues in code
- Automated analysis

## GitHub Interface Overview

### Repository Page

```
┌────────────────────────────────────────────────────────────────┐
│  username / repository-name            ⭐ Star   👁 Watch   🍴 Fork │
├────────────────────────────────────────────────────────────────┤
│  📁 Code  │ 🔀 Pull requests  │ ⚡ Actions  │ 📋 Projects  │ 🔒 Security │
├────────────────────────────────────────────────────────────────┤
│                                                                │
│  📂 src/                                                       │
│  📂 tests/                                                     │
│  📄 .gitignore                                                 │
│  📄 README.md                                                  │
│  📄 package.json                                               │
│                                                                │
├────────────────────────────────────────────────────────────────┤
│  README.md                                                     │
│  ═══════════                                                   │
│  # Project Name                                                │
│  Description of your project...                                │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

### Key Areas

| Tab | Purpose |
|-----|---------|
| **Code** | Browse files, view commits |
| **Issues** | Bug reports, feature requests |
| **Pull requests** | Proposed changes to review |
| **Actions** | Automated workflows |
| **Projects** | Task management boards |
| **Wiki** | Documentation pages |
| **Security** | Vulnerability alerts |
| **Insights** | Repository statistics |
| **Settings** | Configuration options |

## GitHub Vocabulary

| Term | Definition |
|------|------------|
| **Repository (Repo)** | A project folder with Git history |
| **Star** | Bookmark a repo you like |
| **Fork** | Copy someone's repo to your account |
| **Clone** | Download a repo to your computer |
| **Pull Request (PR)** | Request to merge your changes |
| **Issue** | A task, bug, or discussion topic |
| **Gist** | Share code snippets |
| **Organization** | Group account for teams |
| **README** | Project description file |

## GitHub Profile

Your profile shows:
- Bio and information
- Pinned repositories
- Contribution graph ("green squares")
- Recent activity
- Organizations you belong to

```
┌──────────────────────────────────────────────────┐
│  👤 Your Name                                    │
│  @username                                       │
│  "Your bio goes here"                            │
│                                                  │
│  📍 Location   🔗 Website   🐦 Twitter           │
│                                                  │
│  ├── Repositories: 42                            │
│  ├── Stars: 156                                  │
│  └── Followers: 89                               │
│                                                  │
│  📌 Pinned Repositories                          │
│  ┌─────────────────────────────────────┐        │
│  │ awesome-project ⭐ 234              │        │
│  │ My best project description          │        │
│  └─────────────────────────────────────┘        │
│                                                  │
│  📊 Contribution Graph                           │
│  [████ ██ ████████ ███ ██████████]              │
│                                                  │
└──────────────────────────────────────────────────┘
```

## Open Source on GitHub

GitHub hosts millions of open source projects:

- **View code** - Learn from others
- **Report issues** - Help improve projects
- **Contribute** - Submit bug fixes and features
- **Fork** - Build on existing projects

### Popular Open Source Projects on GitHub

- **Linux** - The Linux kernel
- **React** - Facebook's UI library
- **VS Code** - Microsoft's code editor
- **TensorFlow** - Google's ML library
- **Node.js** - JavaScript runtime

## GitHub for Your Career

### Portfolio

Your GitHub profile is like a resume:
- Shows real code you've written
- Demonstrates your skills
- Proves you can collaborate

### Employers Check GitHub

Many companies:
- Look at your contribution history
- Review your code quality
- Check if you contribute to open source

### Tips for a Good Profile

1. **Complete your profile** - Photo, bio, location
2. **Pin best repositories** - Show your best work
3. **Write good READMEs** - Explain your projects
4. **Contribute regularly** - Keep the graph green
5. **Contribute to open source** - Shows collaboration skills

## GitHub Pricing

| Plan | Cost | Features |
|------|------|----------|
| **Free** | $0 | Unlimited repos, basic features |
| **Pro** | $4/month | Advanced features, more storage |
| **Team** | $4/user/month | Team management, org features |
| **Enterprise** | Custom | SAML SSO, advanced security |

For learning and personal projects, **Free is plenty!**

## Alternatives to GitHub

| Platform | Strengths |
|----------|-----------|
| **GitLab** | Built-in CI/CD, self-hosting |
| **Bitbucket** | Atlassian integration (Jira) |
| **Azure DevOps** | Microsoft ecosystem |
| **Gitea** | Self-hosted, lightweight |
| **SourceForge** | Classic, still around |

GitHub is the most popular and has the largest community.

## Getting Started

Ready to create your GitHub account? Continue to:

[[15 - Creating a GitHub Account]]

## Summary

- GitHub hosts Git repositories in the cloud
- It provides collaboration tools like PRs and Issues
- Free for public and private repositories
- Your GitHub profile serves as a developer portfolio
- GitHub is where most open source projects live
- It's the industry standard for code hosting

---

**Next:** [[15 - Creating a GitHub Account]]

**Previous:** [[13 - Push, Pull, and Fetch]]

**Back to:** [[00 - Welcome to Git & GitHub]]
