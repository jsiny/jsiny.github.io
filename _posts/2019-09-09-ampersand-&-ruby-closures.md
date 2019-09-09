---
layout: post
title: What's up with the & (ampersand) in Ruby closures?
date: 2019-09-09 08:19 +0200
last_modified_at: 2019-09-09 17:14 +0200
permalink: ampersand-ruby-closures
description: A detailed explanation of the subtleties behind using the ampersand (&) in Ruby closures (blocks and Procs)
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Ruby
tags: 
  - Ruby
  - Ruby Quirks
  - Closures
  - Learning
  - Ampersand
  - Block
  - Proc
---

Quite surprisingly, the following Ruby program is correct:

```ruby
def first_method(&block)
  second_method(block)
end

def second_method(block)
  third_method(&block)
end

def third_method(&block)
  block.call
end

first_method { puts "hello!" }
# "hello!"
```

You might therefore notice that the `&` (ampersand) pops up and disappears 
pretty randomly in the above program. As it's pretty hard to wrap one's head 
around all this `&` madness, let's dive into this!

<!--more-->

* TOC
{:toc}
<hr>

## What's a closure?

In this post, we'll talk about **closures** (and in particular, *blocks* and
*Proc objects*). And as I like nothing more than a proper introduction, let's
first define a closure.

One of the "official-looking" (and pretty unhelpful) definition I have found
is the following:

> A closure is a first-class function that has lexical scope.

... 😒 (sigh)

It might help to consider the following instead:

> A closure is a 'bunch of code' that can be defined and saved for later use.

Additionally, a closure 'remembers' its surrounding context at the time it was
initialized, ie. it *binds* its environment (local variables, method
definitions, constants) to be sure to have everything it needs to run 
successfully.

In Ruby, closures are: Proc objects, blocks and lambdas.

{% include images.html file="closure.gif" 
  caption="Not exactly *that* type of closure though" 
  alt="Friends Serie Dialogue Closure" %}

Here, we'll only talk about blocks and Procs, and more specifically, how 
to call them from methods.

## Blocks

First, let's talk about *blocks*.

```ruby
[1, 2, 3].map { |n| n + 2 }
```

In the above program, `{ |n| n + 2 }` is the block. A block is an 'unnamed'
function that can be called implicitly or explicitly.

### Implicit Block-Calling

```ruby
def some_method
  puts "hi from the method"
end

some_method { puts "hi from the block!" }

# "hi from the method"
```

The above program only outputs the first string (`"hi from the method"`)
and somehow forgets about the second string (`"hi from the block!"`).

That's because even though we implicitly passed the block to the method, 
we didn't execute the block within the method. To do that, we'd need to 
*yield to the block* by using the keyword `yield`:

```ruby
def some_method
  puts "hi from the method"
  yield
end

some_method { puts "hi from the block!" }

# "hi from the method"
# "hi from the block!"
```

As a matter of fact, **all Ruby methods can implicitly take a block**, without
needing to specify the block in its argument list or even having to execute 
the block.

### Explicit Block-Calling

When we write a method definition, it can be relevant to explicitly
require a block. To do that, Ruby uses a `&` prepending the parameter's name:

```ruby
def some_method(&block)
  yield
end

some_method { puts "hi from the explicit block!" }
```

Here, `block` acts as a handle (a reference) for the block: within the method
definition, that block is no more an *unnamed* function. 

The `&` prefixed to `block` signals that any block passed to `some_method`
upon method invocation will be converted to a `Proc` object.

As such, we can do a bit more than simply *yield* to it:

```ruby
def some_method(&block)
  block.call
end

some_method { puts "hi from the explicit block!" }
```

As `block` now refers to a `Proc` object, we can invoke `call` on it. We can
also pass this object to another method like in our initial example:

```ruby
def first_method(&block)
  second_method(block)
end

# rest of the code omitted for brevity

first_method { puts "hello!" }
```

Here, the block `{ puts "hello"! }` is converted to a `Proc` thanks to the `&`
prefixed in the method definition, and assigned to the local variable `block`.
Then, a second method is invoked and the `Proc` object is passed to it as 
an argument.

