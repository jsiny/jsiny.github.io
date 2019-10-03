---
layout: post
title: How does the Internet work?
date: 2019-10-03 11:06 +0200
last_modified_at: 2019-10-03 19:50 +0200
permalink: how-internet-works
description: Let's dive into networking and explain how IP, TCP, TLS or HTTP work!
image: 
published: true
sitemap: true
excerpt_separator: "<!--more-->"
categories: Networking
tags:
  - Learning
  - How-To
  - Launch School
  - Internet
  - OSI Model
  - HTTP
  - TCP
  - IP
  - DNS
  - TLS
---

Being born in the 90s, I've lived most of my life in a post-Internet world. I
do remember the sweet sound of 56 kb/s modem, but most of my browsing time
has been *after* the dial-up era.

Internet, for my generation, is just an inherent part of life. It's kind
of hard to imagine what it was like *before* (did people actually read books?),
and we never pause to think:

> Wait, how does the Internet even work?

So *that*'s exactly the subject of this post. Buckle up your
seatbelt, we're going deep into networking!

<!--more-->

{% include images.html file="internet.jpg" 
  caption="Welcome to the Internet! I'll be your guide" 
  alt="90s Internet book" %}

We'll examine two aspects of the Internet:
* how data is *transferred* over the network
* how users can *access a webpage*

<hr>

**Table of Contents:**

* TOC
{:toc}
<hr>

## How data is transferred over a network

What happens when you type a URL into your browser?

Let's assume you want to reach Twitter, and typed `https://twitter.com/home`
into your browser.

### URL Parsing

The first thing your browser does is *parse* the URL, in order to extract
its components:
* the **scheme** (`https`), which informs the browser that we want to use 
the HyperText Transfor Protocol Secure to exchange data with the server;
* the **host** (`twitter.com`), which is the computer that *hosts* the 
resources of this website (eg. the HTML, the pictures, etc.);
* the **path** (`/home`), which corresponds to the particular resource we 
want to access.

### DNS Lookup

The domain name (`twitter.com`) typed is nothing more than a human-friendly name
that refers to a server somewhere on the Internet.

In order for data to be transferred to this server, we need to know
its **IP address**. IP addresses (v4) are sets of 4 numbers (from 0 to 255)
separated by dots `.`, like `104.244.42.193`. This logicial address is *unique*
and allows to locate a device on the internet.

As IP addresses would be hard to remember for humans with limited memory
slots, we use domain names to cover up this complexity. But how do we convert
a domain name into an IP address?

That's where **DNS** (Domain Name System) comes in! The DNS is a distributed
database which translates a domain name into an IP address. 

When you typed `https://twitter.com/home` into your browser, it first checked
whether `twitter.com` was already available in its cache (from a previous
browsing session). If it wasn't, the browser used its DNS provider in order 
to find the IP address associated with the domain name (and cached the answer
for later use).

### Encapsulating the Request

As we are in possession of `twitter.com`'s IP address, we are now ready to
send a request to the server! 

The browser thus takes the server's IP address and combines it with the
port number (optional field from the URL) to create a **socket**. 

This request is then passed through several layers where the data is further
encapsulated.

{% include images.html file="wrapped-cat.gif" 
  caption="Example of a cat being encapsulated, with a nice bow header" 
  alt="Cat wrapped in Chritsmas wrapping paper" %}

First, the request is passed to the **Transport Layer**, where a TCP
segment (or UDP datagram) is crafted. This segment now has a *header*, which
includes the following information:

