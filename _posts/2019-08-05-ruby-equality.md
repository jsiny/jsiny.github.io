---
layout: post
title: Making Sense of Equality in Ruby
date: 2019-08-05 11:23 +0200
last_modified_at: 2019-08-05 18:01 +0200
permalink: ruby-equality
description: A detailed explanation about the differences between `=`, `==`, `===`, `equal?` and `eql?` in Ruby.
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Ruby
tags: 
    - Ruby
    - Learning
    - Equality
    - Ruby Quirks
    - Object Oriented Programming
---

When I discovered programming, I was bamboozled by the incredible amout of 
times you type the `=` key. Among other things, I couldn't help but 
wonder: Why on earth was I supposed to use `==` instead of the 
more 'natural' `=` to express equality?

Turns out, it's actually possible to make sense of this `=` madness!
Here's a cheat sheet to gain a better understanding of equality and the 
equal sign `=` in Ruby.

<!--more-->

* TOC
{:toc}
<hr>

## The `=` Madness

Here's a short program:

```ruby
def some_method(a)
  if a == 5
    a = 3
  elsif (1..10) === a
    a += 10
  else
    [1, 2, 3][2] = 4
  end
end

p some_method(5)  # => 3
p some_method(2)  # => 12
p some_method(15) # => 4
```

In the above code, we have no less than *5 different forms* of `=`:
* `=` in `a = 3`
* `+=` in `a += 10`
* `[]=` in `[1, 2, 3][2] = 4`
* `==` in `if a == 5`
* `===` in `elsif (1..10) === a`

Granted, the last situation is actually quite uncommon, but this 
profusion of `=` signs is still confusing. Let's dive in!

## What about `=`?

### General Case: the Assignment Operator

In most cases, the `=` character refers to the **assignment operator**, 
ie. the operator used to assign a new value to a variable. 

Therefore, `a = 3` is Ruby's way of informing the program that from
now on, the `a` variable will now reference the `Integer` `3`.

### `+=` and the combined assignment operators

Ruby comes with 6 extremely handy "combined assignment operators",
that both operate on a variable *and* assign the result back to the 
variable.

```ruby
  a = 2
  a += 10   # => 12
  a         # => 12
```

They are: `+=`, `-=`, `*=`, `/=`, `%=` (modulus), `**=` (exponent).

As with regular assignment, these operators have nothing to do with
testing for equality.

### Element Assignment `#[]=`

Another common Ruby construct is **element assignment**:

```ruby
str = "hello"   # => "hello"
str[0] = "Y"    # => "Y"
str             # => "Yello"
```

Element assignment is actually a method (`#[]=`), available to Strings,
Arrays and Hashes. It replaces the element referenced
by its index. Again, it doesn't check for equality.

### Setter Methods `#method=`

Finally, you'll encounter methods with a final `=`, which (spoiler
alert) have nothing to do with equality. These methods are **setter
methods**: they're used to set a value to an instance variable.

```ruby
class Cat
  def name
    @name
  end

  def name=(name)   # setter method
    @name = name
  end
end

kitty = Cat.new
kitty.name = "Pixel"
p kitty.name  # => "Pixel"
```

----

To sum up, `=` on its own is *never* used to check whether 
two elements are equal. 

Instead, the `==` method will 99% of the times do the job 🌈

## The `==` method and Value Equality

### Examples of `==` usage

`==` usually checks whether the two objects on either side have
the same *value*:

```ruby
3 == 3  # => true

str = "hello"
str ==  "hello" # => true
str == "world"  # => false

{ a: 1, b: 2 } == { b: 2, a: 1 }    # => true

[1, 2, 3] == [1, 2, 3]              # => true
[1, 2, 3] == [3, 2, 1]              # => false
```

From these examples, we can deduce the following:
* 2 identical integers have equal value (which sounds pretty obvious)
* A `String` of value `"hello"` referenced by a variable has the 
same value than another `String` of value `"hello"`
* Two `String` objects of different values (`"hello"` and `"world"`)
are unequal
* Two `Hashes` are equal if their key-value pairs are identical (even
if the order is different)
* `Arrays` must also have an identical order to be considered equal

### The `==` method

How does Ruby know how to compare two Hashes? Two Arrays? Two
custom objects? The answer lies in the fact that `==` is not 
an operator but an **instance method**. You could actually write 
`2.==(2)` instead of `2 == 2`.

Additionally, `==` is a `BasicObject` instance method (ie. the class
that contains every other object in Ruby), which means it's available
to *any* object.

However, we almost never use the default `BasicObject#==` method. 
Instead, each subclass is supposed to **override** the `==` method with a 
custom definition that suits its own needs.

