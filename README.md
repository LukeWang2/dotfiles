# Dotfiles

This repository contains my personal dotfiles and system configuration for both macOS and Linux. The config is split by operating system:

- macOS: `aerospace` window manager, `zsh`, `kitty`, `tmux`, `yazi`, `vim`
- Linux/i3: `i3`, `zsh`, `kitty`, `tmux`, `vim`
- Shared shell and terminal tools: `fzf`, `fd`, `ripgrep`, `zoxide`, `Oh My Zsh`, `Powerlevel10k`

## Repository layout

- `aerospace/` – macOS tiling window manager config
- `i3/` – Linux window manager config
- `kitty/` – terminal config
- `tmux/` – tmux config
- `zsh/` – zsh config and shell setup
- `vim/` – vim setup notes
- `yazi/` – terminal file manager config

---

## Software and packages I use

### macOS

Main desktop/window management

- Aerospace
- Homebrew
- Kitty
- tmux
- zsh + Oh My Zsh + Powerlevel10k
- Yazi
- Vim

Packages installed via Homebrew

- `yazi`
- `ffmpeg-full`
- `sevenzip`
- `jq`
- `poppler`
- `fd`
- `ripgrep`
- `fzf`
- `zoxide`
- `resvg`
- `imagemagick-full`
- `font-symbols-only-nerd-font`

### Linux (i3)

Main desktop/window management

- i3
- dunst notification daemon
- nm-applet network status
- dmenu launcher
- i3status bar
- Kitty
- tmux
- zsh + Oh My Zsh + Powerlevel10k
- Vim

Packages used in the Linux config

- `i3`
- `albert`
- `dex`
- `xss-lock`
- `nm-applet`
- `pamixer`
- `dunst`
- `playerctl`
- `i3status`
- `dmenu`
- `kitty`
- `tmux`
- `zsh`
- `fd`
- `ripgrep`
- `fzf`
- `zoxide`

### Shared shell / terminal tooling

- Oh My Zsh
- Powerlevel10k theme
- zsh-autosuggestions
- zsh-syntax-highlighting
- zsh-vi-mode
- fzf-zsh-plugin
- `z` directory jumping
- `fd` for fast file searching
- `rg` for recursive search
- `fzf` for fuzzy selection
- `zoxide` for smarter directory navigation

---

## macOS install and setup

Use this on a macOS machine.

```zsh
# clone the repo
mkdir -p ~/src && cd ~/src
git clone https://github.com/<your-user>/dotfiles.git
cd dotfiles

# install Homebrew if needed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

echo 'eval "$($(brew --prefix)/bin/brew shellenv)"' >> ~/.zprofile
source ~/.zprofile

# install core packages
brew update
brew install \
  kitty \
  tmux \
  yazi \
  ffmpeg-full \
  sevenzip \
  jq \
  poppler \
  fd \
  ripgrep \
  fzf \
  zoxide \
  resvg \
  imagemagick-full \
  font-symbols-only-nerd-font

# install aerospace
brew install --cask nikitabobko/tap/aerospace

# install Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# install Powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# install zsh plugins
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/jeffreytse/zsh-vi-mode ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-vi-mode
git clone https://github.com/unixorn/fzf-zsh-plugin.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fzf-zsh-plugin
```

> Change powerlevel10k theme with `p10k configure` if necessary

### macOS config file placement

```zsh
# copy shell config
cp ~/src/dotfiles/zsh/zshrc ~/.zshrc

# copy Powerlevel10k config 
cp ~/src/dotfiles/powerlevel10k/.p10k.zsh ~/.p10k.zsh

# copy terminal config
mkdir -p ~/.config/kitty
cp ~/src/dotfiles/kitty/kitty.conf ~/.config/kitty/kitty.conf

# copy tmux config
touch ~/.tmux.conf
cp ~/src/dotfiles/tmux/tmux.conf ~/.tmux.conf

# copy Aerospace config
mkdir -p ~/.config/aerospace
cp ~/src/dotfiles/aerospace/aerospace.toml ~/.config/aerospace/aerospace.toml

# copy yazi config
mkdir -p ~/.config/yazi
cp ~/src/dotfiles/yazi/theme.toml ~/.config/yazi/theme.toml

# install vim runtime if you want the full vim setup
git clone https://github.com/amix/vimrc.git ~/.vim_runtime
sh ~/.vim_runtime/install_basic_vimrc.sh
```

---

## Linux (i3) install and setup

This is aimed at an Ubuntu Linux setup

```bash
# update system
sudo apt update && sudo apt upgrade -y

# install desktop and terminal packages
sudo apt install -y \
  i3 \
  albert \
  dex \
  xss-lock \
  network-manager-gnome \
  pulsemixer \
  dunst \
  playerctl \
  i3status \
  dmenu \
  kitty \
  tmux \
  zsh \
  fd-find \
  ripgrep \
  fzf \
  zoxide \
  git \
  vim \
  curl \
  unzip

# install Oh My Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" -- --unattended

# install Powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"

# install zsh plugins
git clone https://github.com/zsh-users/zsh-autosuggestions "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-autosuggestions"
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting"
git clone https://github.com/jeffreytse/zsh-vi-mode "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/zsh-vi-mode"
git clone https://github.com/unixorn/fzf-zsh-plugin.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fzf-zsh-plugin"

# set zsh as default shell
chsh -s "$(which zsh)"
```

> Change powerlevel10k theme with `p10k configure` if necessary

### Linux config file placement

```bash
# clone repo first
mkdir -p ~/src && cd ~/src
git clone https://github.com/<your-user>/dotfiles.git
cd dotfiles

# copy i3 config
mkdir -p ~/.config/i3
cp ~/src/dotfiles/i3/config ~/.config/i3/config

# copy shell config
cp ~/src/dotfiles/zsh/zshrc ~/.zshrc

# copy Powerlevel10k config 
cp ~/src/dotfiles/powerlevel10k/.p10k.zsh ~/.p10k.zsh

# copy terminal config
mkdir -p ~/.config/kitty
cp ~/src/dotfiles/kitty/kitty.conf ~/.config/kitty/kitty.conf

# copy tmux config
cp ~/src/dotfiles/tmux/tmux.conf ~/.tmux.conf

# optional vim config
mkdir -p ~/.vim_runtime
# use the full vim runtime install if desired
```

Then reload your i3 session or log out and back in:

```bash
# reload i3 config
i3-msg reload
```
