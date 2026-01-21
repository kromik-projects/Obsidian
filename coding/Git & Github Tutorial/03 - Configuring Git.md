# Configuring Git

## Why Configure Git?

Before you start using Git, you need to tell it who you are. Every time you save changes (called a "commit"), Git records:

- **Your name** - Who made the change
- **Your email** - How to contact you

This information is attached to every commit you make and is visible to anyone who views the project history.

## Configuration Levels

Git has three levels of configuration:

| Level | Scope | File Location | Command Flag |
|-------|-------|---------------|--------------|
| **System** | All users on computer | `/etc/gitconfig` | `--system` |
| **Global** | Your user account | `~/.gitconfig` | `--global` |
| **Local** | Single repository | `.git/config` | `--local` |

**Most common:** You'll use `--global` for most settings (applies to all your projects).

Local settings override global, and global overrides system.

## Essential Configuration

### Setting Your Identity

Open your terminal and run these commands (replace with your actual name and email):

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

> [!important] Use Your Real Info
> Use the same email you'll use for GitHub! This connects your commits to your GitHub account.

**Examples:**
```bash
git config --global user.name "Alice Johnson"
git config --global user.email "alice@example.com"
```

### Verify Your Settings

Check what you've configured:

```bash
# View specific settings
git config user.name
git config user.email

# View all global settings
git config --global --list

# View all settings (all levels)
git config --list
```

## Setting Your Default Editor

When Git needs you to write a message (like for commits), it opens a text editor. By default, this is often Vim, which can be confusing for beginners.

### Choose Your Editor

```bash
# Visual Studio Code (recommended)
git config --global core.editor "code --wait"

# Sublime Text
git config --global core.editor "subl -n -w"

# Atom
git config --global core.editor "atom --wait"

# Notepad++ (Windows)
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

# nano (simple terminal editor)
git config --global core.editor "nano"

# Vim (for advanced users)
git config --global core.editor "vim"
```

> [!tip] VS Code Users
> Make sure VS Code is in your PATH. On macOS, open VS Code and press `Cmd+Shift+P`, then search for "Shell Command: Install 'code' command in PATH"

## Setting the Default Branch Name

Historically, Git used `master` as the default branch name. The industry has moved to using `main`. Set this for new repositories:

```bash
git config --global init.defaultBranch main
```

## Useful Additional Settings

### Line Ending Configuration

Different operating systems handle line endings differently. This prevents issues:

**Windows:**
```bash
git config --global core.autocrlf true
```

**macOS/Linux:**
```bash
git config --global core.autocrlf input
```

### Colorful Output

Make Git output easier to read (usually enabled by default):

```bash
git config --global color.ui auto
```

### Set Default Pull Behavior

When pulling changes, tell Git how to handle merging:

```bash
# Recommended for beginners
git config --global pull.rebase false
```

### Enable Helpful Aliases

Create shortcuts for common commands:

```bash
# Shorter status
git config --global alias.st status

# Shorter commit
git config --global alias.ci commit

# Shorter checkout
git config --global alias.co checkout

# Shorter branch
git config --global alias.br branch

# Pretty log
git config --global alias.lg "log --oneline --graph --decorate"

# Show last commit
git config --global alias.last "log -1 HEAD"
```

Now you can use:
```bash
git st          # instead of: git status
git ci -m "msg" # instead of: git commit -m "msg"
git co main     # instead of: git checkout main
git lg          # pretty log view
```

## Viewing and Editing Configuration

### View All Settings

```bash
# All settings with their sources
git config --list --show-origin

# Just global settings
git config --global --list
```

### Edit Configuration File Directly

```bash
# Open global config in your editor
git config --global --edit
```

This opens a file that looks like:

```ini
[user]
    name = Alice Johnson
    email = alice@example.com

[core]
    editor = code --wait
    autocrlf = input

[init]
    defaultBranch = main

[color]
    ui = auto

[alias]
    st = status
    ci = commit
    co = checkout
    br = branch
    lg = log --oneline --graph --decorate
```

### Remove a Setting

```bash
git config --global --unset setting.name
```

## Recommended Starter Configuration

Here's a complete setup script you can run:

```bash
# Identity (CHANGE THESE!)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Editor (choose one)
git config --global core.editor "code --wait"

# Default branch
git config --global init.defaultBranch main

# Line endings (use 'true' on Windows, 'input' on Mac/Linux)
git config --global core.autocrlf input

# Colors
git config --global color.ui auto

# Pull behavior
git config --global pull.rebase false

# Useful aliases
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate"
git config --global alias.last "log -1 HEAD"
```

## Verify Your Setup

Run this to confirm everything is configured:

```bash
git config --global --list
```

You should see output like:

```
user.name=Your Name
user.email=your.email@example.com
core.editor=code --wait
init.defaultbranch=main
core.autocrlf=input
color.ui=auto
pull.rebase=false
alias.st=status
alias.ci=commit
...
```

## Practice Exercise

1. Set your name and email:
   ```bash
   git config --global user.name "Your Actual Name"
   git config --global user.email "your.actual@email.com"
   ```

2. Set your preferred editor:
   ```bash
   git config --global core.editor "code --wait"
   ```

3. Set the default branch name:
   ```bash
   git config --global init.defaultBranch main
   ```

4. Verify your settings:
   ```bash
   git config --global --list
   ```

## Common Questions

### Can I have different settings for different projects?
Yes! Use `git config` without `--global` inside a repository to set project-specific settings:
```bash
cd my-work-project
git config user.email "alice@company.com"
```

### How do I change a setting?
Just run the same command with the new value. It overwrites the old one.

### Where is my config file?
- **Global:** `~/.gitconfig` or `C:\Users\YourName\.gitconfig`
- **Local:** `.git/config` inside your repository

---

## Summary

- Configure your name and email before using Git
- Settings can be system-wide, global (user), or local (repository)
- Use `--global` for settings that apply to all your projects
- Set your preferred editor so Git doesn't open Vim by default
- Set default branch name to `main`
- Create aliases for frequently used commands
- You can view settings with `git config --list`

---

**Next:** [[04 - Your First Repository]]

**Previous:** [[02 - Installing Git]]

**Back to:** [[00 - Welcome to Git & GitHub]]
