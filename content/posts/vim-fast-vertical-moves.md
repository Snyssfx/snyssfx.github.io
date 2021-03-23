+++ 
draft = false
date = 2021-03-21T18:59:00+03:00
title = "vim vertical moves"
slug = "" 
tags = ["vim", "include", "go", "golang"]
categories = []
thumbnail = "images/tn.png"
description = ""
+++

Recently I've read [a great article](https://vimways.org/2018/death-by-a-thousand-files/) about moving around files in vim.
The author says you could move between files faster with using `:edit`,
`:find` command with setting `include` option or `includeexpr` func when imports of language are
rather different from usual project structure.

I don't find the `:find` vim command useful for Go programming since you
should include `$HOME/pkg/mod` in `path`, and search for file is pretty slow at this point.
Neither an `include` option is useful, since Go has `gopls` language server and
it's easy to go-to-definition of a file or variable.
Also the package syntax in Go has github prefixes, and I cannot google `includeexpr` for Go.

What I find useful is command `:ijump /part_of_include` or faster `:ij /part_of_include`.
It allows user to jump to the first include containing `part_of_include` name.
It's faster then search one of the package usage and then go-to-definition,
since you don't have to jump twice.
I wonder if such a command exists for go-to-definition of 1 variable.
