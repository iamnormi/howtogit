# SSH Key Setup Script

This script automates generating an SSH key, adding it to `ssh-agent`, and optionally copying it to the clipboard. It is designed for Linux systems (including Arch Linux) and uses modern defaults.

---

## Script

```bash
#!/usr/bin/env bash
# ^ This tells Linux to run the script using bash

set -e
# ^ Exit immediately if any command fails (safer for beginners)

# -------------------------------
# Configuration
# -------------------------------

# Type of SSH key (ed25519 is modern, fast, and secure)
KEY_TYPE="ed25519"

# Location where the SSH key will be stored
KEY="$HOME/.ssh/id_${KEY_TYPE}"

# Comment added to the SSH key (helps identify it later)
# Arch does not always have the `hostname` command,
# so we safely get it from systemd or /etc/hostname
COMMENT="$USER@$(hostnamectl --static 2>/dev/null || cat /etc/hostname)"

# -------------------------------
# Create ~/.ssh directory
# -------------------------------

# Create the .ssh directory if it does not exist
mkdir -p "$HOME/.ssh"

# Set correct permissions:
# 700 = only the user can read/write/enter this directory
chmod 700 "$HOME/.ssh"

# -------------------------------
# Generate SSH key (if missing)
# -------------------------------

# Check if the SSH key already exists
if [[ -f "$KEY" ]]; then
  echo "✅ SSH key already exists:"
  echo "   $KEY"
else
  echo "🆕 No SSH key found. Generating a new one..."

  # ssh-keygen creates a new SSH key
  # -t : key type
  # -f : file path
  # -C : comment (email / username / machine name)
  ssh-keygen -t "$KEY_TYPE" -f "$KEY" -C "$COMMENT"
fi

# -------------------------------
# Start ssh-agent
# -------------------------------

# ssh-agent keeps your SSH key unlocked in memory
# This avoids typing your passphrase every time
echo "🚀 Starting ssh-agent..."
eval "$(ssh-agent -s)" >/dev/null

# -------------------------------
# Add key to ssh-agent
# -------------------------------

# Add your private key to the agent
# You may be asked for the key passphrase
ssh-add "$KEY"

# -------------------------------
# Show public key
# -------------------------------

echo
echo "📎 Your PUBLIC SSH key (safe to share):"
echo "--------------------------------------"
cat "${KEY}.pub"
echo "--------------------------------------"

# -------------------------------
# Copy public key to clipboard (if possible)
# -------------------------------

# Wayland (most modern Arch desktops)
if command -v wl-copy >/dev/null; then
  wl-copy < "${KEY}.pub"
  echo "📋 Public key copied to clipboard (Wayland)"

# X11 (older desktops)
elif command -v xclip >/dev/null; then
  xclip -selection clipboard < "${KEY}.pub"
  echo "📋 Public key copied to clipboard (X11)"

else
  echo "ℹ️ Clipboard tool not found."
  echo "   Install one of these if you want clipboard support:"
  echo "   sudo pacman -S wl-clipboard   # Wayland"
  echo "   sudo pacman -S xclip          # X11"
fi

# -------------------------------
# Final instructions
# -------------------------------

echo
echo "➡️ Next steps:"
echo "1) Copy this key to your server:"
echo "   ~/.ssh/authorized_keys"
echo
echo "2) Or add it to:"
echo "   GitHub / GitLab → SSH Keys"
echo
echo "✨ SSH key setup complete!"
