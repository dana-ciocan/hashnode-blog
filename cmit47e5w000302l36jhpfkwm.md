---
title: "A weird Playwright bug, AI (again), turning things off and on again and Advent of Code"
datePublished: Fri Dec 05 2025 17:04:34 GMT+0000 (Coordinated Universal Time)
cuid: cmit47e5w000302l36jhpfkwm
slug: weekly-roundup-05122025
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/jOeh3Lv88xA/upload/602e281eedee0bd683b5402f72195f65.jpeg
tags: ai, e2e, vscode-cjevho8kk00bo1ss2lmqqjr51, playwright, end-to-end-testing, copilot, claude-code

---

This week I’ve mostly been getting ready to launch the very first full feature I’ve built from beginning to end in my new job. It’s exciting, but also a bit nerve wracking - I want to get it right, because I want to show that I’m a good, responsible developer who checks their work before just slinging it into Production. To that end, I’ve been writing end-to-end tests and checking everything lots of times this week. This has given me a lot more confidence that the launch will be successful and I will definitely need to make sure I think about end-to-end tests from the beginning next time.

# Playwright reports can interfere with Vitest

Who knew? This was a really odd one - we recently upgraded our repo to React v19 and found that some team members were getting TypeScript errors in their Vitest files. Three of us were trying to debug this along with Gemini and Cursor and we tried things like `yarn cache clear` and deleting the `node_modules` directory, checking our `yarn` and `node` versions and so on and so forth. Nothing was amiss and yet the TypeScript error persisted.

We found the issue when my colleague who was having the issue hovered over the `it` in the Vitest test files - my other colleague saw that the type definition for `it` was being pulled in from the `playwright-report` directory. When the `playwright-report` directory was deleted, the error disappeared! How interesting.

The solution ended up being to add the `playwright-report` directory to the `excludes` array in the `tsconfig.json` and this is what we did, but if you’re anything like me, you like knowing the root cause of things. I tried to have a bit of a dig, but I couldn’t really see what was causing this. The Playwright reports are HTML files and they do contain some JavaScript injected into them in places. So maybe some JavaScript was conflicting with the types for Vitest? In any case, adding them to the `excludes` array fixes it, so maybe it’s best not to worry too much about it for now.

# End-to-end tests are a Good Thing

I almost forgot to write some end-to-end tests for a feature I’ve been working on for a while now. Luckily I remembered before it went live and I’ve been writing them this week. They caught an unbelievable amount of edge case bugs that I wouldn’t have noticed if I hadn’t written these. Very grateful to have such tools at my disposal to make the detecting of bugs like this super simple.

I had one particular bug where I got a `0` where my component should be. This was because I had a condition that determined whether my component should show that read something like `componentData && <ComponentHere />` - when `componentData` was `falsy`, I got a nice `0` in the UI. I changed it to `componentData !== undefined` instead. One to bear in mind in the future!

# Getting a bit lazy with Copilot

I’ve been using Copilot a lot to help me this week and to be honest, I’ve probably been using it a bit *too* much. I would ask it to help me and then spot the problem as it was spitting out its answer. Maybe I should take more care to check things myself before invoking the bot. It’s so tempting to just ask Copilot to do it though, isn’t it? Especially if you’re pushed for time or a bit stressed. I’m going to try and do this less though, because I should know better and I should at least have a look with my own two eyes first. Otherwise it’s a waste of compute resources and energy and I don’t want that.

# Reload before you do *anything* else

I’ve noticed this week how often I reload bits of VS Code: the window, the TypeScript server and the ES lint server. I knew the TS Server reload option existed, but the other two were new to me - I love learning little tips and tricks like this when you start working with new folks! Anyway, whenever anything goes wrong with VS Code I try one of these trusty reload methods before I do anything else. I use the Vitest extension quite a lot for both running tests and debugging them (you can set breakpoints and use all the handy debugger features if you do this, it’s neat!), but it tends to flake out sometimes and the little “play” buttons disappear. This is when reloading the window comes in especially handy. This last tip comes courtesy of my colleague who showed me this the other day - you know who you are! Thank you 🎉

# Claude Code experiments

I won the battle of the complicated instructions (that weren’t actually that complicated) and finally signed up to Claude Code this week. It’s really cool that we’re being given all of these AI tools to try out. So far, I’m enjoying it - the agent mode is pretty good and I can keep using VS Code. Not sure whether it wins against Copilot though, I haven’t quite used it enough yet - only time will tell.

Shout if you’d like me to do an AI coding agent comparison at some point!

# Advent of Code

A friend and I have been doing Advent of Code together this year. I find it helps so much to have a buddy. If I do it on my own I get demoralised almost instantly and give up on day 3. This year, day 3 part 2 was the first puzzle where I got really stuck. I don’t know what it was about it but I completely overthought my approach and didn’t really get anywhere. I ended up consulting a solution video on YouTube in the end, because I figured “not doing it and getting stuck isn’t going go teach me anything”. As soon as it was explained to me, the whole thing made sense because of course it did, and I managed to implement my own solution fairly quickly after that. I’m learning to accept that doing these kinds of problems is a skill that can be improved and you only learn by doing. Sometimes that means getting some help when you’re really stuck and that’s okay.