For instance, the `Hash#==` method does not account for key-value pairs order. 
Here's the corresponding entry in the 
[Ruby documentation](https://docs.ruby-lang.org/en/2.6.0/Hash.html#method-i-3D-3D):

> **hsh == other_hash → true or false**
> 
> Equality—Two hashes are equal if they each contain the same number of keys 
> and if each key-value pair is equal to (according to `Object#==`) 
> the corresponding elements in the other hash.
> *The orders of each hashes are not compared.*

### Implications for Object Oriented Programming

Therefore, if you create a custom class and want to compare for "value equality"
between two instances, you'll need to implement your own custom `==` instance
method.

Otherwise, `==` will still work, but probably not how you intended it:

```ruby
class Cat
  def initialize(name)
    @name = name
  end
end

kitty = Cat.new("teacup")
kitten = Cat.new("teacup")

p kitty == kitten # => false
```
Those two `Cat` objects have exactly the same value but `kitty == kitten`
returns `false` - why?

The answer is that Ruby applied the `BasicObject#==` method, which has the 
same implementation than `BasicObject#equal?` (see next section), and
basically checks whether two *objects* are equal (not whether they
have the same value).

Indeed, how could Ruby know when 2 `Cat` objects are equal? It doesn't 
know how to compare these two custom objects. We need to explicitly tell 
Ruby how to compare them, by including an instance method `Cat#==`:

```ruby
class Cat
  attr_reader :name

  def initialize(name)
    @name = name
  end

  def ==(other_cat)
    @name == other_cat.name
  end
end

kitty = Cat.new("teacup")
kitten = Cat.new("teacup")

p kitty == kitten # => true
```

Here, we chose to consider two cats identical if they have the same `name`
value. It's completely up to us: we could also have chosen their `size` or 
`color`. And it works! `kitty == kitten` now returns `true` 🍾

## The `equal?` method

If we want to know whether two objects are actually *the same object*, we can
use the `object_id` method and compare their IDs:

```ruby
1.object_id   # => 3 

a = 1
a.object_id   # => 3 

1.object_id == a.object_id  # => true
```

Here, both `1` and `a` share the same ID `3`, which means they are both 
pointing to the same object. 

However, there's an easier way to compare for object equality, using the 
`BasicObject#equal?` method:

```ruby
a.equal?(1)   # => true 
```

`equal?` goes deeper than `==`: it checks whether two objects have the same
value *and* whether the two variables point to the same object.

```ruby
str1 = "hi there"
str2 = "hi there"
str3 = str1

str1 == str2      # => true 
str1.equal? str2  # => false 
str1.equal? str3  # => true
```

`str1`, `str2` and `str3` all have the same value `"hi there"`.

However, only `str1` and `str3` point to the same object (as expected, given 
that `str3` is a copy of `str1`). Therefore, `str1.equal? str3` returns `true`, 
while `str1.equal? str2` returns `false`: `str1` and `str2` are different 
objects which happen to have the same value `"hi there"`.

It's pretty rare to use the `equal?` method, but it's still useful to 
understand its behavior, especially when implementing custom classes.

## What about `===`?

If we know how to check for value equality (`==`) *and* for object equality
(`equal?`), what is `===` good for? It's actually used to check for
**range inclusion**.

The `===` method compares two objects by checking whether the first element 
(the *group*) includes the second element. It's rarely used explicitly.

```ruby
(1..10) === 3       # true: 3 is included in the range from 1 to 10
(1..10) === 12      # false
('a'..'d') === 'c'  # true: 'c' is included in the range from a to d
```

`===` is much more often used implicitly though, as this is the method used 
"under the hood" by `case` statements:

```ruby
char = 'd'

case char
when ("a".."e")
  "yay"
end

# => "yay"
```

The above case statement is equivalent to the following code:

```ruby
"yay" if ("a".."e") === char
# => "yay"
```

## The `eql?` method

Here's a last method to consider when thinking about equality. This one is 
pretty obscure, and there's a good chance you'll never even have to use it,
but I'm aiming for exhaustivity here 👩‍🏫

### Ruby Documentation

According to the 
[Ruby documentation](https://docs.ruby-lang.org/en/2.6.0/Object.html#method-i-eql-3F):

> **eql?(other) → true or false**
> 
> The `eql?` method returns `true` if `obj` and `other` refer to the same hash
> key. This is used by `Hash` to test members for equality. For objects of class 
> `Object`, `eql?` is synonymous with `==`. Subclasses normally continue 
> this tradition by aliasing `eql?` to their overridden `==` method, but
> there are exceptions. `Numeric` types, for example, perform type conversion
> across `==`, but not across `eql?`.

Therefore, two `Numeric` objects could be equal (with `==`), but different with
`eql?`:

```ruby
2 == 2.0        #=> true
2.eql?(2.0)     #=> false
2.0.eql?(2.0)   #=> true
```
But most of the time, two objects that are equal through `==` should return 
`true` when `eql?` is called.

### When should you use the `eql?` method?

The answer is: probably never. However,
it's routinely used by `Hash` objects to check for hash key equality. As you 
know, hash keys must be unique, and this is enforced through `eql?`.

To check for this uniqueness, `Hash` objects use the `eql?` method to 
convert the keys through the `hash` method. This method returns a hash code for 
each key.

```ruby
# Two different String objects with a value of "a" have the same hash:
'a'.hash	# => -3382060362238486793
'a'.hash	# => -3382060362238486793
```

If the two `hash` return values are equal (like for `"a"`), then only one
element can serve as a `Hash` key.

```ruby
hash = { 'a' => 1, 'a' => 2 }
# warning: key "a" is duplicated and overwritten
# => {"a"=>2} 
```

In this case, it's interesting to note that both `"a"` elements share the same
`hash`, but not the same `object_id`:

```ruby
# Different object IDs
'a'.object_id	# => 33313480
'a'.object_id	# => 33412160

'a'.eql?('a')	# => true
'a'.equal?('a') # => false
```
Therefore, `eql?` returns `true` (as it compares the two `hash`) and `equal?`
returns `false` (because their `object_id` are different).

### Implications for Object Oriented Programming

If you happen to override `eql?` in a custom class, you'll also need to 
override the `hash` method. If you don't, instances of this class won't 
work as keys in a `Hash`.

Indeed, objects used as keys *must* have a method named `hash` that returns
a numeric hashcode for the key. 

----

## Key Take-Aways

To sum-up:

* `=` on its own is *not* about equality: it's an **assignment operator**.
* `==` checks whether two objects have the same **value**.
* The `==` method should be **overriden** when creating a custom class, in order
to tell Ruby how to compare two custom objects.
* The `equal?` method checks whether two variables point to the **same object**.
* `===` checks for **range inclusion**, and is mostly used by `case` 
statements.
* The `eql?` method is almost exclusively used by `Hash` objects to check the
uniqueness of their hash keys.
