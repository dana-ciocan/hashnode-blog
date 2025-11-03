---
title: "Let's talk about code reviews"
datePublished: Mon Nov 03 2025 20:24:24 GMT+0000 (Coordinated Universal Time)
cuid: cmhjl94bq000102l436ag6zee
slug: lets-talk-about-code-reviews
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/0ZUoBtLw3y4/upload/3bca11727585a2ec4da374c50464bd5d.jpeg
tags: feedback, code-reviews, pull-requests, pr-feedback, merge-requests

---

Giving feedback on pull requests (or merge requests, depending on your flavour of lingo) is something we do every single day as Software Engineers, but if you don’t stop and think about it for a minute, it is quite possible to make a bit of a hash of it. At best, your colleagues could be a bit annoyed, but at worst, you could really do some damage to your relationships with your colleagues if you’re not careful.

Even as someone who’s been in the industry for a long time, I’m still constantly learning and I’m definitely not perfect - I’m a human being and that means I make mistakes - but over the years I’ve found some tricks that have helped me and I thought I’d share these so you can use them too. Let’s go!

# Empathise

This seems like an obvious one and if you’re in a workplace with a good culture, empathy should be a default setting for everyone, but some of us may need a bit more of a push to think about it. Please don’t assume that the person whose code you are reviewing is stupid or not good at their job or even just look down on them for being less experienced than you are.

Put yourself in their shoes - perhaps they have just had a long week and this was a late Friday submission so they missed something silly, or perhaps they are a more junior member of your team and therefore they simply do not know how to do something that you do. Always think about things from the other person’s perspective.

Don’t dive straight in with a critical comment, instead, think of a way to gently broach the topic. I find asking questions can really help here - something like “I don’t know whether this was intentional, but something doesn’t quite look right to me here. Did you mean to leave out X?” This gives the other person room to have a look and explain their approach if it was intentional or say “oops my bad” if it wasn’t.

# Ask questions

On that topic, I find that asking questions is a really good way of both giving feedback but also opening up a discussion. In software engineering, there is often more than one right answer and just because you prefer one method, doesn’t mean it’s the best course of action in this instance. A simple “have you considered doing it this way?” is much more effective than “you should use this other method” (the “idiot” being implied in that last comment).

I find this tool *especially* invaluable when joining a new team or starting a new job. You don’t have all the context, so what might have been a perfectly acceptable ask in your previous role might not work the same way here so it stops you from putting your foot in it if that’s the case. Asking lots of questions is also the best way for you to learn, but it can feel quite vulnerable. If you do feel awkward about it, it’s perfectly okay to add a “just curious, but…” or “quick newbie question from me:” just to soften things a bit.

# Don’t be (too much of) a pedant

It can be tempting to go through a PR with a fine tooth comb and comment on every. single. little thing. This is frustrating and annoying for the author. Sometimes it’s absolutely necessary, don’t get me wrong, but you do not need to pick up on every single little grammar mistake or missing full stop in a comment for instance.

My golden rule tends to be “is this getting in the way of code quality?” - sometimes it does and in that case, go wild! But if it doesn’t, then who cares? One example I can think of recently is an AI guide we had in our codebase, where the AI had used the Americanised spelling of a word and even though it irked me, I thought “there is absolutely no value in me pointing this out”. So I left it - luckily it got fixed up by the author in their next PR anyway, so all is right with the world again now 😆

# Notice the good

This one is absolutely key. Having a barrage of criticism launched at your PR is demoralising - the least you can do is pick out a few good things. Did the author do a quick tidy up while they were there? Point it out! Did you spot them make a user experience fix that’ll make your app nicer to use? Use a heart or a clap emoji to say “good job”. Don’t just assume that the good things go without saying - shout them out! Yes, it might feel cringe and strange at first, but it’s super important to lift people up where you can and it’ll soon become second nature.

There is something to be said for being careful you don’t come across as condescending - it’s not necessary to point out every single teeny tiny thing. There is an element here of finding your own voice when you’re adding PR comments, but as an example I will quite often say things like “love how you did X here”. It’s about letting the author know “I’ve noticed that you’re doing this and it’s good” - this is especially good for behaviour you’d like to encourage someone to carry on doing in the future.

# Explain the why

Especially if you are a more senior engineer commenting on a less experienced teammate’s pull request, I think it is crucial for you to take the time to explain why you think something should be done the way you have said it should be. Don’t take it for granted that the person will know, because we can’t all have come across the same things in our careers. In my opinion, PR reviews are a vital vehicle for upskilling and mentoring others.

As an example, instead of just saying “we should add an aria-label here”, you could expand it to “we should add an aria-label here so that screen reader users will be able to tell what this button does, given the button only has an icon on it and no text”. If it’s a more complex topic and you can add a link to an article that backs you up, even better - that will allow the author to go away and read about it and learn.

Please do not use AI to explain the why - it comes across as condescending and like you couldn’t be bothered to put in the work to explain it yourself. If you want to use AI, at least paraphrase its response rather than just quoting it verbatim.

# Consider using conventional comments

If you haven’t used [conventional comments](https://conventionalcomments.org/) before, I highly recommend giving it a try - I thought it was hokey and cheesy when I first saw it, but when someone on my team started using them, I realised it was a really nice way to preface comments with your intent, making it harder to take things personally.

Here’s how it works. Instead of writing “this isn’t using the correct convention”, you write something like “suggestion: this isn’t using the correct convention” - even better if you can add an actual code suggestion showing how you think it could be improved and then maybe even explain the why.

There’s a whole bunch of categories like suggestion (as shown above), thought, pedantic, issue etc. You can read more about them on the [official website](https://conventionalcomments.org/).

> A more fun variant, which we do at my current workplace, is to think of an emoji to represent each category - this does mean that you have to make the key widely discoverable though as it can be confusing for new folks to see a bunch of emojis in comments without knowing what they mean.

# Most of all, don’t be a dick

If you take one thing away from this article, I want it to be this. In my opinion this is the cardinal rule of PR feedback and yet, we have all encountered that one colleague who is less than tactful when reviewing code. Maybe they’ve had a bad day or maybe they just have the type of personality that considers directness more important than saving people’s feelings. Maybe we’ve even been this person sometimes - I know I have, though hopefully only very rarely!

If you encounter someone like this, the best way to deal with it is with empathy and all the same tips in I’ve mentioned so far in this article. Ask them questions, get them to explain their why and most of all, don’t engage - getting involved in a fight on a PR is not a good look and it ultimately doesn’t help the project or the company you’re working for.

One of the most important mottos of software development is “strong opinions weakly held” and if someone has such a strong opinion that they won’t let it go, sometimes it’s best to just do it their way and drop it, as long as it doesn’t impact code quality negatively. Sometimes you even get to find out later that your way was better after all and then you get to say “I told you so” if only in your head (not that I know this from experience).

> I hope these tips have been helpful - these are by no means the only tips I have so if you want more, let me know! If you’d like to share your favourite PR feedback tips, I’d love to hear them - leave a comment below.