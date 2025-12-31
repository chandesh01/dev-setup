# Git Configuration Guide

A complete, reusable Git setup for fresh systems.

* **Scope:** Git only (no tooling opinions)
* **Philosophy:** Manual commands over scripts (visible, reversible, state-aware).

---

## 1. Setup

This section covers installation, authentication, and optimizing the environment for a fresh system.

### Install Git

**Windows**

```powershell
winget install --id Git.Git
```

*Note: Restart PowerShell or Git Bash after installation.*

**Linux (Arch)**

```sh
sudo pacman -S git
```

**Linux (Ubuntu / Debian)**

```sh
sudo apt update && sudo apt install git
```

**macOS (Homebrew)**

```sh
brew install git
```

**Verify Installation**

```sh
git --version
```

### Basic Configuration (Required)

```sh
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
```

**Default Branch Name**

```sh
git config --global init.defaultBranch main
```

### Authentication with SSH (Strongly Recommended)

**Generate SSH Key**

```sh
ssh-keygen -t ed25519 -C "you@email.com"
```

* Press **Enter** for defaults.
* Set a passphrase for extra security.
* **Never** commit or share your private SSH key (`id_ed25519`).

**Start SSH Agent**

```sh
eval "$(ssh-agent -s)"
```

*Windows users: Run this in **Git Bash**, not PowerShell.*

**Add Key to Agent**

```sh
ssh-add ~/.ssh/id_ed25519
```

**Copy Public Key**

```sh
cat ~/.ssh/id_ed25519.pub
```

Copy the output and add it to:

* **GitHub:** Settings → SSH and GPG keys
* **GitLab:** Preferences → SSH Keys

**Test Connection**

```sh
ssh -T git@github.com
```

### Authentication with HTTPS (Alternative)

Use this only if SSH is blocked or unavailable.

```sh
git clone https://github.com/username/repository.git
```

When prompted:

* **Username:** GitHub/GitLab username
* **Password:** **Personal Access Token (PAT)** (Passwords are deprecated)

**Cache Credentials**

```sh
git config --global credential.helper cache
```

*Windows users: Git automatically uses the "Git Credential Manager".*

### Recommended Global Settings

**Line Endings (Critical)**
Inconsistent line endings cause "phantom" file changes.

*Windows:*

```sh
git config --global core.autocrlf true
```

*Linux / macOS:*

```sh
git config --global core.autocrlf input
```

### `.gitattributes` (Strong Recommendation)

Create a `.gitattributes` file in the **root of your repository** to force consistency regardless of user config.

**Basic Template**

```gitattributes
* text=auto
```

**Strict Template (Optional)**

```gitattributes
*.sh  text eol=lf
*.py  text eol=lf
*.js  text eol=lf
*.bat text eol=crlf
```

### Default Text Editor

Set the editor Git uses for commit messages and rebases.

```sh
git config --global core.editor "code --wait"   # VS Code (Recommended)
git config --global core.editor "nano"          # Nano
git config --global core.editor "vim"           # Vim
```

### Git Aliases

Shortcuts for common commands.

```sh
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
```

**The "Super Log" Alias**
Visualizes the commit history graph in the terminal.

```sh
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)' --all"
```

*Usage:* `git lg`

### `.gitignore` Strategy

1. **Repository `.gitignore**`: Place at the root of a specific repo. Tracks project-specific ignores (e.g., `node_modules`, `dist/`). **Must be committed.**
2. **Global `.gitignore**`: Place in your home directory. Tracks system-wide ignores (e.g., `.DS_Store`, `Thumbs.db`). **Never committed.**

**Setup Global Ignore**

```sh
# 1. Create the file
touch ~/.gitignore_global

# 2. Register it with Git
git config --global core.excludesfile ~/.gitignore_global
```

### GPG Commit Signing (Traditional)

Signs commits to verify your identity (shows "Verified" badge on GitHub).

**1. Install GPG**

* Linux: `sudo apt install gnupg`
* macOS: `brew install gnupg`
* Windows: `winget install GnuPG.GnuPG`

**2. Generate Key**

```sh
gpg --full-generate-key
```

