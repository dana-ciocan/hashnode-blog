---
title: "React Server Components: is history repeating itself?"
datePublished: Mon Feb 19 2024 08:03:55 GMT+0000 (Coordinated Universal Time)
cuid: clssnh51i00000bjwgkad7euf
slug: react-server-components-is-history-repeating-itself
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/oK0e-OhRMqM/upload/3b7c72730c1ea52a05abf5bfacd43f06.jpeg
tags: javascript, web-development, php, history, time-travel, react-server-components

---

React Server Components are a hot topic in front end development right now and there's a fair bit of confusion and controversy around them. I'd like to do a series of posts on the concept to further my own understanding and hopefully yours too. I figured I'd start with something that's been bothering me as I've been reading about React Server Components and other similar technologies: what's the obsession with the server? Didn't we do that already? Is this just history repeating itself? Why am I getting déjà vu?

Maybe you've been wondering about this too so let's travel back in time and see what we can learn from the past.

### Let's step into the time machine...

It's 2004 (how is that twenty years ago?!) and I am a fresh-faced Computer Science graduate. I have just started my first *actual* programming job as a web developer after graduating just as the dot-com bubble burst. I had to do data entry for a few years there while finding a graduate job that didn't require three years' experience but that's a story for another time.

My first job involved using a Python-based web framework called Zope (apparently [it still exists](https://zope.dev/)!), FTP and Dreamweaver - the height of modern tech at the time. Zope was akin to PHP and, much like PHP, ran "on the server". What this means is that when a user goes to a URL in their browser, a request is sent off to another computer on the internet (the "server"), which runs off and grabs some data from a database, combines it with a template and creates some HTML. This is then sent off to the browser to render.

Up until then, websites had largely consisted of static content - videos were still a Big Deal (and very low res) and interactivity was extremely limited, often done in special plugins that users had to download separately. Whenever you did anything on a website, the entire page would reload and this was pretty jarring - websites were slow and the user experience was not great. We just accepted it though because the technology wasn't capable of much else just yet.

### Web 2.0

Soon after that, for better or for worse, we ushered in the era of "[web 2.0](https://en.wikipedia.org/wiki/Web_2.0)" which signalled a world wide web used for social interactions much as it is now. Social media was born and rather than users creating their own websites, they would join an existing one which would host their content for them. MySpace, Bebo, LiveJournal, Flickr and eventually Twitter and Facebook came along and completely changed the face of the internet.

As demand for interactivity increased, developers had to step up their game and so AJAX became a term that was thrown around a lot at the time. I must admit that as a young developer, I didn't really get it, but let me explain it to you now. AJAX stood for Asynchronous JavaScript And XML and basically allowed developers to manipulate parts of the page without having to completely reload it, making websites feel much faster and more responsive.

In reality, all this meant was that once the HTML had finished rendering in the browser, you could get it to run a bit of JavaScript that opened a connection to a server (using [`XMLHTTPRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)) to download further data. This JavaScript code, unlike the PHP from earlier, runs "on the client" which means the user's machine, not a machine out on the internet. At the time, there was no guarantee that the user had JavaScript enabled (a lot of people turned it off due to slow connections) so we still had to do a lot of work to fall back gracefully, or at least tell the user to turn on their JavaScript to get the full experience (there was a lot of that back then).

### JavaScript frameworks

Fast forward a few years to 2010, and I'd changed jobs and the web development world looked very different. Instead of just being a "web developer" I was now a "front end developer" because the industry had grown and there was demand for specialised skills to work in different areas.

JavaScript, the underdog of the internet, had exploded and evolved into a language all of its own, something which still baffles me to this day, because when I started learning it, JavaScript was used for button rollovers and I never would have predicted its success! This was the early days though - JavaScript didn't have classes yet and it certainly wasn't supported in any kind of standard way across all browsers, but it was pretty unlikely that someone would disable it by this point.

Helper libraries popped up to fill the browser interoperability gaps - we used one called Mochikit at the time, but jQuery won out in the end and is still used extensively today. This was the era of MVC (Model View Controller); web frameworks were a dime a dozen and would die out as quickly as they appeared - AngularJS (the predecessor of modern Angular), Ember and Backbone are just some examples - before the likes of React and vue.js came along and changed the landscape forever.

### Spinners and loading states

By this point, very little code was run on the server - the user would go to a URL, a request would be made and the server would send a basic skeleton of a page back to the browser. The actual app was loaded in on the client afterwards and funnily enough this approach was known as Client Side Rendering or CSR. The main down side was that if your app was big, your user could be left staring at a blank screen for several seconds while the browser was downloading all that code, wondering whether anything was actually happening. The web had gotten all slow again, just in a different way.

To help users make sense of what was going on, the "spinner" was born. You've no doubt seem them as they're all over the internet these days - a little circular loading state indicator that shows that says "something is about to happen here, please hold on". It's not the ideal user experience, but hopefully people won't go to your site, wait a few seconds and then refresh because they think it's broken.

Unfortunately, while this addressed usability (kind of), it did not improve performance or Search Engine Optimisation (SEO). Search engine crawler bots were not sophisticated enough to be able to wait until the page had rendered to get the metadata they needed to generate a site's listing which became a real issue for companies who wanted their sites to rank well on Google, which is basically everyone at this point.

### Meta frameworks

Now we are in the latter end of the 2010s. React is the predominant JavaScript framework and I'm busy building a complex and very interactive application built in React with Redux for state management. The app is big and heavy due to the pretty animations we're using and even though it's only a few years old, we're starting to think about a serious refactor because everything is becoming unmanageable.

This is exactly why meta frameworks like Next.js became so popular. React in itself is quite unopinionated in its style and allows you to use it however you like, quite often creating a mess in the process. It's also very much a UI library so it's quite limited in scope. Next.js came with built-in routing and was a little more strongly opinionated on how things should be done (though not a great deal, admittedly), improving the developer experience and making it so teams could build apps in React much faster.

### Going back to the server

Even more importantly however, it came with something called "server-sider rendering" or SSR and this is where things are starting to come full circle. SSR is a rendering method whereby the server will create a "first pass" at the HTML for your website and send it to the client (the user's browser), which will render it - at this point, nothing is interactive yet except things like hyperlinks that work natively. Once the HTML has rendered, React will load in separately (on the user's computer, remember!) and will latch on to this existing HTML and "hydrate" it, sprinkling in the interactivity where it's needed. It could still take a few seconds for this to finish but in the meantime, the user has an almost-functional page to look at which means they're happy.

Gone is the blank page and gone is the need for loading states - plain HTML is fast and loads in quickly enough that the whole experience feels very performant. Even crawler bots are happy because the HTML can include metadata for them to use when generating an entry for their search engine. We've travelled all the way back to 2024 (sorry, that was sneaky, hope you don't get time travel sickness) and this is what I'm using in my job every day - I must admit, it works pretty well. So why do we even need React Server Components then?

### It's all about control

As far as I can see, web development has matured and gone through this whole cycle of starting off on the server, then moving to the client and finally ending up at this half-way house situation where the basic HTML is rendered on the server and JavaScript augments the page with interactivity.

The down side of server-side rendering as it was in Next.js without React Server Components is that all data fetching can only be done at the very top level of a page in a special function called `getServerSideProps` - here you will call your API and get the data you need, before then having to either store this in some kind of state manager or context provider or pass it down using props. So what if you could do this data fetching step **anywhere in your application**? This is exactly the problem React Server Components is trying to solve.

Using this new paradigm, a developer can fetch data from the server in any React component they want to, as long as it's a server component. Server components cannot be interactive as they are immutable once they have been rendered. Client components also exist - these are the equivalent of the "old" React components and will hydrate once the HTML has finished rendering. This is where the interactive parts of your application go. The nice thing is that data can be sent across the server-client boundary using props, meaning that your application will be React components all the way down - no more having to use special functions like `getServerSideProps`.

### So, are we repeating ourselves?

I feel like the cries of "aren't React Server Components just PHP all over again?" are a bit of a misnomer. Server-side rendering isn't exactly a new thing - I feel like the name "server components", although accurate, is somewhat confusing. This is just a refinement of what we've been using for a while and it addresses some genuine problems and issues to boot. There are definitely some sticking points here though - using React Server Components means adopting Next.js if you haven't already and if you have, you'll most likely have to rebuild and restructure years' worth of code.

Saying that, living in a hybrid but more flexible world where we as developers can choose exactly what is server-side and what is client-side can only be a good thing in my opinion and I'm excited to see where this new direction takes us. Maybe React Server Components will only be a stop on the way to the final destination, it's hard to say! In my experience though, if a technology creates as much noise as this has done, it's either a total winner or it's going to end up as a footnote in web development history. I'd love to be able to look into a crystal ball and see the future, but only time will tell...

> I would love to hear what you think of React Server Components - are they nonsense or genius? As for this series, my plan is to do a follow-up with some Actual Code to prove out my thinking even further. Stay tuned!