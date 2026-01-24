---
title: "Weekly roundup: 23/01/2026"
datePublished: Sat Jan 24 2026 21:22:57 GMT+0000 (Coordinated Universal Time)
cuid: cmkstg9ni000b02jodpv9d1gw
slug: weekly-roundup-23012026
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/JKUTrJ4vK00/upload/cb684b7cbcd2c32d760fbc1cd123d849.jpeg
tags: ai, artificial-intelligence, monitoring, multitasking, feelings, alerting

---

This week has been busy and a touch stressful. I’ve been working on a couple of things that felt like high priority and context switching quite a bit, which is something I have accepted I will never get good at. It was a good week for learning things though - I learned about how we do certain things at Octopus, which even though I can’t talk about it here, is useful for me going forwards, and I learned a bunch more about Next.js app router. It still blows my mind every time I remember that client components aren’t *just* rendered on the client! I know that sounds silly, but I keep forgetting it and then re-learning it. Anyway, it’s been a week. Here’s some of my observations.

# 📈 Monitoring is *so* important

I just happened to be working on adding logs and end to end tests for one of our journeys when we had a report that customers were seeing some weird errors on that particular page. I speed-merged the logging changes (followed swiftly by the end to end tests) and we immediately started seeing some interesting stuff in our monitoring platform. It turned out that the journey was not showing any error messages, meaning that users were rage clicking the submit button, further elevating our error rate. After some discussion, we decided to change the front end so that our customers got a nice friendly error message and the submit button disappeared when there was an error. You know what I’m going to say, but because I had end to end tests, that refactor was super easy to do and once it was merged, we immediately saw our error rate fall. Fingers crossed our users will feel less frustrated going forwards too. Adding monitoring to your applications is *incredibly* important and I would not skimp on it - adding it in as you go is a lot less effort than trying to retrofit it and you will benefit hugely from being able to see where your application’s problem areas are. It doesn’t even have to be pricy, you can use open source technologies like OTel, Elastic and Grafana, so there is literally no excuse.

# 🤖 Will AI put us under more pressure?

I found myself multitasking with the help of AI quite a bit this week. I would ask Claude to write an end to end test (for example), while I was off on another screen researching Next.js app router. I found myself wondering whether this is a good or a bad thing. Yes, having an agent in your pocket means they can do one task while you do another, but will that kind of multitasking mean we won’t do either thing well? You still have to guide an AI agent (for now at least) while they’re doing their work so it’s not possible to fully focus on the other task you’re doing. I ended up feeling rushed and overwhelmed and like I needed to be able to do it all. Not that this feeling is unusual to me, even when I’m not using AI. I guess I’m just wondering whether the temptation to let our agents be our ultimate multitasking buddies will be too great to ignore. I certainly found myself falling into this trap more than once this week.

# 🙋Knowing when to ask for help is a skill

I was working on a POC with a colleague this week and we got to a certain point and realised we were just kind of… stuck. So rather than bashing our heads against the wall, we went back to our team and arranged a couple of meetings with other people who had expertise in this area. It helped a lot and we are now unstuck again! It can feel like defeat, to say “okay, I can’t figure this out myself so let’s ask someone else for help” but actually, it’s a superpower. It’s an honour and a privilege to work alongside lots of clever people and it’s actually a really good thing to make the most of it and learn as much as you can from them. And in the meantime, you’re not wasting a load of time trying to figure something out by yourself.

# 😞 Feelings are great teachers

Because this week was stressful, I had some feelings - a bit of overwhelm and a bit of frustration. And that’s okay. It’s *totally* okay to feel those things at work, even when you have a job that you largely enjoy - this was a thought I had as I was kind of shaming myself for having feelings. It’s super important to acknowledge our emotions, because if they’re uncomfortable, they’re usually a sign that something isn’t right. Whether that’s something within ourselves or with our surroundings doesn’t matter - awareness is the first step and will allow us to course correct. In this case I was just trying to do too much and spreading myself too thin. I had also made some assumptions without checking in with folks whether my approach was correct, which is a recipe for frustration and a lesson I still forget sometimes. Lesson learned (again), let’s hope I don’t forget it again so soon!