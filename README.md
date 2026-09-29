# macOS Dotfiles

This repository contains my macOS configuration files for `yabai`, `skhd`, and `zsh`.

## Prerequisites

Before starting, make sure you have [Homebrew](https://brew.sh/) installed:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Installation on a Fresh macOS

### 1. Install Dependencies

Install `yabai`, `skhd`, and `SwiftBar` (used in `.yabairc` for spaces tracking).

```bash
brew install koekeishiya/formulae/yabai
brew install koekeishiya/formulae/skhd
brew install --cask swiftbar
```

*(Note: `zsh` is the default shell on modern macOS versions. If for some reason it isn't, you can install it via `brew install zsh`)*

### 2. Clone the Repository

Clone this repository into your home directory:

```bash
git clone https://github.com/MrTartuf0/dotfiles.git ~/dotfiles
```

### 3. Create Symlinks

Link the configuration files to your home directory so the system can read them:

```bash
ln -s ~/dotfiles/.yabairc ~/.yabairc
ln -s ~/dotfiles/.skhdrc ~/.skhdrc
ln -s ~/dotfiles/.zshrc ~/.zshrc
```

### 4. Yabai Scripting Addition (Optional but recommended)

This `.yabairc` config is set up to load the yabai scripting addition (`sudo yabai --load-sa`). This is required for advanced features like space management and window transparency.

To use this:
1. You must partially disable System Integrity Protection (SIP) on macOS. Refer to the [Yabai Wiki](https://github.com/koekeishiya/yabai/wiki/Disabling-System-Integrity-Protection) for instructions for your specific CPU architecture (Apple Silicon vs Intel).
2. Configure `sudoers` so `yabai` can run the `load-sa` command without a password prompt. Add the following line using `sudo visudo -f /private/etc/sudoers.d/yabai`:
   ```
   <your_username> ALL=(root) NOPASSWD: /opt/homebrew/bin/yabai --load-sa
   ```
   *(If you are on an Intel Mac, the path to yabai will be `/usr/local/bin/yabai` instead)*

### 5. Start Services

Start the services and enable them to run at login:

```bash
yabai --start-service
skhd --start-service
```

### Notes
- **SwiftBar**: Open SwiftBar and install the `yabai_spaces.1d.sh` plugin, as it is referenced in the `.yabairc` config to refresh when spaces change.
- **Terminal & Browser**: The `skhd` configuration includes shortcuts that assume `Terminal` and `Google Chrome` are installed.
- **Autodesk Fusion**: There are several rules in `.yabairc` to prevent yabai from managing Autodesk Fusion dialogs and floating windows properly.
