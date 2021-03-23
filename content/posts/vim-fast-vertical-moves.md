+++ 
draft = false
date = 2021-03-21T18:59:00+03:00
title = "vim ijump command"
slug = "" 
tags = ["vim", "include", "go", "golang", "ijump", "include"]
categories = []
thumbnail = "images/tn.png"
description = "Describes :ijump command from vim"
+++

Recently I've read [a great article](https://vimways.org/2018/death-by-a-thousand-files/) about moving around files in vim.
The author says you could move between files faster with using `:edit`
and `:find` commands. Also for `:find` one you should set `include`
option or `includeexpr` func when imports of language are
rather different from usual project structure.

I don't think the `:find` command is useful for Go programming since you
should include `$HOME/pkg/mod` in `path`, and file searching is pretty slow at this point.
Neither an `include` option is useful, since Go has `gopls` language server and
it's easy to go-to-definition of a file or variable.
Also the package syntax in Go has github prefixes, and I cannot google `includeexpr` for Go.

What I find useful is command `:ijump /part_of_include` or faster `:ij /part_of_include`.
It allows the user to jump to the first include containing `part_of_include` name.
It's faster then searching one of the package usage and then go-to-definition of the one,
since you don't have to jump twice.

I wonder if such a command exists for go-to-definition of 1 variable for LSP, like the great `:tag /part_of_tag`. Do you know any?
