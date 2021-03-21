+++ 
draft = true
date = 2021-03-20T19:16:21+03:00
title = "How to make a site like that"
slug = "" 
tags = ["site", "personal", "blog", "hugo", "markdown", "github", "actions"]
categories = []
thumbnail = "avatar.jpeg"
description = "How to make a personal blog using hugo and github actions"
+++

This site was build with hugo, Github Actions, markdown pages and a drop of love. Here is a couple of links I used:
- [hugo](https://github.com/gohugoio/hugo) is a static site generator, also see [a quick start guide](https://gohugo.io/getting-started/quick-start/)
- [Github Actions](https://github.com/features/actions) is a CI/CD building blocks for Github
- [Github Pages](https://pages.github.com/) is a free hosting for static websites
- You can setup hugo with Github Actions and Pages using [this link](https://gohugo.io/hosting-and-deployment/hosting-on-github/#readout)
- Posts can be edited as markdown documents, syntax cheatsheet is [here](https://www.markdownguide.org/basic-syntax/)
- To be loved you should be nice

Also I replace `--minify` flag in [my Actions file](https://github.com/Snyssfx/snyssfx.github.io/blob/main/.github/workflows/gh-pages.yml#L24) from the guide with `-D`, since the old command couldn't generate new pages.

Here is the CLI commands for hugo:
```zsh
$ hugo new site blog              # create directory 'blog' with site skeleton
$ hugo new posts/my-first-post.md # create first post blog
$ hugo server -D                  # start a local server with hot reloading
$ hugo -D                         # build site
```
