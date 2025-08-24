# Zellij Sessionizer

A fuzzy finder-powered project switcher for [Zellij](https://zellij.dev/) sessions. Quickly navigate and switch between your development projects using [fzf](https://github.com/junegunn/fzf) and automatically create or switch to Zellij sessions with the proper working directory.

Inspired by ThePrimeagen's [tmux-sessionizer](https://github.com/ThePrimeagen/.dotfiles/blob/master/bin/.local/scripts/tmux-sessionizer) but adapted for Zellij.

## Features

- 🔍 **Fuzzy Finding**: Use fzf to quickly search and select from your projects
- 🚀 **Smart Session Management**: Automatically creates new sessions or switches to existing ones
- 📁 **Configurable Paths**: Define your own project directories to search
- 🔄 **Seamless Switching**: Uses the zellij-switch plugin for smooth session transitions
- ⚡ **Fast**: Instant project switching without manual navigation

## Prerequisites

- [Zellij](https://zellij.dev/) terminal multiplexer
- [fzf](https://github.com/junegunn/fzf) fuzzy finder
- [zellij-switch plugin](https://github.com/mostafaqanbaryan/zellij-switch) for session switching

## Installation

1. Clone this repository or download the script:
```bash
curl -o zellij-sessionizer https://raw.githubusercontent.com/yourusername/zellij-sessionizer/main/bin/zellij-sessionizer
chmod +x zellij-sessionizer
```

2. Move the script to your PATH:
```bash
mv zellij-sessionizer ~/.local/bin/ && chmod +x ~/.local/bin/zellij-sessionizer
# or
mv zellij-sessionizer /usr/local/bin/ && chmod +x /usr/local/bin/zellij-sessionizer
```

3. Install the [mostafaqanbaryan/zellij-switch](https://github.com/mostafaqanbaryan/zellij-switch) plugin by adding it to your Zellij config or let it auto-download on first use.

## Configuration

Edit the script to customize your project directories:

```bash
# Directories to search for projects (searches one level deep)
SEARCH_PATHS=("$HOME/Projects" "$HOME/code")

# Specific directories to include
SPECIFIC_PATHS=("$HOME/.dotfiles")
```

### Search Paths
- `SEARCH_PATHS`: Directories where the script will look for project folders (searches one level deep)
- `SPECIFIC_PATHS`: Individual directories to include directly in the selection list

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
3. **Session Management**: Leverages the zellij-switch plugin to handle session creation and switching
4. **Working Directory**: Automatically sets the correct working directory for your project

## Dependencies

- **Zellij**: Terminal multiplexer for session management
- **fzf**: Fuzzy finder for project selection
- **zellij-switch**: Plugin for seamless session switching

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
