# Git Setup & Configuration Guide

A complete, reusable Git setup for fresh systems, including authentication, hygiene files, backups, and dotfiles.

* **Scope:** Git only (no tooling opinions)
* **Note:** This guide avoids scripts because:
  * Git config is global and stateful
  * Manual commands are visible and reversible
  * Less risk than automation

## 1. Install Git

### Windows

```powershell
winget install --id Git.Git
```

> Restart PowerShell or Git Bash after installation.

### Linux (Arch)

```sh
sudo pacman -S git
```

### Linux (Ubuntu / Debian)

```sh
sudo apt update && sudo apt install git
```

### macOS (Homebrew)

```sh
brew install git
```

### Verify Installation

```sh
git --version
```

## 2. Basic Configuration (Required)

```sh
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
```

### Default Branch Name

```sh
git config --global init.defaultBranch main
```

## 3. Authentication with SSH (Strongly Recommended)

### Generate SSH Key

```sh
ssh-keygen -t ed25519 -C "you@email.com"
```

Press **Enter** for defaults.
Set a passphrase if possible.

> Never commit or share your private SSH key (`id_ed25519`).

### Start SSH Agent

```sh
eval "$(ssh-agent -s)"
```

> **Windows:** run this in **Git Bash**.

### Add Key

```sh
ssh-add ~/.ssh/id_ed25519
```

### Copy Public Key

```sh
cat ~/.ssh/id_ed25519.pub
```

Add it to:

* GitHub → Settings → SSH and GPG keys
* GitLab → Preferences → SSH Keys

> Remove unused older keys.

### Test Connection

```sh
ssh -T git@github.com
```

## 4. Authentication with HTTPS (Alternative)

```sh
git clone https://github.com/username/repository.git
```

When prompted:

* **Username:** GitHub/GitLab username
* **Password:** **Personal Access Token (PAT)**

### Cache Credentials

```sh
git config --global credential.helper cache
```

> On Windows, Git uses **Credential Manager** by default.
> This mainly affects Linux/macOS users.

## 5. Recommended Global Settings

### Line Endings (Very Important)

* **Windows**

```sh
git config --global core.autocrlf true
```

* **Linux / macOS**

```sh
git config --global core.autocrlf input
```

## 6. `.gitattributes` (Strong Recommendation)

Create `.gitattributes` in the repository root.

### Basic

```gitattributes
* text=auto
```

### Stricter (Optional)

```gitattributes
*.sh  text eol=lf
*.py  text eol=lf
*.js  text eol=lf
*.bat text eol=crlf
```

## 7. Default Text Editor

```sh
git config --global core.editor "code --wait"   # VS Code
git config --global core.editor "nano"          # Nano
git config --global core.editor "edit"          # Windows Edit
```

## 8. Enable Color Output

```sh
git config --global color.ui auto
```

## 9. Git Aliases

```sh
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
```

### Log Alias

```sh
git config --global alias.lg "log --graph --abbrev-commit --decorate \
--format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) \
%C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(auto)%d%C(reset)' --all"
```

Usage:

```sh
git lg
```

## 10. Advanced (Optional but Useful)

```sh
git config --global fetch.prune true
git config --global rerere.enabled true
```

## 11. Verify Configuration

```sh
git config --list
git config --global user.name
```

## 12. `.gitignore` (Strong Recommendation)

A `.gitignore` file **must be created per repository** and placed at the **root of that repository**.
It controls **what files are ignored only for that repo**.

You can **also** create a **global ignore** for files you *never* want to track in any repo.

### Repository `.gitignore` (Required)

Create a file named `.gitignore` at the **root of each repository**.

Template: [`.gitignore`](./dotfiles/.gitignore)

> `.gitignore` should be committed with the repository.

### Global `.gitignore` (Optional but Recommended)

A **global ignore** applies to **all repositories** on your system.
Use it for OS files, editor junk, and personal preferences.

Create [`.gitignore_global`](./dotfiles/.gitignore_global), then register it:

```sh
git config --global core.excludesfile ~/.gitignore_global
```

and verify:

```sh
git config --global --get core.excludesfile
```

