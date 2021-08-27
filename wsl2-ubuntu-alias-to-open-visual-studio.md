---
layout: default
date: 2021-08-21
title: WSL2 Ubuntu Alias to Open Visual Studio
tags: [WSL2, til, published]
---

I recently reinstalled WSL2 on my Windows machine, and I'm trying to work exclusive through that shell, even when I open Windows-based applications.

VS Code already does this really well, and the integration is great. I, however, work in Visual Studio somewhat regularly, so I wanted the same type of experience as `code .`.

Here's my `.zshrc`:

```bash
export PATH="/mnt/c/Program Files (x86)/Microsoft Visual Studio/2019/Enterprise/Common7/IDE/:$PATH"

if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

export ZSH="/home/tony/.oh-my-zsh"
ZSH_THEME="powerlevel10k/powerlevel10k"

plugins=(git zsh-syntax-highlighting zsh-autosuggestions aws dotnet terraform vault gh)

source $ZSH/oh-my-zsh.sh

cd ~

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

### Fix slowness of pastes with zsh-syntax-highlighting.zsh
pasteinit() {
  OLD_SELF_INSERT=${${(s.:.)widgets[self-insert]}[2,3]}
  zle -N self-insert url-quote-magic # I wonder if you'd need `.url-quote-magic`?
}

pastefinish() {
  zle -N self-insert $OLD_SELF_INSERT
}
zstyle :bracketed-paste-magic paste-init pasteinit
zstyle :bracketed-paste-magic paste-finish pastefinish
### Fix slowness of pastes

alias vs="devenv.exe *.sln > /dev/null 2>&1 &"
```

Note that I add the Visual Studio 2019 path to the `$PATH` environment variable, then I set an alias at the top to fire up Visual Studio for the solutions in the current director with the `vs` alias. I added in the `> /dev/null 2>&1 &` to run it in the background and to pipe output and erros to `stdout`.