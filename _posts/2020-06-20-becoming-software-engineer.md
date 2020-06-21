---
layout: post
title: My First Weeks as a Software Engineer
date: 2020-06-20 18:28 +0200
last_modified_at: 2020-06-21 18:28 +0200
permalink: first-weeks-software-engineer
description: I take a step back and tell the story of how I transitioned into software engineering after a year of studies
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Blogging
tags: 
- Programming
- Blogging
- Learning
- First days in a company
- Software engineer
- Job searching
- Interviews
- Launch School
---

After a year of solitary learning, I've finally started my first software engineering job. I'm 
excited, exhausted and extremely grateful for the path that led me here.

I loved to read career switching stories so I thought I'd give a shot at writing my own.

<!--more-->

* TOC
{:toc}
<hr>

## Introduction

For those who don't know me, I'm a 26 years old woman living with my partner and my cats in Paris, 
France. I studied Economics and previously worked in a successful startup, where I ended up 
becoming general manager - until I decided to quit and become a software engineer. That was 
last August.

Since May 2019, I had joined an online school dedicated to mastery based learning - Launch School,
where I started my programming journey. It took me until the end of 2019 to finish the back-end 
portion of the course, and I still haven't finished the front-end portion (oopsie).

I found a job in March 2020 (more on that later) but only started at the beginning of June, because
I had planned on going to Southern Africa in May 2020 - but covid happened and my safari 
became hundreds of hours playing Animal Crossing. Close enough.

## Job searching

Not gonna lie - I got extremely lucky on that part. I'm not sure how much of my job searching 
experience here is applicable to other situations, but here we go.

