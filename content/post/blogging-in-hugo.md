+++
date = "2016-08-30T22:00:43-04:00"
draft = false
title = "Blogging in Hugo"

+++

Hugo is a "Fast & Modern Website Engine" written in the Go programming
language.  It's what I've chosen to write this blog in because, well, it:

  * is new(ish)
  * has an [active community](https://github.com/spf13/hugo)
  * is relatively simple
  * can deploy easily to [GitHub Pages](https://pages.github.com/) (free hosting yo!)
  * is fast
  * has some [beautiful, modern, responsive (and might I add, free) themes](http://themes.gohugo.io/)
  * is written in [Go](https://golang.org/), which I kinda wanted to learn (and started at the Googs)

This post is really for me since I just started using this lovely blogging
engine and want to remember how to, well, use it.

This post also assumes you've already downloaded [Hugo](https://gohugo.io/),
created the base blog directory, and added a theme.  The below are just bits
plucked directly from the [Hugo Quickstart Guide](https://gohugo.io/overview/quickstart/).


## Step 1: Create the Markdown File

From within the local blog directory, create a new blank post as such:

`hugo new post/good-to-great.md`


## Step 2: Write the Post

Well, this is the easy part.  Write the dang post using markdown!


## Step 3: Preview the Post Locally

To preview the draft, run the following:

`hugo server --theme=hugo-future-imperfect --buildDrafts`

And then visit [http://localhost:1313/](http://localhost:1313/)

## Step 4: Undraft the Post

All looks good?  Undraft the post:

`hugo undraft content/post/blogging-in-hugo.md`

Alternatively, at the top of the markdown file in the TOML section, just
change `draft = true` to `draft = false`.

## Step 5: Deploy to GitHub Pages

You need to do a little magic to set up the git respository and connect it to
your account; please see the official [QuickStart tutorial](https://gohugo.io/overview/quickstart/)
for that.

Once set up, you just 

```sh
rm -rf public

git submodule add -b master git@github.com:getup8/getup8.github.io.git public
``

