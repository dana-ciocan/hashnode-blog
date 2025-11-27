---
title: "Weekly roundup: 27/11/2025"
datePublished: Thu Nov 27 2025 22:44:49 GMT+0000 (Coordinated Universal Time)
cuid: cmii0u5ai000202lbeyqaan6o
slug: weekly-roundup-27112025
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/hk2oPKuCqP0/upload/01fab66ce1d35062b26eaeadf16b818c.jpeg
tags: artificial-intelligence, typescript, software-engineering, apollo, lessons-learned

---

I’ve decided to try a few new things on my blog - I’ve already written one article in my “Today I Learned” series and now I’m starting another new thing: weekly roundups. It occurred to me that in a given week, I often learn little titbits here and there that don’t make good blog posts in and of themselves, but would make a great weekly post summarising everything I’ve learned. I thought it could be kind of interesting anyway - worth a try! It’ll serve as a log for me, and if someone out there learns something from it too, even better.

> I’m on annual leave tomorrow so this weekly roundup is a day early

# TypeScript error or arcane magic?

This week is week 15 (how?!) of my new job and having gone from a role as a Staff Engineer where I did very little coding back into a *much more* hands on Senior position, I am having my fair share of battles with TypeScript of all things. When I was still a Senior in my previous role, I was working in a JavaScript repo, so I am not as experienced at TypeScript as I’d like to be and have found myself confounded at TypeScript’s seemingly arcane errors.

What I learned this week is that these errors are logical and do actually make sense, once you stop and think about them for a minute and don’t just throw your hands up in frustration at yet another red (or yellow) wiggly line with an accompanying piece of text that might as well have come straight out of H.P. Lovecraft’s Call of Cthulhu.

I’m determined to better understand these errors and warnings - up until now, I have been focused on “getting the work done” and have mostly let Copilot or Cursor fix them for me. But really, I want to be able to see a certain error or warning and go “ah, yeah, that one again - let me just fix that up” and I’m not there yet.

So something I’ve been doing is asking Gemini to explain things in an easy-to-understand way - I gave it the context that I’m currently learning TypeScript and am mostly used to working with JavaScript and so far, its explanations have been really helpful.

I learned what the `error` type means for example, which is that TypeScript can’t compute the type so it’s effectively going “excuse me?!” and probably signifies something’s gone a bit wrong in your code. Seems like a pretty basic thing, but I hadn’t realised that before, so there you go.

# When is going fast too fast?

I’ve been working on the frontend for a project this week where I was waiting on confirmed designs and finished backend API endpoints, so I thought “I know! I’ll just make a presentational UI component and plug in the API and the finished designs later”. Nice idea in theory, but I’ve had to do a lot of rejigging after the fact and I’m not sure how much time it really saved me in the end.

I guess the main advantage of this kind of approach is that I was able to merge *something*, even if it wasn’t perfect and at the end of the day, that’s helpful even if it just means that the work is done in smaller chunks and therefore easier for my colleagues to review.

The main disadvantage is the rework and the fact that you’ll pay for any assumptions you make at a later date. I had used composition to combine a few React components, but some of the subcomponents were trying to do way too much and needed to be split into separate components that just did one thing.

There’s a really fine line between trying stuff out and moving quickly and going so fast that you end up tripping over yourself and having to do a bunch of rework. I definitely skirted that line this week. I’ve been feeling a bit sheepish about it because I feel like I should have learned this lesson by now. Then again, we all make mistakes and in the spirit of [the book I’ve been reading this week](https://www.waterstones.com/book/right-kind-of-wrong/amy-edmondson/9781847943781), I want to learn from it rather than beating myself up. I guess in future I will spend a bit more time thinking about my React components in advance and make sure they only have a single responsibility from the get-go.

# Cascading Apollo queries need a `skip`

This was an interesting quirk that I hadn’t appreciated. We are currently still using Apollo in our repo (though we will soon be ditching it!) and I had two queries, the first got an ID from the backend and the second used that ID as a variable.

Turns out, if you don’t add a `skip` attribute that tells Apollo not to do anything unless that ID exists, it will just hang. That was a fun ten minutes of head scratching and digging around trying to figure out why my component wouldn’t switch out of its loading state.

I asked Gemini whether it knew about this and it quite helpfully spat out the answer to my conundrum. And this is where my next point comes in…

# AI is quite handy, actually

When AI first started becoming really popular a few years ago I was a huge sceptic. I am still fairly sceptical to be quite honest - I’m not saying it’s not useful, I just don’t think it’s going to be quite as revolutionary as all the big tech companies seem to think.

However, in the last few months I’ve really let go of that fear of being left behind and the pressure I was feeling to use AI “just because”. As a result, I’ve been experimenting more with the technology and just kind of… trying stuff.

I used to mostly use “ask” mode in VS Code and ask Copilot questions, whereas now I will frequently use “agent” mode to vibe code bits of work. I will always check it afterwards though because there’s no way I will commit code an agent has written without approving it.

I’ve found Cursor’s agent mode excellent, but I dislike the IDE because I prefer vanilla VS Code, so I will switch into Cursor when I want to do fancy stuff and stay in VS Code the rest of the time. I have yet to try Claude Code and am feeling a bit intimidated by the setup for it. Maybe I’ll play with that next week!

I have really embraced Gemini as a source of information, most recently spending some time reading the Vercel docs on caching in app router and asking it to translate the diagrams and complex wording into something I could more easily understand. I’d also ask it things like “I thought client components rendered fully on the client but I’m seeing that this isn’t the case in a toy app I’ve built - do I need to adapt my mental model?” (turns out the answer was “yes” by the way).

So yes, I’m coming round to the fact that AI might actually make things easier for us developers. Do I think it’ll take our jobs? No, I do not. Is it being used as a convenient excuse to make a bunch of folks redundant? Who could say…