* Select **RSA and RSA** (4096 bits).
* **Important:** Email must match your GitHub/GitLab email exactly.

**3. Configure Git to Sign**

```sh
git config --global user.signingkey <KEYID>
git config --global commit.gpgsign true
git config --global tag.gpgsign true
```

*(Run `gpg --list-secret-keys --keyid-format=long` to find your `<KEYID>`)*

**4. Upload Public Key**

```sh
gpg --armor --export <KEYID>
```

Paste this block into GitHub/GitLab GPG settings.

### SSH-Based Commit Signing (Modern Alternative)

Simpler than GPG. Uses your existing SSH key. Requires Git 2.34+.

**Enable SSH Signing**

```sh
git config --global gpg.format ssh
git config --global commit.gpgsign true
git config --global gpg.ssh.program ssh-keygen
git config --global user.signingkey ~/.ssh/id_ed25519.pub
```

**Register Key**
Upload the key content again to GitHub/GitLab, but select **"Signing Key"** instead of "Authentication Key".

---

## 2. Backup

Critical steps to secure your configuration and identity files.

### Backup Git Configuration

```sh
cp ~/.gitconfig ~/gitconfig.backup
cp ~/.gitignore_global ~/.gitignore_global.backup
# Optional: backup entire config dir
cp -r ~/.config/git ~/git-backup
```

### Backup GPG Keys (Critical)

If you lose your private GPG key, you **cannot** sign as that identity again.

**1. Identify Key ID**

```sh
gpg --list-secret-keys --keyid-format=long
# Look for the ID after 'sec rsa4096/' (e.g., ABC123456789)
```

**2. Export Private Key (Secure Storage Only)**

```sh
gpg --armor --export-secret-keys <KEYID> > gpg-private.key
chmod 600 gpg-private.key
```

**3. Export Public Key**

```sh
gpg --armor --export <KEYID> > gpg-public.key
```

### Backup SSH Keys

**1. Copy Keys**

```sh
cp ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.backup
cp ~/.ssh/id_ed25519.pub ~/.ssh/id_ed25519.pub.backup
```

**2. Secure Permissions**

```sh
chmod 600 ~/.ssh/id_ed25519.backup
```

### Checklist: What to Backup

* [ ] `~/.gitconfig`
* [ ] `~/.gitignore_global`
* [ ] SSH Private Key (Encrypted location)
* [ ] GPG Private Key (Encrypted location)

---

## 3. Restore

Steps to bring a fresh system to a working state using your backup files.

### Restore Dotfiles

*Assumes you have copied your backup files to the current directory.*

```sh
cp gitconfig.backup ~/.gitconfig
cp gitignore_global.backup ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```

### Restore SSH Keys

**1. Place Files**

```sh
mkdir -p ~/.ssh
cp id_ed25519.backup ~/.ssh/id_ed25519
cp id_ed25519.pub.backup ~/.ssh/id_ed25519.pub
```

**2. Fix Permissions (Required)**
SSH will reject keys with open permissions.

```sh
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

**3. specific Add to Agent**

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Restore GPG Keys

**1. Import Keys**

```sh
gpg --import gpg-private.key
gpg --import gpg-public.key
```

**2. Restore Trust Level**
Required to use the key without "Untrusted" warnings.

```sh
gpg --edit-key <KEYID>
```

Inside the `gpg>` prompt, type:

1. `trust`
2. `5` (Select "Ultimate")
3. `quit`

### Reset Git Configuration (Clean Slate)

Use this only if you want to wipe the current machine's Git config before restoring.

**Soft Reset (Unset Globals)**

```sh
git config --global --unset-all user.name
git config --global --unset-all user.email
git config --global --unset-all core.editor
git config --global --unset-all core.autocrlf
```

**Nuclear Reset (Delete Config Files)**

*Linux / macOS:*

```sh
rm -f ~/.gitconfig
rm -rf ~/.config/git
rm -f ~/.git-credentials
```

*Windows (PowerShell):*

```powershell
Remove-Item $HOME\.gitconfig -Force -ErrorAction SilentlyContinue
Remove-Item $HOME\.config\git -Recurse -Force -ErrorAction SilentlyContinue
```
