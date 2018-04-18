---
layout: post
title: "How to Set Up Jekyll to Publish to Github Pages"
date: 2015-05-25 21:23:00
categories: 
tags: jekyll, github_pages, github
---

While setting up the publishing environment for this blog, I found it surprisingly difficult to find accurate, straightforward information about configuring Jekyll to publish to a Github User Page.

First, the basics.  A Github User Page is just a regular repository in your Github account that has a special name (\_username\_.github.io), which gets automatically recognized/converted into your Github User Page.  That repo has to have, at a minimum, a file called index.html at the top level for this to work.  

You don't have to use Jekyll to create your Github User Page.  All you have to do is to create a repository by that name and either manually create an index.html or go into the settings of that repository and you'll see some special options for using the site building tools integrated right into the Github interface.  However, under the hood Github uses Jekyll to build their Github Pages, so it's easy for users to use Jekyll explicitly to manage their Github User Page if they'd like to.

So, back to my setup story... I wanted a very typical setup.

1. Add and edit blog posts locally on my laptop.
2. Preview them there.
3. Publish to the production Github Page site when ready.

This Github Pages integration feature is prominently listed on Jekyll's front page, so I thought it would be simple, but I was unable to find a step-by-step guide on doing this in one place.  I pieced together info from Github, Jekyll, the internet at large, and semi-informed guessing to produce this set of instructions.  Without further ado...

## Setting Up Jekyll to Publish to Github Pages

This recipe assumes you have a working Ruby environment and git command.  If you don't, do that first.

1. `gem install github-pages` (Do this INSTEAD of gem install jekyll, this will install a jekyll that matches the Github Pages environment, so you avoid nasty surprises when publishing to Pages)
2. `jekyll new my-new-website`
3. `cd my-new-website`
4. `git init` to turn your Jekyll site into a git repository.
5. Go to Github, and in your account create the repository called `username.github.io`
6. Back on your local machine, do `git remote add origin https://github.com/_username_/_username_.github.io.git` to add the Github Pages area as a remote repo for your Jekyll site (replacing \_username\_ with your username, of course.)
6. Edit \_config.yml to add `baseurl: ""` and `url: "http://\_username\_.github.io` entries. The internet might tell you to put something like "/username.github.io" in the baseurl key - the internet is _wrong_.  Don't give any value to baseurl unless you're specifically publishing your Jekyll site in a subdirectory of your Github User Page site.  Bad advice on this cost me a lot of time.
7. `git add .` and `git commit -a` to add all files and make your initial commit of the site.
8. `git push` to upload the site to Github.
9. http://\_username\_.github.io/ should now show your site.

This should get you a minimal setup.  There are other things you may want to do. For instance, I changed my remote origin setup to use SSH and my SSH key instead of https access, but that's beyond the scope of this tutorial (and not hard to figure out either).  I also wanted a custom domain name (blog.franfabrizio.com, as you can see), which was a simple matter of setting up a CNAME in my domain DNS to point blog.franfabrizio.com to franfabrizio.github.io.

Now, I can create blog content and access all of the Jekyll functionality in the local my-new-website directory, and I can use `jekyll serve --force_polling` to start up a server that will preview the site locally at http://127.0.0.1:4000/ and auto-regenerate any files that get added or edited.  Publishing it out to Github Pages is a simple matter of `git commit -a` and `git push`.  In essence, you're pushing Jekyll source files over to Github, which then runs Jekyll on the files on their end to produce the same site you're seeing locally.

One note to this setup: Github Pages disables Jekyll plugins, so any extra plugins you've installed locally will not work on the Github Pages side.  To use plugins, you have to run Jekyll locally and push the generated site files instead of the Jekyll source files.  That is not something I've needed to tackle, but there is information about it out in Googleland and it shouldn't be too hard to figure out.




