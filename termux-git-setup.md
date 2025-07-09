# Termux Git Setup Guide

## 1. Install Git and OpenSSH
```bash
pkg update && pkg upgrade
pkg install git openssh
```

## 2. Configure Git Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## 3. Generate SSH Key for GitHub
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
cat ~/.ssh/id_ed25519.pub
```

## 4. Add SSH Key to GitHub
1. Copy the output from the `cat` command above
2. Go to GitHub Settings → SSH and GPG keys
3. Click "New SSH key"
4. Paste your key and save

## 5. Test SSH Connection
```bash
ssh -T git@github.com
```

## 6. Configure Git for Mobile
```bash
# Use simple push (recommended for mobile)
git config --global push.default simple

# Set up credential caching (optional)
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'

# Enable color output
git config --global color.ui true

# Set default branch name
git config --global init.defaultBranch main
```

## 7. Storage Access (Important!)
```bash
# Grant storage permission to Termux
termux-setup-storage
```

## 8. Clone Repositories Using SSH
```bash
# Use SSH URL format
git clone git@github.com:username/repository.git

# For your cheatsheet repo:
git clone git@github.com:GGPrompts/claude-code-cheatsheet.git
```

## Common Issues & Solutions

### Permission Denied
```bash
# Fix SSH permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### Host Key Verification Failed
```bash
# Add GitHub to known hosts
ssh-keyscan github.com >> ~/.ssh/known_hosts
```

### Timeout Issues
```bash
# Add to ~/.ssh/config
echo "Host github.com
  Hostname ssh.github.com
  Port 443
  User git" >> ~/.ssh/config
```

### Termux-Specific Git Aliases
```bash
# Add useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.pl pull
git config --global alias.ps push
```

## Quick Setup Script
Save this as `setup-git.sh`:
```bash
#!/data/data/com.termux/files/usr/bin/bash

echo "Setting up Git for Termux..."

# Update packages
pkg update -y && pkg upgrade -y
pkg install -y git openssh

# Get user info
read -p "Enter your GitHub username: " github_user
read -p "Enter your GitHub email: " github_email

# Configure Git
git config --global user.name "$github_user"
git config --global user.email "$github_email"
git config --global init.defaultBranch main
git config --global color.ui true
git config --global push.default simple

# Generate SSH key
ssh-keygen -t ed25519 -C "$github_email" -f ~/.ssh/id_ed25519 -N ""

# Set correct permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# Display public key
echo -e "\n\nYour SSH public key (copy this to GitHub):"
cat ~/.ssh/id_ed25519.pub

echo -e "\n\nSetup complete! Add the above key to GitHub, then test with:"
echo "ssh -T git@github.com"
```

Run with:
```bash
bash setup-git.sh
```