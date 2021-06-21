+++ 
draft = false
date = 2021-06-18T14:09:24+03:00
lastmod = 2021-06-18T15:09:24+03:00
title = "Programs for fast access via terminal and my fasd configuration"
description = "How to access directories and files faster with fasd program"
slug = ""
tags = ["fasd", "z", "v", "autojump", "zoxide", "terminal", "cd"]
categories = []
externalLink = ""
series = []
+++

# Introduction
If you ever find yourself in a repetitive process of `cd` to another directory you have ever used, 
there is a family of programs you should learn of.  

The [`z`](https://github.com/rupa/z), [`autojump`](https://github.com/wting/autojump),
[`v`](https://github.com/rupa/v), [`fasd`](https://github.com/clvv/fasd) and
[`zoxide`](https://github.com/ajeetdsouza/zoxide)
terminal programs stores recently visited directories and files that you can `cd` into, 
open them with `$EDITOR` or `xdg-open` and use them as arguments to another commands (`mv`, `cp` etc).  

Next I will tell you about the differences and features of each one.

### References
- https://github.com/rupa/z
- https://github.com/rupa/v
- https://github.com/wting/autojump
- https://github.com/clvv/fasd
- https://github.com/ajeetdsouza/zoxide

---

### z
With `z`, you can `cd` into a directory by typing only a part of the path. 
You can use it to enter directories you are often used.
Before that you should enter some directories as usual and wait until `z` adds them to a local database.  

`z` holds a cache of directories you've visited based on 'frecency': it's a combined metric 
of frequency and recency of accessing a directory. 
The metric was initially developed by Mozilla, you can check details [here](http://devdoc.net/web/developer.mozilla.org/en-US/en/The_Places_frecency_algorithm.html).  
Examples:
```bash
z foo     # cd to most frecent dir matching foo
z foo bar # cd to most frecent dir matching foo, then bar
```

### autojump
`autojump` has the same functionality as `z` for jumping to a directory, 
but instead of `z` command it introduces `j` command and aliases that can `xdg-open` directories with a file explorer (Mac Finder, Windows Explorer, GNOME Nautilus, etc.).  
Examples:
```bash
j foo    # same as z foo
jc bar   # jump to a child directory of a current working dir
jo music # jump to a music dir and open it through a file explorer window
```

### v
As long as `z` stores directories, `v` stores files that has been accessed through `vim`: 
it parses `.viminfo` file that stores vim history, 
and you can quickly edit the file from anywhere in the terminal.  
Examples:
```bash
v            # list and choose from all files
v -0         # reopen most recently edited file
v foo bar    # edit first file matching foo and bar
v -c foo bar # choose files in current dir matching foo and bar
v -l foo bar # list and choose files matching foo and bar
```
Although it has the great vim support, it lacks the neovim way of storing history: neovim stores `shada-file` 
(you can look for more details in `:help shada-file` in neovim), 
and the file has a different syntax which cannot be parsed by `v`. 

### fasd
`fasd` is a compilation of `z`, `v` and `autojump` commands. It stores not only directories, 
but also files that are ordered by 'frecency' like in `z`. 
It comes with handy aliases: `f` for selecting files, `d` for selecting directories, and `a` for all.  
Also, it has first-class `zsh` support (like `z`), so you can complete other commands 
by passing `fasd` paths that are started with `,` (comma symbol).

Also like the `v` command it auto caches files from `.viminfo`, and like in `v` it doesn't work 
for neovim.
Examples:
```bash
v def conf # vim /some/awkward/path/to/type/default.conf
j abc      # cd /hell/of/a/awkward/path/to/get/to/abcdef
f js$      # list frecent files that ends in js, fzf-like bindings

vim `f rc lo`   # vim /etc/rc.local as a subcommand
vim ,rc,lo<Tab> # vim /etc/rc.local, it is autocompleted through zsh hooks
f -e vim rc lo  # vim /etc/rc.local, find a file and pass it to an executable (vim in this example)
```

### zoxide
`zoxide` works only for directories like `z`, but it also includes `cd` functionality, 
so you can `alias cd='zoxide'` and boost your productivity. Also, it is integrated with `fzf` 
command for faster searching through the stored cache.  
Examples:
```bash
z foo  # go to a directory whose path contains 'foo'
zi foo # interactive search through all 'foo' occurences with fzf program
```
---

# My fasd configuration
To sum up the review, you should choose between `fasd` and `zoxide`, since they implement other tools' features and add new ones.  

As for me, `fasd` incorporates all `z`, `v` and `autojump` features, while `zoxide` 
cannot allow me to access files which is crucial for a vim user.  

Users that don't often access files in the terminal could add `alias cd='zoxide'` in the `.zshrc` and 
play with the program for some time.  

Now I'm going to share my configuration that integrates [neo]vim and fasd more closely:  

First I want to use 'comma' functionality that auto completes fasd-cached files 
for other programs.
For this reason I install `fasd` plugin using oh-my-zsh.

Secondly, I wanted to open vim with the projects I'm working on as soon as I open the terminal.
For this purpose I have the handy alias-function in my `.zshrc`:  
```zsh
# jump to dir and fastly open it
function vi() {
    z $@ && vim .
}
```
For example, it allows me to type commands `vi gam` that opens a game project with vim.

Finally, since I'm using neovim, `v` features doesn't work out of the box, and it bothered 
me every time. 
So I find [the solution](https://github.com/clvv/fasd/issues/91#issuecomment-270817365)
that updates `fasd` cache every time neovim opens a file. Here is the lua version of it
(you can customize your neovim in both `vimscript` and `lua` languages, I choose the latter):
```lua
-- update fasd entries on buf enter
function _G.FasdUpdate()
   vim.api.nvim_exec([[
        if empty(&buftype) || &filetype ==# 'dirvish'
            call jobstart(['fasd', '-A', expand('%:p')])
        endif
   ]], true)
end
vim.api.nvim_exec([[
    augroup fasd
        autocmd!
        autocmd BufWinEnter,BufFilePost * lua _G.FasdUpdate()
    augroup END
]], true)
```
So now my development experience consists of opening a terminal and typing `vi proj` or `v file`
if I've ever used one of the project or the file. It's super handy, try it by yourself!

