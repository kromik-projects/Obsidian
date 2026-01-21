# Creating a GitHub Account

## Step-by-Step Account Creation

### Step 1: Go to GitHub

Open your browser and visit: **https://github.com**

### Step 2: Sign Up

Click the **"Sign up"** button in the top right corner.

### Step 3: Enter Your Information

You'll need to provide:

1. **Email address**
   - Use a professional email
   - This will be visible in commits (unless you use a private email)

2. **Password**
   - At least 15 characters OR
   - At least 8 characters including a number and lowercase letter
   - Use a password manager!

3. **Username**
   - This becomes your GitHub URL: `github.com/username`
   - Choose carefully - changing it later can break links
   - Keep it professional

> [!tip] Choosing a Username
> - Use your real name or a professional handle
> - Avoid numbers like "dev123" or "coder2024"
> - Keep it simple and memorable
> - Consider: future employers will see this!

### Step 4: Verify Your Account

Complete the puzzle/verification (proves you're human).

### Step 5: Personalization (Optional)

GitHub may ask about:
- Your role (student, developer, etc.)
- What you'll use GitHub for
- Your experience level

You can skip these or answer honestly.

### Step 6: Verify Your Email

Check your inbox for a verification email and click the link.

**Congratulations! You have a GitHub account!**

## Setting Up Your Profile

### Add a Profile Picture

1. Click your avatar (top right) → **Settings**
2. Under "Profile", click "Edit" on your photo
3. Upload a professional photo or avatar

> [!tip] Profile Photo Tips
> - Use a real photo or professional avatar
> - Make sure you're recognizable
> - Keep it appropriate for work settings

### Complete Your Bio

1. Go to **Settings** → **Profile**
2. Fill in:
   - **Name** - Your full name
   - **Bio** - Brief description (160 chars)
   - **Company** - Where you work/study
   - **Location** - City, Country
   - **Website** - Your portfolio or blog
   - **Social accounts** - Twitter/LinkedIn

**Example Bio:**
```
Full-stack developer | JavaScript enthusiast | Open source contributor
Learning something new every day 🚀
```

### Create a Profile README

A special feature that displays on your profile:

1. Create a new repository named exactly: **your-username**
   (e.g., if your username is "alice", create a repo called "alice")

2. Make it public and initialize with a README

3. Edit README.md with information about yourself:

```markdown
# Hi, I'm Alice! 👋

## About Me
- 🔭 I'm currently working on **awesome projects**
- 🌱 I'm learning **TypeScript and React**
- 💬 Ask me about **JavaScript, Git, and web development**
- 📫 How to reach me: **alice@example.com**

## Languages and Tools
![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Python](https://img.shields.io/badge/-Python-3776AB?style=flat&logo=python&logoColor=white)

## GitHub Stats
![Your GitHub stats](https://github-readme-stats.vercel.app/api?username=your-username)
```

## Configuring Settings

### Email Settings

1. Go to **Settings** → **Emails**
2. Important options:
   - **Keep my email private** - Use GitHub's no-reply email
   - **Block command line pushes** - Prevent accidental email exposure

If you enable private email, use this in your Git config:
```bash
git config --global user.email "username@users.noreply.github.com"
```

### Notifications

1. Go to **Settings** → **Notifications**
2. Configure how you're notified:
   - Email notifications
   - Web notifications
   - Mobile notifications (if using app)

**Recommendation:** Start with defaults, adjust as you get more activity.

## Setting Up SSH Keys

SSH keys let you push/pull without entering passwords.

### Generate SSH Key

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

Press Enter for default file location. Optionally add a passphrase.

### Add Key to SSH Agent

**macOS/Linux:**
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Windows (Git Bash):**
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Copy Public Key

**macOS:**
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

**Linux:**
```bash
cat ~/.ssh/id_ed25519.pub
# Copy the output manually
```

**Windows:**
```bash
clip < ~/.ssh/id_ed25519.pub
```

### Add to GitHub

1. Go to **Settings** → **SSH and GPG keys**
2. Click **New SSH key**
3. Give it a title (e.g., "My Laptop")
4. Paste your public key
5. Click **Add SSH key**

### Test Connection

```bash
ssh -T git@github.com
```

You should see:
```
Hi username! You've successfully authenticated...
```

## Setting Up Two-Factor Authentication (2FA)

**Highly recommended** for account security!

### Enable 2FA

1. Go to **Settings** → **Password and authentication**
2. Click **Enable two-factor authentication**
3. Choose method:
   - **Authenticator app** (recommended) - Authy, Google Authenticator
   - **SMS** (less secure but better than nothing)

### Save Recovery Codes

GitHub provides recovery codes. **Save these somewhere safe!**
- Password manager
- Secure note
- Printed and locked away

If you lose your phone, these codes let you access your account.

## Personal Access Tokens

For HTTPS authentication (instead of passwords):

### Create a Token

1. Go to **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
2. Click **Generate new token (classic)**
3. Give it a name: "My Laptop CLI"
4. Select scopes:
   - `repo` - Full repository access
   - `workflow` - If using GitHub Actions
5. Click **Generate token**
6. **Copy immediately** - You won't see it again!

### Use the Token

When Git asks for your password, paste the token instead.

To save it:
```bash
# Cache for 1 hour
git config --global credential.helper 'cache --timeout=3600'

# Or use your OS credential manager
git config --global credential.helper osxkeychain  # macOS
git config --global credential.helper manager      # Windows
```

## GitHub Student Developer Pack

If you're a student, you get free access to:
- GitHub Pro features
- Free domains
- Cloud credits
- Development tools

**Apply at:** https://education.github.com/pack

## Install GitHub CLI (Optional)

The GitHub CLI lets you manage GitHub from your terminal:

```bash
# macOS
brew install gh

# Windows
winget install GitHub.cli

# Login
gh auth login
```

Now you can:
```bash
gh repo create        # Create repos
gh pr create          # Create pull requests
gh issue list         # View issues
```

## What's Next?

Your account is ready! Next steps:
1. Create your first repository
2. Push some code
3. Explore other projects

---

## Summary

- Create an account at github.com
- Choose a professional username
- Complete your profile (photo, bio, info)
- Set up SSH keys for secure access
- Enable 2FA for security
- Create a profile README to stand out
- Consider GitHub CLI for terminal workflow

---

**Next:** [[16 - Your First GitHub Repository]]

**Previous:** [[14 - Introduction to GitHub]]

**Back to:** [[00 - Welcome to Git & GitHub]]
