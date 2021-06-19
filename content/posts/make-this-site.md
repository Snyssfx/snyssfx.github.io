+++ 
draft = false
date = 2021-03-20T19:16:21+03:00
lastmod = 2021-03-22T18:16:21+03:00 
title = "How to make a site using Hugo, Github Actions and pages"
description = "How to make a personal blog using hugo and github actions"
keywords = ["site", "personal", "blog", "hugo", "markdown", "github", "actions", "pages"]
tags = ["site", "blog", "hugo", "markdown", "github"]
slug = "" 
categories = []
thumbnail = "avatar.jpeg"
+++

This site was build with hugo, Github Actions, Markdown pages and a drop of love. Here is a couple of links I used:
- [hugo](https://github.com/gohugoio/hugo) is a static site generator, also see [a quick start guide](https://gohugo.io/getting-started/quick-start/)
- [Github Actions](https://github.com/features/actions) is a CI/CD building blocks for Github
- [Github Pages](https://pages.github.com/) is a free hosting for static websites
- You can setup hugo with Github Actions and Pages using [this link](https://gohugo.io/hosting-and-deployment/hosting-on-github/#readout)
- Posts can be edited as Markdown documents, syntax cheat sheet is [here](https://www.markdownguide.org/basic-syntax/)
- To be loved you should be nice.

Also, I replace `--minify` flag in [my Actions file](https://github.com/Snyssfx/snyssfx.github.io/blob/main/.github/workflows/gh-pages.yml#L24) from the guide with `-D`, since the old command couldn't generate new pages
(UPD: `-D == --buildDrafts`, so you should not mark posts as drafts
and everything will be OK with the default configuration)

Here is the CLI commands for hugo (also see [cheat.sh](https://cheat.sh/hugo)):
```py
hugo new site blog              # create directory 'blog' with site skeleton
hugo new posts/my-first-post.md # create first post blog
hugo server -D                  # start a local server with hot reloading
hugo -D                         # build site
```
