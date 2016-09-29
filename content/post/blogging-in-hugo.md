+++
date = "2016-08-30T22:00:43-04:00"
draft = false
title = "Blogging in Hugo"
description = "A guide to getting set up on Hugo and deploying to GitHub Pages."
tags = [ "hugo", "github", "blogging" ]
categories = [ "tech" ]

+++

[Hugo](https://gohugo.io/) is a "Fast & Modern Website Engine" written in the
Go programming language.  It's what I've chosen to write this blog in because,
well, it:

  * is new(ish)
  * has an [active community](https://github.com/spf13/hugo)
  * is relatively simple
  * can deploy easily to [GitHub Pages](https://pages.github.com/) (free hosting yo!)
  * is fast
  * has some [beautiful, modern, responsive (and might I add, free) themes](http://themes.gohugo.io/)
  * is written in [Go](https://golang.org/), which I kinda wanted to learn (and started at the Googs)


Below is a quick start guide to get blogging using Hugo and GitHub User Pages.
I assume you've downloaded and installed Hugo and have a GitHub account.

I also assume you've created the base blog directory, and added a theme.  There
are great instructions in the [Hugo Quickstart Guide](https://gohugo.io/overview/quickstart/).

So now you have Hugo locally and you're ready to actually get something on the
web!


## Step 1: Create the GitHub Respositories

The way I decided to do it was to create two separate GitHub respositories, one
to keep my raw Hugo source and then the GitHub Pages one to deploy the compiled
HTML to.

In my case, that meant setting up:

  1. https://github.com/getup8/getup8.github.io - my GitHub User Page
     respository and where we'll story the generated static files for the blog
  2. https://github.com/getup8/getup8-hugo for the Hugo source

Create both of those.  For the first, you'll want to follow the instructions
[here](https://pages.github.com/).


## Step 2: Set up Git and Local Directories

Now you'll want to set up local directories that will tie to each of these
repositories.  So create a directory named `blog` or something of that sort
and from within that directory run:

`git clone https://github.com/getup8/getup8.github.io`

and

`git clone https://github.com/getup8/getup8-hugo`

This will create and initialize two local repositories.  Easy peasy.


## Step 3: Set up Hugo

If you've followed the Hugo QuickStart guide, you have the Hugo directory
structure set up elsewhere and you've downloaded a theme, etc.  Copy those
files into your local source respository (e.g. `getup-hugo/`).

It should work just the same there as it was elsewhere.


## Step 4: Create a Blog Post

From within the local blog directory (`getup8-hugo`), create a new post by
running this on the command line:

`hugo new post/testing.md`


## Step 5: Write the Post

Well, this is the easy part.  Open that file (`getup8-hugo/content/post/testing.md`)
and write the dang post using markdown!  Maybe for now just put "Test" in the
content section.


## Step 6: Preview the Post Locally

To preview the draft, run the following:

`hugo server -t hugo-cactus-theme --buildDrafts`

And then visit [http://localhost:1313/](http://localhost:1313/)


## Step 7: Undraft the Post

All looks good?  Undraft the post:

`hugo undraft content/post/blogging-in-hugo.md`

Alternatively, at the top of the markdown file in the TOML section, just
change `draft = true` to `draft = false`.


## Step 8: Commit Your Changes and Push

```sh
# Add all files to staging
git add --all
# Check the status, make sure files have been added
git status
# Commit locally
git commit -m "Test post"
# Push to GitHub repository
git push -u origin master
```


## Step 9: Deploy to GitHub Pages

Almost there but you're not done yet.  This is the most important part.  We
now need to generate our static files and push them to our GitHub Pages
repository.

From within the blog source directory again, execute the following.

```sh
# Generate the static files with your chosen theme and most importantly,
# direct them to your *other* directory
hugo -t hugo-future-imperfect -d ../getup8.github.io

# Now move to that directory
cd ../getup8.github.io

# And commit all those files
git add --all
git commit -m "Test post"
git push -u origin master
```


## Fin!

With a little luck, when you browse to your blog's URL, you'll see your
beautiful test post.  Once you have it working, you can actually automate
Steps 8 and 9 (I automate Step 9) by creating a simple shell script.

Hope this was helpful, let me know if you have any trouble.
