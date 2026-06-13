# Zellij Sessionizer

A fuzzy finder-powered project switcher for [Zellij](https://zellij.dev/) sessions. Quickly navigate and switch between your development projects using [fzf](https://github.com/junegunn/fzf) and automatically create or switch to Zellij sessions with the proper working directory.

<img width="1907" height="1238" alt="image" src="https://github.com/user-attachments/assets/086d2fcc-2d0f-44fa-896f-9e704eaa49b8" />

Inspired by ThePrimeagen's [tmux-sessionizer](https://github.com/ThePrimeagen/.dotfiles/blob/master/bin/.local/scripts/tmux-sessionizer) but adapted for Zellij.

## Features

- 🔍 **Fuzzy Finding**: Use fzf to quickly search and select from your projects
- 🚀 **Smart Session Management**: Automatically creates new sessions or switches to existing ones
- 📁 **Configurable Paths**: Define your own project directories to search
- ⚡ **Fast**: Instant project switching without manual navigation

## Prerequisites

- [Zellij](https://zellij.dev/) terminal multiplexer
- [fzf](https://github.com/junegunn/fzf) fuzzy finder

## Installation

1. Clone this repository or download the script:
```bash
curl -o zellij-sessionizer https://raw.githubusercontent.com/victor-falcon/zellij-sessionizer/refs/heads/main/zellij-sessionizer
chmod +x zellij-sessionizer
```

2. Move the script to your PATH:
```bash
mv zellij-sessionizer ~/.local/bin/ && chmod +x ~/.local/bin/zellij-sessionizer
# or
mv zellij-sessionizer /usr/local/bin/ && chmod +x /usr/local/bin/zellij-sessionizer
```

## Configuration

Edit the script to customize your project directories:

```bash
# Directories to search for projects (searches one level deep)
SEARCH_PATHS=("$HOME/Projects" "$HOME/code")

# Specific directories to include
SPECIFIC_PATHS=("$HOME/.dotfiles")
```

Or use environment variables to override default project directories:

```bash
# Override default environment variables when launching zellij-sessionizer
# Each variable can contain one or more paths, separated by spaces.

# Directories to search for projects (searches one level deep)
# Default: $HOME/Projects $HOME/Code
ZELLIJ_SESSIONIZER_SEARCH_PATHS="$HOME/projects $HOME/notes" \

# Specific directories to include
# Default: $HOME/.dotfiles $HOME/.dotfiles/.config/nvim
ZELLIJ_SESSIONIZER_SPECIFIC_PATHS="/etc/somedir /etc/otherdir" \

# Operating system type (used for OS-specific behavior)
# Default: $(uname), usually no need to specify this.
ZELLIJ_SESSIONIZER_OS_TYPE_OS_TYPE="Linux" \

zellij-sessionizer
```

### Search Paths
- `SEARCH_PATHS`: Directories where the script will look for project folders (searches one level deep)
- `SPECIFIC_PATHS`: Individual directories to include directly in the selection list

## Zellij keybinfing
With a Run action on Zellij, you can show the sessionizer in a floating window, with a shortcut, and quickly switch to another session.  

This will replicate the popup you can see in the image in this README file:

```
bind "Super s" { Run "zellij-sessionizer" {
    close_on_exit true
    floating true
    x "30%"
    y "10%"
    width "40%"
    height "80%"
}; SwitchToMode "locked"; }
```

## Usage

Simply run the script:

```bash
zellij-sessionizer
```

This will:
1. Scan your configured directories for projects
2. Open an fzf prompt with all found directories
3. Create or switch to a Zellij session named after the selected directory
4. Set the working directory to your selected project

### Keybinding

For optimal productivity, bind the script to a key combination. Add this to your shell config (`.bashrc`, `.zshrc`, etc.):

```bash
bind -x '"\C-f": zellij-sessionizer'  # Bash
bindkey -s '^f' 'zellij-sessionizer\n'  # Zsh
```

## How It Works

1. **Directory Collection**: The script scans your configured paths and collects all valid directories
2. **Fuzzy Selection**: Uses fzf to present an interactive list of projects
3. **Session Management**: Creates or switches to the selected project using Zellij
4. **Working Directory**: Automatically sets the correct working directory for your project

## Dependencies

- **Zellij**: Terminal multiplexer for session management
- **fzf**: Fuzzy finder for project selection

Install dependencies:

```bash
# macOS with Homebrew
brew install zellij fzf

# Ubuntu/Debian
sudo apt install fzf
# Install zellij from GitHub releases

# Arch Linux
sudo pacman -S zellij fzf
```

## Customization

### Adding More Search Paths
```bash
SEARCH_PATHS=("$HOME/Projects" "$HOME/code" "$HOME/work" "$HOME/personal")
```

### Adding Specific Projects
```bash
SPECIFIC_PATHS=("$HOME/.dotfiles" "$HOME/.config" "$HOME/Documents/special-project")
```

### Modifying fzf Behavior
Change the fzf options in the script:
```bash
selected_dir=$(printf '%s\n' "${all_dirs[@]}" | fzf --prompt="Select project: " --height=40% --border)
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