* the destination port (which defaults to 80 for HTTP and 443 for HTTPS)
* the source port (chosen from the kernel's available range)

These network ports is what allows two specific processes on two different
devices to communicate. A device likely has multiple processes running
at the same time (eg. a browser connected to multiple websites, a Spotify
application running in the background, your email client, etc.), with
each having a special dedicated network port.

Second, the segment is sent to the **Network Layer**, where it is wrapped
with additional headers containing:

* the destination IP address (obtained through the DNS mapping of the URL)
* the source IP address (your device's IP address)

The segment is now an IP packet.

Third, the packet is sent to the **Link Layer**, where another header is added,
containing:

* the source MAC address (of the device's NIC)
* the destination MAC address (at this point being the exit gateway's address,
ie. the local router's)

Fourth, the **Physical Layer**. The frame is converted to binary data and sent
through the physicial medium (eg. Ethernet cable, optic fiber, radio waves)
linking your device to the rest of the network.

At this point, the frame is now ready for the great travel throughout the
unknown network beyond your local router!

{% include images.html file="adventure.gif" 
  caption="Good luck tiny packet!" 
  alt="Adventure through the unknown" %}

### Travelling on the network

The internet is a vast *network of networks*, which connects your home local
network to an infinite information sphere (the *Web*).

Once the packet leaves your local network through the subnet's router, it
needs to find its way up to its destination IP (featured within its Network
Layer header).

On its way, the packet will encounter **routers**, which will extract its 
destination IP and orient it to the next relevant network hop. The route
taken by the packet is not necessarily the *shortest*: among other things,
routers take into account the network congestion when deciding how to
route packets.

If the packet errs for too long on the network (ie. when its Time-to-Live
countdown equals 0), it will be dropped mercilessly.

Additionally, if a router is overflowed with packets, it will not hesitate
to shamelessly abandon the next packets.

{% include images.html file="computer-destruction.gif" 
  caption="Accurate depiction of a router murdering an IP packet" 
  alt="IT guy destroying a computer with a hammer" %}

Being a packet on the internet is tough.

All this also means that the internet is essentially an *unreliable* network.
Fortunately, we've invented protocols to abstract away from this 
unreliability: this is the role of the Transport Control Protocol (see below).

Let's assume here that our packet has a safe travel and reaches its destination
server (congrats tiny packet!)

### Receiving the Request

When the packet gets to the destination host, it has to go through the same
encapsulation layers, but in reverse order, in order to strip off all the
header information that was attached by the sender for a safe navigation
on the internet seas.

1. The Physical Layer receives a frame containing the packet, and sends it to
the Link Layer.
2. The Link Layer verifies that the frame is intact (through its checksum), and
removes the frame header, before sending it to the Internet Layer.
3. The Internet Layer assembles the fragmented packets into the original
datagram. It also removes the packet header before sending the datagram
over to the Transport Layer.
4. The Transport Layer (in our example, TCP) uses the destination port
(contained in the header) to know to which application to route
the request. It removes the Transport headers and sends the segment to the
Application Layer.
5. The Application Layer receives the segment and performs the requested
operation.

{% include images.html file="phew.gif" 
  caption="Our tiny packet made it all the way!" 
  alt="Jeff Goldblum sighing" %}

Our original request has now arrived to the server. However, that doesn't
explain *how* our browser communicates with a remote server. For all we know,
our request could have been immediately dropped by the server because
it didn't speak *the same language*.

So - how does our browser communicate with a web server? To answer this
question, we will now explore HTTP, the Web Protocol.

<hr>

## How to access a webpage

A web page is a document written in HTML, with references to various 
resources (images, videos, etc.)

However, the browser and the server exchange quite a lot before displaying 
a webpage onto your screen. There are several round-trips of exchanges 
before a single HTTP request is sent to the server.

### The TCP Handshake

One of these exchanges correspond to the TCP handshake, ie. the way our
browser establishes a *connection* to a remote server.

This handshake goes a little bit like this:
* Browser: "Hey server, I have something to ask you, do you mind?" [`SYN`]
* Server: "Hey browser, I'm listening. What do you want?" [`SYN ACK`]
* Browser: "Cool! I'll tell you what I want" [`ACK`]

{% include images.html file="syn-ack.jpg" 
  caption="I'll tell you what I want, what I really really want!" 
  alt="SYN ACK joke" %}

Once the browser has sent the last `ACK` segment, it can now start sending
data to the server.

Using the Transport Control Layer protocol ensures that the 
exchange of data is now being done onto a reliable network.
One a connection is established, TCP takes care of:

* Checking that the data has not been altered during transit
* Checking that the various segments are all here, and if not, supervises
the retransmission of lost packets
* Logically ordering the packets
* De-duplicating the packets

TCP effectively allows us to abstract away from the unreliability of the
lower-layer protocols. However, this reliability comes at the price of
performance, as TCP requires an entire round-trip of latency before the
browser can send its request.

### The TLS Handshake

Furthermore, if the URL's scheme is `https` (which it is, in our example), we
need another exchange before the HTTP requests can begin. This exchange
will ensure the **encryption** of all subsequent HTTP requests between 
the client and the server, and **authenticate** the host.

Here's a broad picture of how this handshake works:
* Browser: "Here's the TLS version I support, and here are my favourite
cipher suites" [`ClientHello`]
* Server: "Okay so let's use this TLS version, this cipher, and by the way, 
here are my public certificate and my public encryption key" [`ServerHello`]
* Browser: *checks the validity of the certificate* "Ok you're good!"
* Browser: "Here's how we'll decide on a private symmetric key for encryption"
* Server: "Copy 5/5! Will now start using this key for encryption"

This TLS handshake uses asymmetric encryption to agree on:
* which version of TLS to use
* the exchange of symmetric encryption key
* the validity of the host's certificate
* the cipher suite used

Once the TLS handshake is completed, all messages exchanged between the server
and the browser are now encrypted.

{% include images.html file="matrix.gif" 
  caption="There is no spoon" 
  alt="Neo from the Matrix" %}

### The HTTP Request / Response cycle

"Okay", the browser asks timidly, "am I good to send my HTTP request now?" - 
Yes, dear browser, you can!

The browser uses HTTP, a protocol designed for the communication between
a browser and a server, to ask the server for a particular web page.

The requests are sent in plaintext and would look like this:

```http
GET /home HTTP/1.1
Host: twitter.com
[Other headers]

```
The HTTP request (v1.1) features a request line, one mandatory header (`Host`)
and ends with an empty line. 

Here are the components from the request line:

* `GET` is the HTTP request method, which tells the server what we want
to do with the resource (in this case, to retrieve it)
* `/home` is the path of the resource we want to access
* `HTTP/1.1` is the version of the HTTP protocol we want to use

The server receives the request, and responds, also in plain text:

```http
200 OK
```
This status line (which indicates that the request was processed successfully)
can be accompanied with optional headers and body, like the raw HTML that
composes Twitter's home page:

```html
<!DOCTYPE html>
<html lang="fr" data-scribe-reduced-action-queue="true">

<head>
  <!-- Rest of the page -->
```

If the HTTP response contains references to other resources (like images,
fonts, or scripts), our browser automatically sends new HTTP requests to
collect them. If these resources are hosted on a different domain than 
the current one, the whole TCP / TLS process starts again for these new
domains.

Now that our browser has everything it needs, it parses the HTML, CSS
and JavaScript files, and renders the web page. I'm still a newbie in 
front-end so this part of the explanation will be for a future article 🥺

<hr>

## Internet - better than magic

{% include images.html file="internet-surfing.gif" 
  caption="Here we are, surfing on the web!" 
  alt="Surfer between internet memes" %}

Turns out: internet is *actually* a tangible thing that can be explained! 

But it's still damn hard to do so.
