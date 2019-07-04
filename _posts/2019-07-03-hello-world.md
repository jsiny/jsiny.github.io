---
layout: post
title: "Hello World"
date:   2019-07-03 10:28:08 +0200
permalink: hello-world
categories:
  - Life

tags:
  - Blogging
  - Jekyll
  - Medium
---

> It's alive!

After a sleepless night, several gallons of tears and dozens of hours spent 
browsing stackoverflow, my new blog is now live 🌈

I'm not exactly new to blogging, but this is the first time I'm wandering away
from Wordpress. Oh boy, that was *difficult*.

## Why would I do that?

It all came down to one of my dearest colleague ranting about Medium.
I had just wrote [my first Medium post](https://medium.com/@juju.siny/my-study-habits-ae5c778b5a14)
(and was pretty pleased with myself), when he told me:

> I like your post, but why would anyone pay to read blog posts that could be 
found somewhere else, without any added value to the reading experience?

Admittedly, he's a grumpy old man, but as I'm not too fond of the new 
Medium paywall either, I thought he had a point.

Anyway, I had wanted to create a "professional" blog for ages, and thought that
my 3 months of consecutive programming might be enough to create a "real"
blog, away from traditional CMS.

Looking back, I *may* have bitten more than I could chew. No regrets though, 
the learning experience was well worth it.

## How I did it

Initially, I tried to set up a blog through [Hugo](https://gohugo.io/),
because I had read somewhere that their loading time was exceptionally fast,
and (let's be honest) because their templates were stunning.

However, I failed miserably. It seemed that whatever I did, my Cloud9
environment refused to accept `Homebrew`. 

My ego a little bruised, I looked up alternatives and found another
static-site generator: [Jekyll](https://jekyllrb.com/).
* Good news: it's in Ruby! I can finally grasp what's happening 
under the hood 🙌 Hugo, on the other hand, is written in Go and therefore
looks like gibberish to the beginner that I am.
* Bad news: Jekyll seems a bit ouf of fashion, and most resources about
it are somewhat dated. Most templates or blog posts are based on earlier
versions of Jekyll, therefore I encountered a couple of version issues.

The biggest difficulty arose when I tried escaping the dry 
[Minima](https://jekyll.github.io/minima/) default Jekyll template.
Apparently, there are some layout naming issues between templates
and Github pages that made transitions difficult.

A bit lost, I tweaked my `_layout` and `_includes` a lot, heavily drawing
inspiration from [Ryan Kozak](https://github.com/d0n601/ryankozak.com)
and [Laura Tebben](https://github.com/ltebben/ltebben.github.io)'s 
public repositories (thank god for public repositories), and finally
managed to install the [Hydeout](https://github.com/fongandrew/hydeout) theme 🍾

My next challenge will be to buy and set up my first domain (bye bye ugly
`github.io` domain name, you will be missed) ...but this is for another day.