I had registered on specialised platforms where software engineers describe their skills and 
job / salary expectations, and are later contacted by companies interested in their profile. 
Most French engineers use [talent.io](https://www.talent.io/en/) or 
[hiresweet](https://www.hiresweet.com/) for that purpose.

I set up my profile without much expectations - given that I was a half-baked engineer - and 
thought I'd go back and improve it later (spoiler: I never did).

A couple of weeks later, I was contacted by a recruiter from a company. I had 
already received my fair share of annoying Linkedin recruiters telling me I was perfect for some
position that clearly proved they hadn't read a thing of my resume - but this offer stood out.
We got in touch, and as I moved along the interview process, it became clear that I could
*actually* receive an offer from the company.

So I did the only rational thing possible: I dropped everything and job searched like a maniac.
I didn't want to receive an offer and not be able to actually know whether I liked this company
more than others, or if the salary offer was any good. I had grown accustomed to hearing the 
insane salaries that the [Launch School Capstone students](https://launchschool.com/results) earn 
in the US, so I needed to tune my own expectations to the realities of the French engineering
market.

I approached the job search exercise quite boldly. I had previously hired and interviewed dozens
of candidates, and I think this experience taught me quite a few things on how to craft a good
application. Therefore, I didn't waste my time sending dozens of applications to positions I didn't
even know. Instead, I researched the companies that I liked and tried to envision myself working
there. Once I could, I tried to get in touch with their recruiters on Linkedin (recruiters are
craving for connections with engineers so it usually is pretty easy), in order to directly send them
my carefully crafted application. I also contacted my network in order to know whether any 
fitting position was opened. This led to interesting leads that never went through though.

In the end, I applied to 5 companies, and received 2 offers - a third was perhaps
on the way, but I got hired before finishing the process. The two offers promised different things,
but in the end I chose the company that contacted me in the first place.

## Interviews

Most companies I applied to were engineering-centric and had pretty similar processes:
1. a screening call (done by a recruiter) that mostly focuses on whether you've actually read the 
job opening and know the basics of the company
2. an on-site interview with a lead developer (with or without some live-coding)
3. a take-home project that takes between 2 and 4 hours
4. an on-site live-coding interview with another lead developer
5. a team lunch / dinner / drink to meet other people of the team and assess the cultural fit

Some companies switched steps 2 and 3, but the overall structure remained the same.

As for the coding exercises in particular, I was surprised on how much emphasis there was on
actually building a small working application during the take-home projects. Most were about 
writing from scratch a small application with limited features, without forgetting a test suite.
I could usually choose the framework (and opted for Sinatra, of course!). I also made the mistake 
of discovering how APIs and JSON conversion worked during one of them!

Live-coding exercises are always pretty stressful but I felt that probably was where I shined 
the most. I guess that endless study sessions with Launch School students definitely prepared me
on managing my stress level and on being able to think while I speak (a surprisinly difficult feat). 
It also didn't hurt that I extensively prepared through Leetcode exercises and became familiar
with some algorithmic patterns.

Here are some examples of live-coding exercises I was given:
- writing a new feature to my take-home project (that seems to be pretty common)
- solving the [coin change problem](https://www.geeksforgeeks.org/understanding-the-coin-change-problem-with-dynamic-programming/)
- implementing from scratch the `reduce` function

## My company and position

I'm a proud full-stack software engineer at [Shipup](https://shipup.co), a SaaS company that
helps online retailers create a better post-purchase experience for their customers (eg. better 
delivery tracking emails, integration with customer support in case there's an issue with the
delivery, etc.)

Basically, the company is extremely API-oriented: it's integrated with dozens of different carriers
and provides multiple ways for online retailers to send them order data. The technical stack is a 
mix of Ruby on Rails and React.

I'm still pretty new to the React world so my work has been mostly focused on Rails so far - but
I'm trying to do some 
["just-in-time" learning](https://medium.com/launch-school/just-in-time-learning-f6a10886ddfe) in 
order to soon become proficient in React.

Shipup is a small French startup, with only 25 employees so far (including 6 engineers). They're
pretty ambitious and I can see these numbers rapidly growing in the upcoming months - I feel like it's an
exciting time to join a company! 

## Bridging the gap between studying and working

I started working 3 weeks ago, and since then, I've had to learn an insane amount of tools 
and technologies. Here they are, with a personal assessment on how well I need to know them.

| Tool | Importance? | Comment |
|-|-|-|
| [Rails](https://rubyonrails.org/) | Extremely | I was already pretty familiar with the framework |
| [RSpec](https://rspec.info/) | Extremely | I use it every day |
| [WebMock](https://github.com/bblimke/webmock) | Very important | Essential for API testing |
| [Faraday](https://lostisland.github.io/faraday/) | Important | Very useful for opening a persistent connection with an API |
| [Docker](https://www.docker.com/) | Limited | I only use some specific commands and so far, I haven't had to master anything Docker-related |
| [Kubernetes](https://kubernetes.io/) | Limited | Same as Docker |
| [React](https://reactjs.org/) | Extremely | Unfortunately I'm still very new to the framework so I feel a lot of pressure on quickly becoming up to speed |
| [Redux](https://redux.js.org/) | Very important | Same as React |
| [Jest](https://jestjs.io/) | Very important | Fortunately, I already knew some basics |
| [Storybook](https://storybook.js.org/) | Very important | I'm still unfamiliar with this technology |
| [Gatsby](https://www.gatsbyjs.org/) | Important | Used for the corporate website |

On top of that, I also have to acclimatize to this gigantic codebase, to the various APIs I have
to work with, and to using a specific git workflow.

I guess it becomes easier with time, but the first few weeks have been packed with discoveries and
frustration at my own ignorance.

The hardest and central part of my job seems to be "making every tool work together", surprisingly.
I usually do not tackle difficult puzzle or code challenge - most of my Ruby knowledge is more 
than enough to solve the problems I'm faced with. However, identifying the problem(s) and 
unveiling the various problematic layers take a lot of patience and pugnacity. Finding what to do
is where most of my job resides - actually coding it is the easy part.

So far, I've had to build 2 features, that demanded an in-depth understanding of the core business 
and the existing codebase. Before writing a single line of code, I've had to dive deep in various
files in order to actually understand what the hell was going on there. It doesn't help that my
first weeks were done remotely (covid, again) and that I'm not very good at asking for help when
I need it - I'm working on that though.

## Useful resources

Launch School's core curriculum provides strong programming foundations, and is not meant to be
exhaustive. Here are some resources that helped me build on these foundations:

- Preparing for interviews:
  - [A Common Sense Guide to Data Structures and Algorithms](https://pragprog.com/titles/jwdsal2/)
  by Jay Wengrow
  - [Cracking the Coding Interview](http://www.crackingthecodinginterview.com/) by 
  [Gayle Laakmann McDowell](http://www.gayle.com/)
- Ruby on Rails:
  - [Rails Tutorial](https://www.railstutorial.org/) by 
  [Michael Hartl](https://www.michaelhartl.com/)
  - [Demystifying Rails](https://launchschool.com/books/demystifying_rails) by 
  [Launch School](https://launchschool.com) (free)
- React:
  - [Fullstack React](https://www.newline.co/fullstack-react/) by [Newline](https://www.newline.co/)
- APIs:
  - [Working with Web APIs](https://launchschool.com/books/working_with_apis/) by 
  [Launch School](https://launchschool.com) (free)

## Final Notes

I've been asked a couple of questions by other Launch School students - I'll try to answer them 
here.

**In my job search, which industry did I target?**

I didn't target any specific industry. However, I did target one *type* of company: SaaS companies
(as in [Software as a Service](https://www.techradar.com/news/what-is-saas)).

My goal was to join a company where the technical team was a *profit-center* rather than a 
*cost-center*, ie. where the product shipped by the engineers was the main money-maker of 
the company. I felt that SaaS startups fit that description pretty well.

**Any surprises during the job interviews?**

The highs and lows of job searching are exhausting. Between applications, screening calls, 
interviews, take-home projects and preparing for the future interviews, job searching is a full 
time job. In my experience, it's not compatible with other things like still working for your 
previous job, advancing through the curriculum or caring for anything else.

As for the interviews themselves, I was surprised by how awkward some companies were regarding 
promoting diversity. I felt extremely uncomfortable when a recruiter candidly told me that they
would get an additional bonus for recruiting a female software engineer - ugh, okay.

**Is there anything I wished was covered by the LS curriculum?**

First, I'll start by saying how grateful I am that the Networking course is that much in-depth. 
I use this knowledge on an everyday basis.

As stated in the prevous section, I have used numerous resources to complement my Launch School
knowledge. Most of these resources are not based on 'fundamental knowledge' - I need them because
I use these technologies at my workplace, not because of their intrinsic value.

However, there are two topics that I think should be covered more in LS (or at least seem
pretty fundamental to me):
- Data Structure and Algorithms
- Web APIs

That being said, it's pretty easy to pick up a book about these topics once you've worked 
through the Core curriculum.

**How is using git 'in real life'?**

Short answer: not that difficult and awesome!

Most companies have their own version of a git workflow. We use 
[oneflow](https://www.endoflineblog.com/oneflow-a-git-branching-model-and-workflow), which is 
a simplified version of 
[git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) 
(which seems to be pretty widespread).

Using git *in real life* is mostly, to me:
- Always working on a separate branch
- Being extremely careful with how I name my commits
- ...and with *what* I commit (`git add --patch` is my new best friend)
- Constantly rewriting my local git history (`git rebase -i origin/master`) so that my commits
are self-explanatory and grouped logically
- Always making a Pull Request once I'm done with my feature (to allow my colleagues to review
my work)
- Merging with incredible care into `master`
- And going through the CI/CD pipeline before deploying to production

**What's unique about France's tech industry compared to the US?**

I've never worked in the US and can only guess.

I think the main difference is the type of companies you can work with here. You won't find any 
tech giant like in the Bay Area or New York. The biggest engineering companies probably have a 
maximum of a 100 engineers. Therefore, your options are limited to:
- tech startups (my choice)
- IT services companies (tech consultancy) 
- companies with a 'cost-center' IT department (and you'd rather avoid these)

Paris is a great place for tech startups, and I guess that most major cities (Lyon, Lille, 
Bordeaux...) have some bubbling startup activity but I wouldn't expect it to be true elsewhere. 
In short, there are only a handful of cities where some interesting engineering work can be found.

Also, English truly is the main language for software engineering - even in France. Most of my 
meetings, all of the code and all the documentation is in English. That caught me a bit off-guard
in a country that fought so long against the invasion of the English language. (In all seriousness, 
the [French academy](http://www.academie-francaise.fr/dire-ne-pas-dire/neologismes-anglicismes) has
a list of English phrases that *should* be replaced by French sentences.)

Finally, I should mention that the tech industry salaries definitely are above average in France, 
but are *not* exponentially inflated like they are in some US cities. Realistic figures are between
€35-40,000 (graduate) and €100,000 (experienced manager) - and 
[Paris](https://www.numbeo.com/cost-of-living/in/Paris) has a pretty high cost of life as well.

In short, while most software engineers have a better wage than most here, it's not exactly
as insanely profitable as it is in the US.

----

Alright! This has been a wildly long article, and I hope you found it useful.
Don't hesitate to get in touch with me if you have some further questions, and I wish you all
the best on your programming journey!


