---
layout: post
title: How I Prepared for Launch School's 109 Written Assessment
date: 2019-07-17 12:14 +0200
last_modified_at: 2019-08-12 16:57 +0200
permalink: preparing-launch-school-109-written-assessment
description: Here are my tips on how to study for Launch school's first written assessment (109)
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Launch-School
tags: 
    - Launch School
    - Learning
    - Memory
    - Ruby
    - Anki
    - Timelogs
---

I recently took Launch School's first written exam (RB 109), that comes at the
end of the first course, RB 101, Programming Foundations.

This course is especially challenging because it forces us to simultaneously:
* learn to learn again,
* learn Ruby syntax,
* learn problem solving.

I thought it would be a good time to reflect on my study methods and the time
it took me to get there.

<!--more-->

**Disclaimer**: The time it takes to get through the course is entirely
personal. I may have been at ease on some topics, and completely stuck
on other parts. The time logs are simply indicative and should not impact
your own study flow.

## Going through the 101 courses

During the lessons, I always took notes in **Markdown** (this will come in handy
later), using [Typora](https://typora.io/). My notes were pretty detailed
(sometimes even bordering on copying word after word the lesson). I guess 
this meticulous copying helps my memorization, even though I haven't re-read
my notes for the most part.

I spent a significative time going through the lessons (**37.5 hours**), and
was striving to understand every line of the lesson.

## The Ruby Small Problems

To take a break in between lessons, I was also advancing on the **Ruby Small 
Problems**. My goal was to always find a working solution myself, and if I
didn't, I added this problem in my "to be done again" list.

{% include images.html file="to-do-list.png" 
  caption="Pro tip: you can create a checkbox in markdown with `[ ]`" 
  alt="My exercises to do list" %}

I would then briefly read the solution (trying not to spend more than a 
couple of seconds on it), then hide the solution and try to come up with 
the exact same program without peeking too much.

If the solution introduced a new method, I would look it up on the 
documentation and sometimes incorpore it in my Anki memory cards (more on that
below).

If I could, I would also work on the Further Exploration. But most of the time,
the Further Exploration joined the "to be done again" list.

When I was nearing the end of the 101 course, I started re-doing the "to be 
done again" exercises, and even though some remained difficult, most of them
felt much easier. This was probably the biggest sign that I was actually
making a progress (and it felt good!) 

Most of my time on 101 was spent on the Ruby Small Problems, which took me
more than **60 hours**. (And I haven't quite finished a couple of
Advanced Problems.)

## Creating Flash cards on Anki

Everytime I would encounter an information that seemed important enough, 
I would create an Anki flash card.

**Note:** on desktop, I prefer using [Anki's web interface](https://ankiweb.net) 
rather than their pretty dated software interface.

What's my gradiant for "important enough"?
* An information that contains some general knowledge about computer science
(eg. regular expressions, command line interface...)
* An information about Ruby's behavior (eg. pass by value / reference, 
variable scope, truthiness)
* A method that seemed particularly useful (eg. `Array#|` to merge two arrays
while only keeping the unique values)

Example of questions and answers:

> How can I add an element to the beginning of the array?
> 
> By using `Array#unshift` (destructive)

> How can I check that a collection has at least one element that satisfies an 
> expression?
>
> By using `Enumerable#any?`

> What does the last expression return? 
> ```ruby
> arr = [['a', ['b']], { b: 'bear', c: 'cat' }, 'cab']
> arr[1][:b][0]
> ```
> 
> `"b"`

I would use my commute time to go through my Anki deck (on the mobile app),
sometimes editing old questions when the formulation was too vague or implied
that I didn't quite grasp a concept at that time.

## The Study Sessions

At the end of the 101 course, I started to attend as many study sessions as 
I could. Before that, I was pretty embarrassed to showcase my lack of 
mastery, and prefered avoiding them. 

{% include images.html file="buzz.gif" 
  caption="How I thought TAs would react when I'd open my mouth" 
  alt="Buzz Lightyear gif" %}

However, I can now see how mistaken I was. The Teacher Assistants are nothing
but kind and encouraging. Attending study sessions both helped me 
try new solving methods and gain in confidence. These sessions are 
absolutely essential for the oral assessment, but I believe they helped me
for the written assessment as well.

## The Study Guide

Launch School provides a Study guide that details what will be covered in the
written assessment. And this is actually 100% true: what is listed *will*
be useful during the exam.

I personally spent quite some time on the following:
* Variables as pointers
* Mutative methods
* Pass by reference & Pass by value
* Truthiness

Whenever a concept came up, I tried to create my own example on Ruby and saved
it for the exam. Complete mastery of the concept is not enough: you need to be 
able to answer fast, and having pre-made bits of answers can go a long way. 

Keep in mind that you'll have more than 20 questions (I had 23) and only
3 hours: if you take into account the necessary time to read the questions and
proofread your answers, you'll have less than 10 minutes per question.

To assess whether I was ready to take the exam, I've worked on 
[Srdjan](https://medium.com/how-i-started-learning-coding-from-scratch/advice-for-109-written-assessment-part-3-d39dceb06c0c)'s
programs while trying to spend less than 5 minutes to precisely describe 
what was happening under the hood.

I ended up creating a handful of pre-made sentences that were useful all the
time, like:

> We've initialized the variable `var_name` and assigned to it the 
> Integer/String/etc object `value` to it.

This little trick saved me a couple of critical minutes during the exam.

## My Timelogs

I've used [Toggl](https://www.toggl.com/) to keep track of how long I spent
on each topic, and also to make sure that I reached my 15-hours per week
objective. 

Here's the total breakdown of my **127 hours** spent on the 101 course:

| Topic | Duration |
| ----  | -------- |
| Lessons | 33.5 hours |
| Video Lessons | 4 hours |
| Walk-through / Assignments | 12 hours |
| Ruby Small Problems | 52 hours |
| Practice Problems | 10 hours |
| Live-coding | 8 hours |
| Exams (incl. quizzes) | 7.5 hours |

{% include images.html file="toggl.png" 
  caption="The weekly breakdown" 
  alt="My weekly toggle timelogs" %}

Now, time to practice for the interview assessment!

----

If you're currently preparing the 109 Launch School exams, congratulations! 🎉 
Additionally, you might find these other posts useful:
* [How I Prepared for Launch School's 109 oral assessment](preparing-launch-school-109-oral-assessment)
* [My Favorite Katas to Prepare for Launch School's 109 oral assessment](codewars-kata-launch-school-109-oral-assessment)
