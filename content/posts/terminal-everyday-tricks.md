+++ 
draft = false
date = 2021-05-12T12:56:31+03:00
lastmod = 2021-05-12T12:56:31+03:00
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
In [the previous post](https://snyssfx.github.io/posts/terminal-advices/) I wrote how to master the terminal, now I can show a few tricks I use to simplify everyday programming life.

#### __History command__
You can count what commands you type the most frequently and then rewrite them or relearn not to type them at all.
You can see the commands using this command:  
`history -n | sort | uniq -c | sort -n | tail -5`

#### __Find the command with fuzzy search__
It's better then the reverse search with `Ctrl-R`,
`fzf` is super useful when you need to search one thing, and you can execute the command because of the backticks:  
`` `history -n | fzf` `` 

#### __Plugins from oh-my-zsh that adds aliases__
Personally I use `git`, `kubectl`, `golang` and `docker-compose` plugins a lot, so they allows me to type `gsb` instead of `git status`.  

#### __`fasd` plugin and program__
`fasd` maintains the most recent used cache for directories and files and has pretty short aliases.  
You can write `z part of dir` to jump to `/home/snyssfx/part/of/long/long/directory`.  
Also works fine with `$EDITOR` env: `v part of dir` for `$EDITOR /also/part/of/long/dir/path/file.txt`.

#### __Calculator in the terminal__
I can write `calcc '(20+2.5)/7'` for fast calculation having this function in my `.zshrc`:
```python3
function calcc {
  calc <<< "$@; quit"
}
```
#### __Fastly edit pre-commit hooks__
```py3
PRE_COMMIT=.git/hooks/pre-commit
alias precommited="touch $PRE_COMMIT && chmod +x $PRE_COMMIT && vim $PRE_COMMIT"
```
#### __Copy the output of the command to clipboard__
You can type `some_command | xclipp` with this handy alias:
```py3
alias xclipp='xclip -selection clipboard'
```
#### __(Only for zsh) hook `cd` and `fasd` commands to show `ls` or `git status` on entering directory__
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
#### __Search your clipboard in Google__
I use i3 tiling manager and can bind bash scripts to hotkeys. With this shortcut I can open the search engine (DuckDuckGo in this example) with something that I store in the clipboard:
```py3
bindsym $mod+F2 exec "xclip -out -selection clipboard | sed \\"s,^,'https://duckduckgo.com/\\?q\\=,\\" | sed \\"s,$,',\\" | xargs xdg-open"
```

#### __Open GUI tool from the terminal and close the terminal__
It's hard to open some GUI programs and closes the terminal at the same time, because the GUI is created as the child process and if you close the terminal, you also close the program. So I use a little hack that separate the GUI process from the terminal and then closes the window:
```py3
# i3-specific func for background task
# usage: $cmd --with-lots-of-args &; bgr
function bgr() {
    disown && i3-msg "kill"
}
```

### Conclusion
It's super handy to know the terminal tool, because you can hack your system and make your life not so bothersome. Be kind and laugh more, don't spend the time on the repetitive tasks!