Notice that we dropped the `&` in the `second_method` method invocation.

To sum up: in the context of a **method definition**, prepending the last 
parameter with an `&` indicates that the method takes an explicit block and that 
this block is converted to a `Proc` object (with a name) within the method body.

## The `&` within a method call

As a [Codewar addict](/codewars-kata-launch-school-109-oral-assessment),
I've had my fair share of time spent on coming up with "one-liners", aka
the shortest programs possible.

One of the tricks I use is the `&`:
```ruby
['a', 'b', 'c'].each(&:upcase!)
# ['A', 'B', 'C']
```

Somehow, this code:

```ruby
(&:upcase!)
```

...is converted to this code:
```ruby
{ |char| char.upcase! }
```

Here's the mechanism at play here (in the context of a **method invocation**):
* Ruby checks whether the object right after the `&` is a Proc:
  * If it is: great! Ruby uses the Proc object as it is
  * If it isn't, Ruby calls a `to_proc` method on the object, if such a method
  exists for that particular class. Fortunately, a `Symbol#to_proc` instance 
  method does exist. In our example, the `:upcase` symbol is therefore 
  converted to a `Proc` object.
* If the object is now a `Proc`, the `&` converts the `Proc` into a `block`. 

Let's go back to our initial example (and recall that the `first_method` 
converted the initial block to a `Proc` and passed that object to the 
`second_method`):

```ruby
def second_method(block)
  third_method(&block)
end
```

The `second_method` receives a `Proc` object, assigned to the local variable
`block`. Within the method body, a `third_method` is called, with `&block`
passed to it as an argument.

As we're here in the context of a **method invocation**, the `&` does the
following:

1. Checks whether `block` is indeed a `Proc` (which it is)
2. Converts the `Proc` into a block

## Explaining our initial example

We now have everything required to understand our initial example! Let's 
rewrite it with more self-explanatory names:

```ruby
def block_to_proc_method(&block_to_proc)
  proc_to_block_method(block_to_proc)
end

def proc_to_block_method(proc_to_block)
  call_the_block_to_proc(&proc_to_block)
end

def call_the_block_to_proc(&block_to_proc)
  block_to_proc.call
end

block_to_proc_method { puts "hello!" }
```

Let's explain the program step-by-step, thanks to our new understanding
of the subtleties behind the `&`:

* At first, the `block_to_proc_method` is invoked, with a block 
`{ puts "hello!" }` passed to it as an argument.
* The block `{ puts "hello!" }` is converted to a `Proc` object thanks to the
`&` prefixed within `block_to_proc`'s method definition. This `Proc` is 
assigned to the local variable `block_to_proc`.
* Within the first method's body, a second method is invoked
(`proc_to_block_method`), with the `Proc` passed to it as an argument.
* The `proc_to_block_method` initializes the local variable `proc_to_block` 
and assigns the `Proc` object to it.
* Within the second method's body, a third method is invoked 
(`call_the_block_to_proc`), with `&proc_to_block` passed to it as an argument.
In the context of a method invocation, that `&` first checks whether
`proc_to_block` is a `Proc` (it is) and then converts it to a block.
* The block received by `call_the_block_to_proc` is converted to a `Proc`
object because of the `&` prefixed to the parameter within the method
definition. Therefore, `block_to_proc` refers to a `Proc` object within the 
third method's body.
* The `Proc` is then called, which outputs `"hello!"`

{% include images.html file="spongebob.gif" 
  caption="Phew! We made it" 
  alt="Spongebob Squarepants goes Phew" %}

## TL;DR - It's all about context!

To sum up, an `&` prefixing an object can do two opposite actions, depending
on the *context*:

* Within a **method definition**, the `&` converts a block (passed as an 
argument) to a `Proc`

```ruby
def some_method(&block)   # & within a method definition
  block.call
end

some_method { puts "hi from the explicit block!" }
```

* Within a **method invocation**, the `&` first converts the object to a `Proc`,
and then converts the `Proc` to a block

```ruby
[1, 2, 3].map(&:odd?)    # & within a method invocation
```


