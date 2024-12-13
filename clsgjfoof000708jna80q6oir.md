---
title: "What the heck is INP?"
datePublished: Sat Feb 10 2024 20:37:34 GMT+0000 (Coordinated Universal Time)
cuid: clsgjfoof000708jna80q6oir
slug: what-the-heck-is-inp
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/krV5aS4jDjA/upload/4d52a0f73b3c9de7b0d18982ab1deb00.jpeg
tags: web-performance, core-web-vitals, interaction-to-next-paint

---

If you've been working in the web space for a while and you have been doing work around performance, you are probably aware of Google's [Core Web Vitals](https://web.dev/explore/learn-core-web-vitals). If not, these are the "page experience" metrics the search engine announced back in 2020 and started using as part of its rankings in 2021. Making sure you meet the thresholds for each metric is important as it can change the ranking of your page and affect your SEO.

As a quick recap, up until now, the three important metrics have been:

* **Largest Contentful Paint (LCP)** - the amount of time it takes for the largest piece of content on your page to load
    
* **Cumulative Layout Shift (CLS)** - the amount content moves about as your page loads; nobody likes it when a button moves as you go to click it and you accidentally click on something else!
    
* **First Input Delay (FID)** - how long it takes for your page to respond after the user interacts with it for the first time
    

However, FID will soon be retired and this is where INP comes in.

### Why is First Input Delay (FID) being binned?

First, let's answer the obvious question: what's wrong with FID? It's served its purpose for four years so why is Google getting rid of it now?

Let's have a look at the definition of First Input Delay from [web.dev](https://web.dev/articles/fid):

> FID measures the time from when a user first interacts with a page (that is, when they click a link, tap on a button, or use a custom, JavaScript-powered control) to the time when the browser is actually able to begin processing event handlers in response to that interaction

So FID only measures how quickly a site responds when a user **initially** interacts with a page. This means that there could be sites out there that respond very well initially, but as more of the content loads in or something blocks the main thread, the site slows down or becomes unresponsive and FID would not be able to detect this.

This is exactly why Interaction to Next Paint is being introduced.

### Interaction to Next Paint (INP)

When we look at the definition of Interaction to Next Paint (INP) on [web.dev](https://web.dev/articles/inp):

> The goal of INP is to ensure the time from when a user initiates an interaction until the next frame is painted is as short as possible, for all or most interactions the user makes

It becomes obvious that it solves that big pain point we noticed with FID. Rather than just checking what the site is like when it first loads in, INP will measure responsiveness throughout the lifecycle of the page.

INP keeps track of all the interactions a user makes with your page and then reports the time threshold that most of the interactions were under. So if your INP is 120ms, your site responded to user interactions in 120ms or less in most cases.

### What does good look like for INP?

As with all the other Core Web Vitals, there are three thresholds for INP:

* Under 200ms is good
    
* Between 200 and 500ms needs improvement
    
* Over 500ms is poor
    

If you don't respond to a user's interaction quickly, they might think that your page is broken or slow. For example, say some data is loading in and the UI sits there and does nothing - we've all been there, we hit refresh because we assume the page has gone to sleep, right? However, if the user sees something (perhaps a spinner) to indicate that something is happening in the background, then they know to wait because something will be loading in soon.

This is the kind of behaviour INP tries to encourage - if you can't respond to your user's interaction quickly, at least give them a sense that something is happening so they're not left wondering.

### How do I measure INP?

You can measure INP in the lab and in the field, but Google recommends using RUM (real user metrics) data over lab data if you are able.

The easiest way is to enter your domain into [Page Speed Insights](https://pagespeed.web.dev/) and take a look. This tool provided by Google uses both lab and field data so should give a fairly accurate representation of your INP.

I tried running a Core Web Vitals test in WebPageTest but as of today it is not showing the INP metric yet. This may be because it has not quite replaced FID just yet.

Which brings me to...

### When does INP become stable?

INP will replace FID on the 12th of March 2024, which is less than a month away now, so best to get cracking and have a little look so you're not caught by surprise!