* `.gitignore` → **per repository**, committed to Git
* `.gitignore_global` → **per machine**, never committed

If a file is **already tracked**, ignoring it won’t remove it:

```sh
git rm --cached filename
```

## 13. Backup Git Configuration

### Backup

```sh
cp ~/.gitconfig ~/gitconfig.backup
cp ~/.gitignore_global ~/.gitignore_global.backup
cp -r ~/.config/git ~/git-backup
```

## 14. Restore Dotfiles (Fresh System)

### From Backup

```sh
cp ~/.gitconfig.backup ~/.gitconfig
cp ~/.gitignore_global.backup ~/.gitignore_global
cp -r ~/git-backup ~/.config/git
git config --global core.excludesfile ~/.gitignore_global
```

### From Dotfiles

```sh
cp ./dotfiles/.gitconfig ~/.gitconfig
cp ./dotfiles/.gitignore_global ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```

## What to Include / Exclude

### Include

* `.gitconfig`
* `.gitignore_global`
* `.gitattributes`

### Never Include

* SSH private keys (`~/.ssh/id_*`)
* Stored credentials
* System Git config

## 15. Reset Git Configuration (Clean Slate)

Use this when you want to **completely remove Git configuration** and start fresh.

### 15.1 Inspect Existing Configuration (Important)

Before deleting anything, see **what exists and where**:

```sh
git config --list --show-origin
```

This shows whether a setting comes from:

* system
* global
* local (repo)

### 15.2 Soft Reset (Recommended)

Removes **common global settings** without deleting files.

```sh
git config --global --unset-all user.name
git config --global --unset-all user.email
git config --global --unset-all init.defaultBranch
git config --global --unset-all core.autocrlf
git config --global --unset-all core.editor
git config --global --unset-all color.ui
git config --global --unset-all credential.helper
git config --global --unset-all fetch.prune
git config --global --unset-all rerere.enabled
```

Remove all aliases:

```sh
git config --global --remove-section alias
```

Use this if you want to **keep Git installed but reset behavior**.

### 15.3 Nuclear Reset (Full Clean Slate)

Deletes **all global Git configuration files**.

#### Linux / macOS

```sh
rm -f ~/.gitconfig
rm -rf ~/.config/git
rm -f ~/.git-credentials
```

#### Windows (PowerShell)

```powershell
Remove-Item $HOME\.gitconfig -Force -ErrorAction SilentlyContinue
Remove-Item $HOME\.config\git -Recurse -Force -ErrorAction SilentlyContinue
Remove-Item $HOME\.git-credentials -Force -ErrorAction SilentlyContinue
```

This removes:

* username / email
* aliases
* autocrlf
* editor
* credential helpers
* stored HTTPS credentials

Best option for **starting completely fresh**.

### 15.4 Remove Repository-Local Config (Per Repo)

Run **inside a repository**.

⚠️ This affects only that repo.

#### Nuclear (fast)

```sh
rm .git/config
```

#### Safer (selective)

```sh
git config --local --remove-section core
git config --local --remove-section remote
git config --local --remove-section branch
```

### 15.5 Remove System-Wide Git Config (Advanced)

⚠️ Only if you know what you’re doing.

#### Linux / macOS

```sh
sudo rm /etc/gitconfig
```

#### Windows (Git for Windows)

```text
C:\Program Files\Git\etc\gitconfig
```

### 15.6 Remove Stored Credentials

#### Windows

List credentials:

```powershell
cmdkey /list
```

Delete Git entries:

```powershell
cmdkey /delete:git:https://github.com
cmdkey /delete:git:https://gitlab.com
cmdkey /delete:git:https://dev.azure.com
```

#### macOS

* Open **Keychain Access**
* Remove GitHub / GitLab entries

#### Linux

```sh
rm -f ~/.git-credentials
```

### 15.7 Verify Reset

```sh
git config --list
```

If nothing prints → **Git is fully reset**

### TL;DR (Nuclear Reset)

```sh
rm -f ~/.gitconfig
rm -rf ~/.config/git
rm -f ~/.git-credentials
```
