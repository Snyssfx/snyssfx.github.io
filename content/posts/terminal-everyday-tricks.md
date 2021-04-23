+++ 
draft = true
date = 2021-04-23T12:56:31+03:00
lastmod = 2021-04-23T12:56:31+03:00
title = "My terminal tricks for everyday usage"
description = "Show some of my terminal tricks from my zsh setup"
slug = ""
authors = []
tags = ["zsh", "bash", "terminal"]
keywords = ["zsh", "bash", "terminal", "git", "cd"]
externalLink = ""
series = []
+++

### My terminal tricks
Now I can describe some of the tricks I use to make terminal more convenient:
1. __`history` command__
    - you can count what commands you type the most frequently and then rewrite them or relearn not to type them at all!
    - `history -n | sort | uniq -c | sort -n | tail -5`
2. __find command with fuzzy search, not just `Ctrl-R` search__
    - `` `history -n | fzf` `` - `fzf` is super useful when you need to search one thing!
3. __plugins from oh-my-zsh that adds aliases__
    - Personally I use `git`, `kubectl` and `golang` plugins a lot, so the plugins allows me to type `gsb` instead of `git status`
4. __`fasd` plugin and program__
    - `fasd` maintains most recent used cache for directories and files and has pretty short aliases
    - you can write `z part of dir` to jump to `/home/snyssfx/part/of/long/long/directory`
    - works fine with `$EDITOR` env: `v part of dir` for `$EDITOR /also/part/of/long/dir/path`
5. __calculator in the terminal__
    - I can write `calcc '(20+2.5)/7'` for fast calculation
```python3
function calcc {
  calc <<< "$@; quit"
}
```
6. __fastly edit pre-commit hooks__
```py3
PRE_COMMIT=.git/hooks/pre-commit
alias precommited="touch $PRE_COMMIT && chmod +x $PRE_COMMIT && vim $PRE_COMMIT"
```
7. __copy some command to clipboard__
```py3
alias xclipp='xclip -selection clipboard'
```
8. __(only for zsh) hook `cd` and `fasd` commands to show `ls` or `git status` on entering directory__
```py3
function chpwd() {
    emulate -L zsh
    if [ -n "$(git rev-parse --git-dir 2>/dev/null)" ]; then
        git status
    else
        ls
    fi
}
```
9. __Search your clipboard in Google__
    - I use i3 tiling manager and can bind bash scripts to hotkeys:
```py3
bindsym $mod+F2 exec "xclip -out -selection clipboard | sed \\"s,^,'https://duckduckgo.com/\\?q\\=,\\" | sed \\"s,$,',\\" | xargs xdg-open"
```
