+++ 
draft = false
date = 2021-04-05T14:31:48+03:00
lastmod = 2021-04-11T14:31:48+03:00
title = "lua programming trick for neovim scripting"
description = "How to effectively program on lua language for neovim"
slug = "" 
tags = ["neovim", "lua", "ctags", "lsp"]
keywords = ["vim", "neovim", "lua", "init.lua", "ctags", "lsp", "sumneko"]
categories = []
thumbnail = "images/tn.png"
+++

__TL;DR__ you can generate __ctags__ for go-to-definition in lua code and explore sources for better, for example, lsp configuring.  
You can't go-to-definition with __sumneko__ and other language servers for lua.  
The instruction of how to use __ctags__ is below.

### Introduction and lua

I'd like to share the one trick for neovim programming.  
Recently I've found out that you can rewrite (almost) all your neovim scripting code to lua language.  
And it turns out to be the smallest and simplest language possible.  
It has:
- control flow statements like conditions and for loops;
- anonymous functions;
- and tables (aka map or dict in other languages)

Tables are also great like the language itself:  
with tables you can do everything you need for basic neovim scripting 
like mappings,  
nested options and complex function arguments for neovim API.

Also all of the newest neovim plugins like __neovim-native lsp__,  
__telescope.nvim__ for fuzzy finding everything in your code and  
__treesitter__ for semantic syntax highlighting have lua setup support,  
so I decided to give it a try.

### ctags for lsp configuration

One of the challenges I met was customizing native __language server protocol__ for neovim.  
I want to create a command that opens type definition in vertical split,  
so I can see a function or a struct signature.

However when I tried to see how the basic `vim.lsp.buf.type_definition()` handler works,  
I failed to go to definition of the function, since __sumneko__ language server can't do it,  
neither is __lua-language-server__ (another LS for lua).  

So I solve it by creating `ctags` file, and use tag commands to
explore neovim sources.  

Overall, you should do the next steps for go-to-definition of lsp sources:
1. install `ctags` (you can use the maintained fork `universal tags`)
1. go to neovim config directory where the `init.lua` file is located.
1. generate `ctags` file with including neovim runtime files:
```py {linenos=false}
ctags -a /usr/share/nvim/runtime/lua/**/*.lua **/*.lua
```
4. open `init.lua` and type `:tag /type_definition`

The last command allows you to jump to a tag that have only part of the full name.  
It is necessary because __ctags__ generates tags with internal module name,  
so jumping to the tag with `CTRL-[` don't do a trick.
