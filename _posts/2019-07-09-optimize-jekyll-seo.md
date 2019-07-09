---
layout: post
title: "A Beginner's Guide to SEO optimization in a Jekyll static website"
date: 2019-07-09 09:16 +0200
last_modified_at: 2019-07-09 13:21 +0200
permalink: optimize-seo-jekyll
description: Optimizing Jekyll for SEO is easy! Here are a few plugins and best practices you can use.
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories:
    - How-To
tags: 
    - Jekyll
    - SEO
    - Google
    - How-To
    - Lighthouse
    - Jekyll plugin
    - HTML
    - CSS
---


> What? There's no sitemap here?
> *- Me when I discovered my new Jekyll blog*

Although Jekyll comes a little "naked" in terms of necessary SEO tools
(especially in comparison to traditional CMS), it's pretty easy to remedy this
situation. Here are a couple of easy steps to follow, in order to improve your
SEO ranking and 
[your Lighthouse score](https://developers.google.com/web/tools/lighthouse/).

<!--more-->

* TOC
{:toc}
<hr>

## Install jekyll-seo-tag

The first thing you want to do is install the 
[jekyll-seo-tag plugin](https://github.com/jekyll/jekyll-seo-tag).

This plugin will automatically generate the following meta tags:
* Page title and description
* Canonical URL
* Open Graph title, description (useful for Facebook or Linkedin)
* Twitter Summary Card metadata
* and other stuff

Once the plugin is added to your `_config.yml` file, you'll need to add a simple
line to the `head` of every page. To do that, I created a 
`custom-head.html` file in the `_includes` folder and added the following 
SEO tag:

{% gist 17b76ed8bf8dc7d892dd2e19ca9a59d4 %}

Now, all you have to do is to update your title, metadescriptions and permalink
on every article or page ✨

```yml
title: "How to Set Up a Contact Form on Jekyll"
permalink: setup-contact-form-jekyll
description: Here's a detailed tutorial on how to set up a 
             free contact form on static websites like Jekyll
```

## Install jekyll-sitemap and optimize date management

The next thing you'll need is have a good sitemap, to help web crawlers
do their job. 

{% include images.html file="happy-index-robot.jpg" 
  caption="🤖 Must... index... everything... 🤖" 
  alt="Busy robot from Wall-E" %}

Fortunately, there's a plugin for that: 
[jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap)! And its use is
pretty straightforward.

The only subtlety is the date and time management. The sitemap plugin will
automatically use your **Created date** to fill the `<lastmod>` tag.

However, you probably want to have your **Last modified date** instead. 
To do that, you could use
[the jekyll-last-modified-at plugin](https://github.com/gjtorikian/jekyll-last-modified-at).

However the plugin isn't compatible with Github Pages, because of Github's 
automatic builds. Instead, you can add add the parameter `last_modified_at`
inside your front matter directly, and the sitemap will automatically use
this date as the Last modified date.

```yml
date:               2019-07-03 10:28:08 +0200
last_modified_at:   2019-07-07 11:55:00 +0200
```

To simplify your use of timestamps, I recommend using the 
[jekyll-compose plugin](https://github.com/jekyll/jekyll-compose). It will
automatically create your posts with the perfect timestamp and your custom
front matter.

All you need to do is correctly set up your `_config.yml` file and then
type `bundle exec jekyll post "My post name"` in your CLI.

Here are my own custom front matter settings:

```yml
jekyll_compose:
  post_default_front_matter:
    last_modified_at: 
    permalink: 
    description:
    image:
    published: true
    sitemap: true
    excerpt_separator: <!--more-->
    categories:
    tags:
```

Additionally, you should specify your UTC timezone in your `_config.yml` file,
using the [IANA TimeZone Database](https://en.wikipedia.org/wiki/Tz_database)
naming convention.

```yml
timezone: Europe/Paris
```

This will allow your timestamps to use your correct timezone:

```yml
# Before setting the timezone
date:  2019-07-03 08:28:08 +0000

# After setting the timezone
date:  2019-07-03 10:28:08 +0200
```

## Add a Google Analytics tracking ID

If you haven't already, you'll need to add a Google Analytics tag in order
to follow your traffic. 

To do that, let's create an `analytics.html` file in your `_includes` folder.

```html
<!-- Global site tag (gtag.js) - Google Analytics -->
<link rel="preconnect" as="script" 
  href="https://www.googletagmanager.com/gtag/js?id=YOUR_TRACKING_ID">
  
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', YOUR_TRACKING_ID);
</script>
```

Then, you'll need to include `analytics.html` in your `custom-head.html` file:

{% gist e8a02a89d20d53ba4c5671f1c6121de8 %}

The `% if %` condition removes the tracking tag from my own local server. Thus,
my own local tests will not be taken into account in my global Analytics
reports.


## Performance optimizations

### Google Analytics tracking

You may have noticed that, in the `analytics.html` file, I did not use the
default script provided by Google.

```html
<!--Default script-->
<script async 
  src="https://www.googletagmanager.com/gtag/js?id=YOUR_TRACKING_ID">
</script>

<!--Custom script-->
<link rel="preconnect" as="script" 
  href="https://www.googletagmanager.com/gtag/js?id=YOUR_TRACKING_ID">
```

Instead, I'm using the resource hint `rel="preconnect"` in order to tell the 
browser to start loading the Google Analytics script before an HTTP request 
is sent to the server. This performance optimization improved my loading time 
by **130 ms**.

### Reduce image size

Before uploading an image, you should always:
* Resize the image at its minimum. For instance, my blog accepts images up to 
800 px width, therefore it's no use uploading a 1500 px photo.
* Compress the image with a service like [TinyPNG](https://tinypng.com/)

This simple action will save you dozens of ms of loading time.

### Replace Github gist by code snippets

Whenever possible, use Markdown code snippets instead of Github gist. As 
pretty as they are, they also take up some precious loading time (about
**300 ms** for my blog).

### Remove useless fonts

My Jekyll theme came with a **190 ms** loading time title font. Which could 
mean only one thing: the font had to go.

Surprisingly, it was actually pretty difficult to get rid of it.

As the font was present in the default `_includes/font-includes.html` file,
I had to create a custom `_includes/head.html` file.

Inside this new `head`, I deleted the infamous
`% include font-includes.html %` line, and the font loading time magically
disappeared. 🚀

## Accessibility

The theme I've used scored pretty poorly on Accessibility items, because the 
colors chosen (albeit beautiful) lacked contrasts. This was especially true
for the theme's code snippets.

Therefore, I've used this 
[contrast tool](https://dequeuniversity.com/rules/axe/3.3/color-contrast)
to select new colors. Then, I've included the new hexadecimal codes in 
my `assets/css/main.scss` file. Here's an excerpt:

```css
/* Literal.Number */
.highlight .s { color: #C04343; }
/* Literal.String */
.highlight .na { color: #8B38D1; }
```

## SEO 101

Finally, and perhaps the most important thing, is to consistently respect
the SEO Best practices throughout your website. 

Here are a few of them:
* Use **HTTPS** (plus it's so easy to enforce HTTPS with Github Pages!)
* Declare the **HTML doctype** at the beginning of the page, along as the
**<lang>** attribute
* Have a valid **robots.txt** file
* Use **consistent URLs** (either `/my_link` or `/my_link/` but not a mix 
of both)
* Use the **`alt` attribute** on your images, both for ranking and accessibility
reasons
* Choose a discernable name for your **links**
* Make all **external links** `_blank` and `nofollow noopener`
* Create a **netlinking** strategy, to improve your pagerank and enhance the 
Internet user's journey
* ...and a bunch of other stuff

Your best bet is to frequently run
[Lighthouse audits](https://developers.google.com/web/tools/lighthouse/)
on your pages and fix every problematic item.
