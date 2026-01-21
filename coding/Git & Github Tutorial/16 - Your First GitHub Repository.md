# Your First GitHub Repository

## Two Ways to Create a Repository

1. **On GitHub** - Create on the website, then clone locally
2. **Locally first** - Create with Git, then push to GitHub

Let's cover both methods.

## Method 1: Create on GitHub (Recommended for New Projects)

### Step 1: Click "New Repository"

- Click the **+** in the top right corner
- Select **New repository**

Or go directly to: https://github.com/new

### Step 2: Configure Your Repository

Fill in the form:

**Repository name**
- Use lowercase letters, numbers, and hyphens
- Be descriptive: `my-portfolio`, `todo-app`, `learning-python`

**Description** (optional but recommended)
- Brief explanation of the project
- Shows in search results and on the repo page

**Visibility**
- **Public** - Anyone can see it
- **Private** - Only you (and collaborators) can see it

**Initialize repository**
- ✅ **Add a README file** - Good to check
- ✅ **Add .gitignore** - Select your language/framework
- ✅ **Choose a license** - MIT is a good default for open source

### Step 3: Click "Create repository"

Your repository is created! You'll see the repository page.

### Step 4: Clone to Your Computer

Copy the URL and clone:

```bash
# HTTPS
git clone https://github.com/username/repo-name.git

# SSH (if you set up SSH keys)
git clone git@github.com:username/repo-name.git

# Then enter the directory
cd repo-name
```

Now you can work locally and push changes!

## Method 2: Push an Existing Local Repository

Have code already? Push it to GitHub.

### Step 1: Create Empty Repository on GitHub

Same as above, but:
- **DON'T** check "Add a README file"
- **DON'T** add .gitignore
- **DON'T** add a license

(These would conflict with your existing files)

### Step 2: Connect and Push

GitHub shows these commands after creating an empty repo:

```bash
# Navigate to your existing project
cd my-existing-project

# Initialize if not already a Git repo
git init

# Add all files
git add .

# Create first commit (if none exist)
git commit -m "Initial commit"

# Connect to GitHub
git remote add origin https://github.com/username/repo-name.git

# Push to GitHub
git push -u origin main
```

## Understanding Repository Contents

### Required Files

**README.md**
The homepage of your repository. Include:
- Project title and description
- How to install
- How to use
- How to contribute

Example README:
```markdown
# My Awesome Project

A brief description of what this project does.

## Installation

```bash
npm install my-awesome-project
```

## Usage

```javascript
const awesome = require('my-awesome-project');
awesome.doSomething();
```

## Contributing

Pull requests welcome! See CONTRIBUTING.md for guidelines.

## License

MIT
```

**.gitignore**
Files Git should ignore. GitHub provides templates:

```
# Node.js
node_modules/
npm-debug.log

# Python
__pycache__/
*.pyc
venv/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Environment
.env
.env.local
```

**LICENSE**
Tells others how they can use your code:
- **MIT** - Do whatever, just include the license
- **Apache 2.0** - Like MIT but with patent protection
- **GPL** - Must share improvements under same license
- **No license** - All rights reserved (others can't use it)

### Optional Files

**CONTRIBUTING.md** - How others can contribute
**CODE_OF_CONDUCT.md** - Community behavior guidelines
**CHANGELOG.md** - History of changes
**.github/ISSUE_TEMPLATE/** - Templates for issues
**.github/PULL_REQUEST_TEMPLATE.md** - Template for PRs

## Repository Settings

### Basic Settings

Go to **Settings** tab:

**General**
- Rename repository
- Change visibility
- Transfer ownership
- Archive or delete

**Collaborators**
- Add people who can push to the repo

**Branches**
- Set default branch
- Add branch protection rules

### Branch Protection

Protect important branches (like main):

1. Settings → Branches → Add rule
2. Branch name pattern: `main`
3. Options:
   - ✅ Require pull request reviews
   - ✅ Require status checks
   - ✅ Include administrators

This prevents direct pushes to main—all changes must go through PRs.

## Working with Your Repository

### Basic Workflow

```bash
# 1. Pull latest changes
git pull origin main

# 2. Create a feature branch
git switch -c feature/new-feature

# 3. Make changes
echo "New content" >> README.md

# 4. Stage and commit
git add README.md
git commit -m "Update README"

# 5. Push to GitHub
git push -u origin feature/new-feature

# 6. Create Pull Request on GitHub

# 7. After PR is merged, update local main
git switch main
git pull origin main

# 8. Delete feature branch
git branch -d feature/new-feature
```

### Keeping Fork Updated

If you forked someone's repo:

```bash
# Add the original as upstream
git remote add upstream https://github.com/original/repo.git

# Fetch upstream changes
git fetch upstream

# Merge into your main
git switch main
git merge upstream/main

# Push to your fork
git push origin main
```

## Practice Exercise

Let's create your first repository:

1. **Go to GitHub** and create a new repository:
   - Name: `hello-github`
   - Description: "My first GitHub repository"
   - Public
   - ✅ Add README
   - ✅ Add .gitignore (choose: Node)
   - License: MIT

2. **Clone it locally:**
   ```bash
   git clone https://github.com/yourusername/hello-github.git
   cd hello-github
   ```

3. **Make changes:**
   ```bash
   echo "
   ## About
   This is my first repository on GitHub!
   " >> README.md
   ```

4. **Commit and push:**
   ```bash
   git add README.md
   git commit -m "Update README with about section"
   git push origin main
   ```

5. **Check GitHub** - Your changes are live!

## Quick Reference

| Action | Command/Step |
|--------|-------------|
| Create repo (web) | github.com → + → New repository |
| Clone repo | `git clone <url>` |
| Connect local to GitHub | `git remote add origin <url>` |
| First push | `git push -u origin main` |
| Regular push | `git push` |
| Pull changes | `git pull` |

---

## Summary

- Create repositories on GitHub or push existing local repos
- Always include a README.md to explain your project
- Use .gitignore to exclude files from tracking
- Choose an appropriate license for your code
- Clone to work locally, push to share changes
- Protect important branches with branch rules

---

**Next:** [[17 - Cloning Repositories]]

**Previous:** [[15 - Creating a GitHub Account]]

**Back to:** [[00 - Welcome to Git & GitHub]]
