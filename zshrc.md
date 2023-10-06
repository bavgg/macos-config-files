# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

#
# ███████╗███████╗██╗  ██╗██████╗  ██████╗
# ╚══███╔╝██╔════╝██║  ██║██╔══██╗██╔════╝
#   ███╔╝ ███████╗███████║██████╔╝██║
#  ███╔╝  ╚════██║██╔══██║██╔══██╗██║
# ███████╗███████║██║  ██║██║  ██║╚██████╗
# ╚══════╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝
#
# ZSH Config File by Arfan Zubi



# Aliases
alias q='exit'
alias ..='cd ..'
alias lc='ls -t -A'
alias t='tree'
alias rm='rm -v'
#alias open='xdg-open'

alias sv='sudo nvim'

alias gs='git status'
alias ga='git add -A'
alias gc='git commit'
alias gpull='git pull'
alias gpush='git push'
alias gd='git diff * | bat'
alias gl='git log --stat --graph --decorate --oneline'

alias pu='sudo pacman -Syu'
alias pi='sudo pacman -S'
alias pr='sudo pacman -Rsu'
alias pq='sudo pacman -Qe'
alias autoclean='sudo pacman -Qtdq | sudo pacman -Rns -'

alias b='bat'
alias rr='ranger --choosedir=$HOME/.rangerdir; LASTDIR=`cat $HOME/.rangerdir`; cd "$LASTDIR"'
alias z='zathura'

# System aliases
alias standby='xset dpms force standby' 

# Colored output
#alias ls='ls -laGH --color=auto'
#alias diff='diff --color=auto'
#alias grep='grep --color=auto'
#alias ip='ip --color=auto'

# Colored pagers
export LESS='-R --use-color -Dd+r$Du+b'
export MANPAGER='less -R --use-color -Dd+r -Du+b'
#export MANPAGER="sh -c 'col -bx | bat -l man -p'"

# Setting Default Editor
export EDITOR='nvim'
export VISUAL='nvim'

# File to store ZSH history
export HISTFILE=~/.zsh_history

# Number of commands loaded into memory from HISTFILE
export HISTSIZE=1000

# Maximum number of commands stores in HISTFILE
export SAVEHIST=1000

# Setting default Ranger RC to false to avoid loading it twice
export RANGER_LOAD_DEFAULT_RC='false'



# Loading ZSH modules
autoload -Uz compinit

zstyle ':completion:*' matcher-list 'm:{a-z}={A-Za-z}'
zstyle ':completion:*' menu select
zstyle ':completion::complete:*' gain-privileges 1
zstyle ':completion:*' rehash true                      # Rehash so compinit can automatically find new executables in $PATH
zstyle ':vcs_info:git:*' formats 'on %F{red} %b%f '    # Set up Git Branch Details into Prompt

compinit
_comp_options+=(globdots)

# Load Version Control System into Prompt
autoload -Uz vcs_info
precmd() { vcs_info }

# Prompt Appearance
#setopt PROMPT_SUBST
#!/bin/bash
#!/bin/bash

# Oh-my-zsh
# ZSH_THEME="powerlevel10k/powerlevel10k"
ZSH_THEME="eastwood"
source ~/.config/oh-my-zsh/oh-my-zsh.sh
#plugins=()


# ZSH Autosuggestions
source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh

# ZSH Syntax Highlighting - must be at the end of .zshrc!
source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.

# Opening file with specific application.
mkd() {
    open -a /Applications/MacDown.app "$1"
}

clion() {
  open -a "/Applications/CLion.app/" "$1"
}

code() {
  open -a "/Applications/Visual Studio Code.app/" "$1"
}

ai() {
  curl -s https://free.churchless.tech/v1/chat/completions \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
      "model": "gpt-3.5-turbo",
      "messages": [{"role": "user", "content": "'"${1}"' + \" your answer will be formatted in markdown code\""}],
      "temperature": 0.7
    }' | jq -r '.choices[0].message.content' > ai_result.md
}

pai() {
  curl -s https://free.churchless.tech/v1/chat/completions \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $OPENAI_API_KEY" \
    -d '{
      "model": "gpt-3.5-turbo",
      "messages": [{"role": "user", "content": "'"${1}"'"}],
      "temperature": 0.7
    }' | jq -r '.choices[0].message.content' > code.py
}

