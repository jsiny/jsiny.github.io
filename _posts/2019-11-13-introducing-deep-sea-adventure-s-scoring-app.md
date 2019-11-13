---
layout: post
title: Introducing Deep Sea Adventure's Scoring App
date: 2019-11-13 09:42 +0100
last_modified_at: 2019-11-13 11:23 +0100
permalink: deep-sea-adventure
description: This app is a project built in Ruby / Sinatra, dedicated to be a assistant to the board game Deep Sea Adventure
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Project
tags: 
  - Ruby
  - Sinatra
  - Bootstrap
  - Heroku
  - Travis CI
  - Minitest
  - Project
  - Learning
  - Deep Sea Adventure
  - Game
---

This [website](https://deep-sea-adventure.herokuapp.com/) is a **scoring tool**
dedicated to the board game
[Deep Sea Adventure](https://oinkgms.com/en/deep-sea-adventure) edited by
[Oink Games](https://oinkgms.com/en/).

Its goal is to provide players a **reliable way to compute the oxygen decrease**
during a round. It's meant to be used side by side with the board game,
either on a mobile or computer.

After 6 months of learning, this project is my **first** big, entirely personal
project, and I'm very proud of it.

[Visit the website](https://deep-sea-adventure.herokuapp.com/) | [See on Github](https://github.com/jsiny/deep_sea_adventure)

<!--more--> 

<hr>
* TOC
{:toc}

## Tech Stack

This tool has been developed in **Ruby**, as I've spent the past months
learning programming through that language. I've applied an object-oriented
design as it felt natural to segment the various elements into objects with
an interface (`Players`, `Round`, etc.)

I've chosen to develop the website through the light-weight, Ruby 
domain-specific language **Sinatra**. Even though I've previously worked with
Ruby on Rails, I preferred using a lighter library rather than a comprehensive
framework that may hide away the complexity of web applications.

```ruby
# Homepage
get '/' do
  erb :home
end
```

For instance, this Sinatra code snippet means that a `GET` request to the
homepage (`/`) will trigger the loading of the ERB (embedded Ruby) template
`home.erb`.

As the project grew in complexity, I've added a comprehensive test suite (with
**Minitest**), in order to be able to safely refactor and prevent regressions.

{% include images.html file="minitest.jpg" 
  caption="All green! 💚" 
  alt="Minitest" %}

Additionally, I taught myself to work with **Bootstrap** for this project.
Being a complete beginner in front-end development, with no knowledge of
JavaScript and only the very basics of CSS, this proved to be quite
challenging.

However, I'm happy I went through that struggle because Bootstrap helped me
build a smooth and user-friendly application (both on desktop *and* mobile).

I've deployed the application on **Heroku**, mostly because it's a 
free hosting service. (The app is hosted onto an EU server, so US-based
users might encounter some latency.)

Finally, I also took the opportunity to learn about **Travis CI** and set up
my first continuous integration and automatic deployment, through
`Github > Travis CI > Heroku`. As I was working alone on this project,
this configuration probably is a luxury, but it's never too early to learn
the best practices.

## Challenges

Through this project, I've faced two main challenges:
* I had to learn the basics of front-end and Bootstrap to go through it
* I wanted to build an application *with no database and log-in system* so
instead, I extensively used session storage to persist user data

**Why did I choose to steer clear of login and databases?**

Mainly because I think that most users find it tiresome to go through a
registration process for almost every Internet service. A "plug and play"
approach is much nicer instead.

Plus, in this situation, using session storage worked pretty well because:
* Most games last less than 1 hour so sessions expiring was not a concern
* Even though several players could want to keep score, it feels acceptable
that they use only one player's device.

## Motivation

I've chosen to build this app mostly because I like games but dislike
arguing over a messy count score.

In Deep Sea Adventure, players dive into the deep ocean looking for treasures.
All divers share the same oxygen tank, and each treasure picked up weighs down
the diver and increases its oxygen intake. All divers must be back into the
submarine before the oxygen tank becomes empty. As such, it is critical to
accurately monitor the available oxygen. ([More on the game's rules](https://oinkgms.com/en/deep-sea-adventure))

However, experience shows that it can be difficult to accurately compute the
available oxygen in a quick game setup, and that arguments over which player
should have drowned tend to ruin the fun. This is where this Scoring App comes
handy!

## Screenshots

{% include images.html file="player_turn.png" 
  caption="The app records the choices made by the player and displays the available oxygen supply" 
  alt="Deep Sea Adventure - Player's turn" %}

{% include images.html file="score.png" 
  caption="At the end of the round, players who made it back to the submarine count their treasures" 
  alt="Deep Sea Adventure - Score" %}

{% include images.html file="end.png" 
  caption="After 3 rounds, the app computes the scoreboard" 
  alt="Deep Sea Adventure - Score" %}