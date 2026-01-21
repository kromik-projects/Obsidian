# Installing Git

## Overview

Before you can use Git, you need to install it on your computer. This guide covers installation for all major operating systems.

## Check if Git is Already Installed

Open your terminal (or Command Prompt on Windows) and type:

```bash
git --version
```

If you see a version number like `git version 2.42.0`, Git is already installed! You can skip to [[03 - Configuring Git]].

If you see "command not found" or an error, follow the instructions below for your operating system.

---

## Windows Installation

### Option 1: Git for Windows (Recommended)

1. **Download the installer**
   - Go to https://git-scm.com/download/windows
   - The download should start automatically

2. **Run the installer**
   - Double-click the downloaded `.exe` file
   - Click "Yes" if Windows asks for permission

3. **Installation options** (recommended settings):

   | Screen | Recommended Choice |
   |--------|-------------------|
   | Select Components | Keep defaults, ensure "Git Bash Here" is checked |
   | Default Editor | Choose your preferred editor (VS Code recommended) |
   | Initial Branch Name | Select "Override" and use `main` |
   | PATH Environment | "Git from the command line and also from 3rd-party software" |
   | SSH Executable | "Use bundled OpenSSH" |
   | HTTPS Transport | "Use the OpenSSL library" |
   | Line Ending Conversions | "Checkout Windows-style, commit Unix-style" |
   | Terminal Emulator | "Use MinTTY" |
   | Default Behavior of git pull | "Default (fast-forward or merge)" |
   | Credential Helper | "Git Credential Manager" |
   | Extra Options | Keep defaults |

4. **Finish installation**
   - Click "Install" and wait for completion
   - Click "Finish"

5. **Verify installation**
   - Open a new Command Prompt or PowerShell
   - Type: `git --version`
   - You should see the version number

> [!tip] Git Bash
> The installation includes **Git Bash**, a terminal that provides a Unix-like command line on Windows. Many developers prefer using Git Bash over Command Prompt.

### Option 2: Using winget (Windows Package Manager)

If you have Windows 10/11 with winget:

```powershell
winget install Git.Git
```

---

## macOS Installation

### Option 1: Xcode Command Line Tools (Easiest)

1. Open Terminal (Applications → Utilities → Terminal)

2. Type:
   ```bash
   git --version
   ```

3. If Git isn't installed, macOS will prompt you to install the Xcode Command Line Tools. Click "Install"

4. Wait for the installation to complete (may take several minutes)

5. Verify:
   ```bash
   git --version
   ```

### Option 2: Homebrew (Recommended for Developers)

If you have Homebrew installed (or want to install it):

1. Install Homebrew (if needed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Install Git:
   ```bash
   brew install git
   ```

3. Verify:
   ```bash
   git --version
   ```

### Option 3: Official Installer

1. Download from https://git-scm.com/download/mac
2. Open the `.dmg` file
3. Run the installer package
4. Follow the prompts

---

## Linux Installation

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install git
```

### Fedora

```bash
sudo dnf install git
```

### Arch Linux

```bash
sudo pacman -S git
```

### openSUSE

```bash
sudo zypper install git
```

### Verify Installation

```bash
git --version
```

---

## Verifying Your Installation

After installing Git, open a new terminal window and run these commands:

```bash
# Check Git version
git --version

# Check where Git is installed
which git      # macOS/Linux
where git      # Windows
```

You should see output like:
```
git version 2.42.0
/usr/bin/git
```

## Understanding the Terminal

Since you'll be using Git through the terminal, here's a quick primer:

### What is a Terminal?

A **terminal** (also called command line, console, or shell) is a text-based interface to your computer. Instead of clicking icons, you type commands.

### Opening the Terminal

| Operating System | How to Open |
|-----------------|-------------|
| **Windows** | Search for "Git Bash" or "Command Prompt" |
| **macOS** | Applications → Utilities → Terminal |
| **Linux** | Usually Ctrl+Alt+T or search for "Terminal" |

### Basic Terminal Commands

These will be helpful as you learn Git:

```bash
# Print current directory (where you are)
pwd

# List files in current directory
ls              # macOS/Linux
dir             # Windows Command Prompt
ls              # Git Bash on Windows

# Change directory
cd folder_name          # Go into a folder
cd ..                   # Go up one level
cd ~                    # Go to home directory

# Create a new directory
mkdir folder_name

# Clear the screen
clear           # macOS/Linux/Git Bash
cls             # Windows Command Prompt
```

### Terminal Tips

> [!tip] Tab Completion
> Press **Tab** while typing a file or folder name to auto-complete it. This saves time and prevents typos!

> [!tip] Command History
> Press **Up Arrow** to cycle through previous commands. Press **Down Arrow** to go forward.

> [!tip] Cancel a Command
> Press **Ctrl+C** to stop a running command or cancel what you're typing.

## Practice Exercise

Let's verify everything is working:

1. Open your terminal

2. Check Git is installed:
   ```bash
   git --version
   ```

3. Create a practice folder:
   ```bash
   cd ~
   mkdir git-practice
   cd git-practice
   pwd
   ```

4. You should see a path like `/Users/yourname/git-practice` or `C:\Users\yourname\git-practice`

You now have a practice folder ready for the upcoming tutorials!

## Troubleshooting

### "git: command not found"
- Make sure you opened a **new** terminal window after installation
- On Windows, try Git Bash instead of Command Prompt
- Verify Git is in your system PATH

### Installation Failed on Windows
- Run the installer as Administrator
- Temporarily disable antivirus software
- Download from the official site only

### macOS Says "unidentified developer"
- Right-click the installer and select "Open"
- Or go to System Preferences → Security & Privacy → click "Open Anyway"

### Permission Denied on Linux
- Make sure you're using `sudo` for installation commands
- Check that you have administrator access

---

## Summary

- Git can be installed on Windows, macOS, and Linux
- Windows users should install "Git for Windows" which includes Git Bash
- macOS users can install via Xcode Command Line Tools or Homebrew
- Linux users can install via their package manager
- The terminal is where you'll run Git commands
- Create a `git-practice` folder to use throughout these tutorials

---

**Next:** [[03 - Configuring Git]]

**Previous:** [[01 - What is Version Control]]

**Back to:** [[00 - Welcome to Git & GitHub]]
