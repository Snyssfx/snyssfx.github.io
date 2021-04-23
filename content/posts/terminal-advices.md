+++ 
draft = false
date = 2021-04-23T9:56:31+03:00
lastmod = 2021-04-23T21:56:31+03:00
title = "Terminal productivity advices"
description = "Skills I find useful for speeding up a terminal workflow"
slug = ""
authors = []
tags = ["zsh", "bash", "terminal"]
keywords = ["zsh", "bash", "terminal", "git", "cd"]
externalLink = ""
series = []
+++

I'd like to show some of my terminal tricks that can boost your productivity in both everyday programming and related stuff.  
However, I'll do it in the next blogpost, since they are just examples of how to combine basic terminal skills,  
so firstly I should describe skills that helps me to develop the workflow suited for my everyday usage.  
I try to sort the skills from most important to less.  
Some of them are obvious and boring, others are super advices with modern terminal programs.

## Terminal skills
#### 1. practice 10-finger typing (most useful and boring point!)
It speeds up your typing in the terminal and coding!  
Personally I used https://www.typingstudy.com/  
It was super boring, but now I can type and code faster, so it was worth it!  

#### 2. __learn pipes__ (and maybe subcommands)
Most programs in bash are either:
  - produce strings and lines
  - convert (= maps) them to another lines 
  - filter them.

All of it you can combine with pipes!  
see https://cheat.sh/bash/pipes or https://learnxinyminutes.com/docs/bash/ for full reference.

#### 3. __learn how to customize .bashrc or .zshrc__
You can sets plugins (what I use is below), aliases (also below) and env vars  
(this one you can see examples in the next point, I promise!), all of them are pretty dope.  
I use oh-my-zsh plugin system, so I can find some useful ones [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

#### 4. __learn hotkeys for the terminal__
It speeds up your traversing. Some of them are:
  - `Ctrl-w`, `Ctrl-a`, `Ctrl-e`, `arrows + Ctrl`;
  - setup `$EDITOR` env to, for example, `vim` or `vscode`, so you can edit the command with `Ctrl-x Ctrl-e` quickly.

See https://cheat.sh/bash/shortcuts

#### 5. __know how to use standard programs__
`echo`, `cat`, `find`, `grep`, `xargs`, `sed`, `awk`, `curl`, `wget`, `ls` are all super useful for combining in pipelines!  
You can find references [here](https://www.educative.io/blog/bash-shell-command-cheat-sheet).

#### 6. __try not standard programs__
Programs that you can `apt-get`, `brew install` and so on.  
They are colorize output and make terminal cooler:
  - `rg`, `sd`, `fd`, `exa`, `bat`, `delta`, `httpie` instead of `grep`, `sed`, `find`, `ls and tree`, `cat`, `diff` and `curl` respectively.

Personally I'm not using all of them, but it's certainly worth to try them.  
Go to github for the full descriptions of each one.

#### 7. __learn aliases and how to create simple functions__
It's better to hide the complexity of the nasty bash syntax into things you know!

#### 8. __learn how to store your .bashrc and .zshrc in git repo__
If the job gives you a laptop for work, you can just clone all your cool aliases!  
I use [dotfiles project](https://github.com/mathiasbynens/dotfiles) and store there bash scripts, themes, vim keybindings and more!

----
Once it's done, it all enables to combine commands and aliases, and also enables to execute complex tasks.  
Also you can send _macroses_ that you write to your colleagues without screenshots and descriptions where the right button is located in the UX!

