---
layout: post
title: Using Metaprogramming to Pass an Argument to a Rails Module
date: 2020-04-06 15:35 +0200
last_modified_at: 2020-04-07 10:25 +0200
permalink: rails-metaprogramming-pass-argument-to-module
description: Here's a detailed example of passing an argument to a Ruby on Rails module through some metaprogramming
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Ruby
tags: 
- Rails
- Ruby
- Metaprogramming
- Ruby on rails
- Module
- How-To
---

**Refactoring** is my favorite hobby. Nothing feels quite as satisfying than 
extracting some common methods to an elegantly named module.

Quickly though, I usually run into trouble - how exactly am I supposed to pass an 
argument to a module in Ruby? The answer is: through some **metaprogramming**!
(*such a scary word*)

<!--more-->

Let's draft up a (somewhat contrived) example using Ruby on Rails.

Imagine a Facebook-like application with the following models and `Likeable` 
module:

<script src="https://gist.github.com/jsiny/0baf8980901e299d9534e0d2fae828eb.js"></script>

Through the `Likeable` module, we can now retrieve the total number of likes for
any instance of the `Image` (or `Video`) class with the following pattern: 
`Image.find(params[:id]).total_likes`.

That's pretty neat.

Now, let's assume that the two classes handle differently which users get 
notified when a new like is submitted. As it's related to likes, we'd like to
include this behaviour within the `Likeable` module. 

However, Ruby does *not* provide an easy way to pass an argument to a method
defined within a module. We could of course add some conditional logic to the
module method, but that would become messy quickly as we create other 
classes mixed in the `Likeable` module.

<script src="https://gist.github.com/jsiny/699caa3540195819b844194b0f167412.js"></script>

Let's *not* do that.

Instead, we'd like to be able to directly define who should be notified for 
each class within the model, like so:

<script src="https://gist.github.com/jsiny/15bb9e42c214db82cdfee5a1800f2d1d.js"></script>

Turns out, we can use some metaprogramming to mimic the passing of an argument:

<script src="https://gist.github.com/jsiny/40b97c1ea25599c0c468b6cfcd322716.js"></script>

Here's what this code does:
- Lines 5-7: when the module `Likeable` is included within the class, the 
(Rails) class attribute `users_to_be_notified` is created. 
- Lines 18-22: Within the `Likeable` module is defined the class method 
`notifiable_users`. This method sets `users_to_be_notified` to the
parameters.
- Line 34: `notifiable_users :creator, :tagged_users`: the `notifiable_users` 
class method is called with two arguments (representing ActiveRecord attributes).
This sets the class attribute `users_to_be_notified` to `[:creator, 
:tagged_users]` (for the `Video` class).
- Line 14: we retrieve the values behind `:creator` and `:tagged_users` for 
the specific instances of the class, and notify them individually.

You can now create a new class and easily define who gets notified for new
likes:

<script src="https://gist.github.com/jsiny/af94934e767fa0da4f721544278628d4.js"></script>

There you go!