---
title: "Five tips that'll up your Git game"
datePublished: Tue Nov 12 2024 20:32:07 GMT+0000 (Coordinated Universal Time)
cuid: cm3ewrsh4000a09jye54i41vd
slug: five-tips-thatll-up-your-git-game
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HKUkWePHS0w/upload/5b400ec978cab5501fa57aa484e0ed8d.jpeg
tags: version-control, git, tips, cli, coding

---

I’ve been using Git for erm… at least ten years now? Probably longer. I remember the time before version control and it was *dark* - uploading straight to the Production web server using FTP, no Staging or QA/Dev environments for testing… We were hardcore and we were nervous wrecks (at least I was). Version control has saved many a developer’s neck when it comes to deploying changes to a live environment and has saved me personally a heck of a lot of time and energy when coding every single day.

I’ve managed to collect quite a few Git tips over the years and I thought I’d share them - I might do a second (and maybe third?) one at some point because I have more!

# Tip 1: commit little and often

Trust me on this one - even when you think “there is no point to committing anything yet”, do it. I have accidentally lost my changes way too many times after not committing when I should have - I learned this lesson so you don’t have to. Once you’ve reached a point where you’ve done a concrete “thing”, commit it. Did you add a function? Make a commit - with tests, of course. Did you refactor a class? Make a commit. Anything that can easily be described in a commit message like “Add a function to get the latest prices” or “Call API endpoint to get most read articles” deserves its own commit. This practice, by the way, is called “atomic” commits and I might do another post about it at some point because I could talk about it for ages.

Have you ever gotten yourself into a refactoring mess? I mean when you start refactoring something because, well, it needs to be refactored, and you’ve edited twenty files and you’ve gotten yourself into a massive tangle and you just end up starting over instead of trying to figure it all out? Yep! I’ve done it too ☠️ Atomic commits can really save you here, because you’ll generally have an idea of the separate things that need to be done to get this to work and committing each little bit independently means it becomes much easier to roll back to a state where you *know* things were still working correctly. No more starting from scratch! It also forces you to plan a bit more, rather than just attacking the problem from all angles and hoping that it’ll magically work itself out.

# Tip 2: learn the command line

This might seem a bit old-fashioned - there are plenty of great GUI-based tools for Git these days - but I do think you learn more about how Git actually works if you learn how to use the command line. Yes, it’s annoying having to remember the commands and yes it takes a while for it all to stick, but once it does, you have a great grasp of Git and you will be able to do *so* much more with it.

Unfortunately, you’ve gotta learn the Git CLI by doing it and there’s not really a way around it. I would recommend giving [the Pro Git Book](https://git-scm.com/book/en/v2) (available for free!) a read - it’s extremely helpful and very well written. Once you start learning how branching *actually* works in Git (not how you have conceptualised it in your head), a lot of things will start to click and you’ll be a pro in no time.

# Tip 3: do not use aliases

Don’t do it!

This was a tip I actually got from someone else - the idea is that if you’ve set up an alias, say, `gc` for `git checkout`, then if you SSH into a server that doesn’t have those aliases set up, you’re a bit stuffed. And in a situation where you’re dealing with an outage, you don’t want to be asking your favourite chatbot/search engine what the commands are again because this takes precious minutes to do. This example is perhaps over-simplified and contrived, but there are some quite complex aliases you can create to save yourself typing time and having to remember those off by heart would be tough. I did away with aliases when a colleague made that point and I must say, I haven’t missed them. At the very least, I would try to use the full commands every once in a while so that you don’t forget them - our brains so very quickly forget things it doesn’t consider important any more.

# Tip 4: `git switch -`

If you haven’t discovered the wonders of `git switch -` yet, I am about to blow your mind! The `switch` command is a relatively new addition to Git and splits the branch switching functionality of `git checkout` into its own command (in case you didn’t know, the checkout command actually does *several* things, not just switching branches - you can read more about it in [the Pro Git book](https://git-scm.com/docs/git-checkout)).

The most exciting thing about the `git switch` command though is that you can give it a dash (`-`) as an argument, and it will switch back to the branch you were just on! Say you’re on `main` and you switch to `my-super-branch`. Typing `git switch -` will take you right back to `main`. How cool is that?! Okay, maybe it’s just me who gets excited about this kind of thing.

This is honestly the main reason I started using `git switch` instead of `git checkout` and I must use this command at least a hundred (okay maybe not quite) times a day. Just think of all the typing you can save yourself…

> UPDATE (03/12/2024): I’ve just been informed that `git checkout -` also works - so if you haven’t adopted `git switch` yet or you don’t want to, you don’t have to for this tip (thanks Marcus!)

# Tip 5: Git will generally tell you what’s up

Are you in the middle of sorting out conflict hell? Doing an interactive rebase and you’ve lost track of what bit you’re on? Just not sure whether you pushed or not? The `git status` command is your absolute best friend.

It took me an embarrassingly long time to figure this out, but typing `git status` will quite literally tell you what you need to do next the majority of the time.

Come back to a repo after not touching it for a while?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731443243801/b089df6b-a39e-49de-8c24-83adab690c9b.png align="center")

Just type `git status` and you can instantly see what you were last working on.

In the middle of an interactive rebase?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1731443303976/6d3ca566-427e-4afd-97d8-5c9005801aae.png align="center")

That same `git status` command will tell you what you’re supposed to be doing next.

Next time you’re confused in the middle of your workflow, try using `git status` and see if it’ll help you out!

> That’s it for today’s tips and let me know if you’d like to hear more of these