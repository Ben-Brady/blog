---
layout: post
title:  "XSS on Safebooru via URL Embeding"
date:   2023-03-28 +0000
---

Recently I read a [blog](https://swarm.ptsecurity.com/fuzzing-for-xss-via-nested-parsers-condition/) by Igor Sak-Sakovskiy on how to get XSS on forums by abusing their multiple parsers. Creating payloads that the chain of parsers with transform into malicous HTML. 

Since I've been doing a lot of security reports on gelbooru recently and they have their own system for BBs style tags to use on their forums and comments sections. Being their own custom made solution, it seems ripe for opportunity.

## Source Code Analysis

Instead of attempting to fuzz on the live site which would be quite distruptive and against their rules. I instead made use of the published Gelbooru 1.11 source code that was made public in 2008... quite outdated. However, I knew that most of the code had been left relatively untouched, with only new features tacked on every so often.

The forum parsing code is handled by three funtions: `short_url`, `swap_bb_tags`, and `linebreaks`. Interestingly, there isn't a function that combines them all together, they're simply called in order in the UI code. This meant forum and comment encoding were handled differently since they were called ina a different order. Comment encoding does `swap_bbs_tags -> short_url -> linebreaks` while forum encoding does `short_url -> swa p_bbs_tags -> linebreaks`. This has no effect on regular users, however more exotic payloads may be handled differently due to this, However I still made sure I took this into account when writing payloads.

### swap_bbs_tags

![short_url Code](/images/safebooru-swap_bb_tags.webp)

The swap_bb_tags function is pretty simple, it interates through each pattern and matches anything inbetween two bb tags and places them into the HTML templates. With most tags, this is relatively normal. However, with the the `[post]` and `[forum]` tags it both duplicates the content and also places it in a attribute. Both of these features may prove to be useful when crafting an XSS

### short_url

![short_url Code](/images/safebooru-short_url.webp)

The short_url code on the other hand was a different beast entirely. For swapping out URLs with anchor tags it was really quite complex. I found it very hard to understand this code, so I gave up trying to understand how it worked logically, instead trying to understand what it might do. I was able to gather a few points:
- There is a maxmimum of 50 links per post
- Links over 60 characters are shortened into their beginning and end
- The href is reflected directly into the HTML
- The link isn't parsed to see if it's valid, only a http:// prefix is checked.
- Links are terminated by a space, newline or tab

## Crafting a Payload

In order to help with creating a payload I copied all the code into a PHP so that I could create a playground to test different payloads easily on the original forum code.

![Safebooru Playground](/images/safebooru-playground.webp)

Using this I was able to discover that a bug in the URL parser caused the `http://http://test` url to be parsed strangely. I was able to inject the attribute `FOO"` into the anchor tag.

![Test Attribute Injected](/images/safebooru-attribute-injection.webp)

However, when trying to use `http://http://onmouseover=alert(document.domain)` I got a javascript syntax error which prevented the payload from being executed. It took me a while to figure out what was causing this, turns out the because of the way the parsing was done left a stray quote on the end of the javascript. 

This mean that the payload became `onmouseover='alert(document.domain)"'`. The stray quote on the end causing a syntax error that prevented execution. Furthermore, there was no way to remove it due to the way it templated into the page. Luckily I managed to find a bypass this by forming it into valid javascript by putting a `+"` on the end, so that the final output with be `alert(document.domain)+&quot;"`. In order to evaluate the expression it would need to run the alert first.

### Success

I ended up with the final payload: `http://http://onmouseover=alert(document.domain)+"`

which when rendered on the server would get transformed into

```html
<a
    href="http://http://<a href="
    onmouseover=alert(document.domain)+&quot;"
...
```

And... it worked!

![](/images/safebooru-xss.webp)

## Resolution

With a working example I was able to report this to the Gelbooru team in order for it to be patched and I was generously payed £40 for my efforts by LozerTUser. This attack only worked on safebooru as they hadn't switched to a new method of parsing URLs using regex, so I can't claim I hacked Rule34... again.

Funnily enough, I only actual implented the fuzzer from the article inspiring this whole thing after getting it working manually. The fuzzer immeditaly was able to detect the parameter injection in the URL parser.

![](/images/forum-fuzz-url.webp)

I also attempted to see if an XSS was possible with the just the BB tags. However, the only things you could do was create a few broken parameters. You weren't able to inject arbitrary HTML tags or attributes in order to get an XSS. 

![](/images/forum-fuzz-bb.webp)
