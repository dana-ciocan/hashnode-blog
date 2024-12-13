---
title: "Why are there so many types of JavaScript modules?"
datePublished: Tue Nov 05 2024 21:28:16 GMT+0000 (Coordinated Universal Time)
cuid: cm34yp0r0000409jqhtihg3mx
slug: why-are-there-so-many-types-of-javascript-modules
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/7eQlPra81zQ/upload/6213297cfb02b07953623c9d17ffb042.jpeg
tags: javascript, ecmascript, es6, commonjs, javascript-modules

---

Let’s cast our minds back to 1995. Netscape Navigator was the predominant browser folks were using to get their internet fix (if at all - there was certainly no guarantee you had the internet at home back then!) and connecting to the internet [sounded like a portal to hell was opening up right underneath your modem](https://www.youtube.com/watch?v=gsNaR6FRuO0)…

This was the year JavaScript came into the world, kicking and screaming - famously invented in just *ten days* by Brendan Eich, it allowed you to write code that ran in the browser and didn’t require you to jump through all sorts of server-based hoops. Most people writing hobby websites only had access to hosting that would allow you to render HTML, so having the power to run code in the browser without needing a server to run Java or CGI script was a big boon.

It didn’t really take off all that quick to begin with - most people kind of considered JavaScript a bit of a joke and not a “serious” language. You could hardly blame them - object-oriented languages were The Thing at the time and JavaScript didn’t even have a `class` keyword! It ended up being used for button rollovers and cute animations and played no small part in the internet culture of the 90s, but certainly wasn’t the powerhouse it is today.

# 1997: the ECMAScript standard

This is worth a mention, because these days we refer to the version of JavaScript we are using as “ES6” or “ES2022” and this is where this came from. ECMA is a European organisation that aimed to standardise a bunch of computer-related technologies. The ECMA-262 standard was for a general purpose scripting language and even though JavaScript was invented before the standard was written, it conforms to it. ECMA have other interesting standards too, like ECMA-404, for JSON. You can read [the current specification for ECMAScript](https://ecma-international.org/technical-committees/tc39/) (aka JavaScript) on ECMA’s website.

# Y2K (ish): JavaScript persists

Despite being seen as a bit of a joke, JavaScript stuck around. Writing anything more than a handful of lines of it was tricky though. There was no tooling available and the only way you could add it to your websites was by adding a `<script>` tag to your HTML, so the developer experience was *horrible*.

More and more `<script>` tags would get added to HTML files, which adversely affects performance (every network request adds latency) and makes the code even more difficult to manage - just making sure that files earlier in the list of `<script>` tags didn’t use any functions from files lower down the list was a nightmare!

As more and more code was written, minifiers became commonplace. These are tools like [JSMin](https://www.crockford.com/jsmin.html) (invented by Douglas Crockford) that remove any comments and unnecessary spacing from files. This allowed developers to write more code but use less bandwidth as the files were smaller. It was all about saving those bits back in those days, much as it is now to be fair!

# 2005: the first JavaScript libraries

We developers are lazy and if we can find a way to reuse code, we will. By now everyone knew that JavaScript was here to stay, joke language or not, so various libraries came out that built *on top* of JavaScript, turning it into something more serious.

Libraries like MooTools, which gave JavaScript object-oriented capabilities, Underscore (the predecessor to lodash), which gave developers access to all sorts of common utility functions, jQuery helped us herd the DOM in a more straightforward manner and there were loads more.

You have to remember, this is all before NPM, so libraries were simply included using `<script>` tags - the files were either downloaded to your server and hosted there or you could use a CDN.

# 2009: the advent of Node.js

Up until now, JavaScript could *only* run in the browser. Now that we had finally decided JavaScript wasn’t a joke any more, developers wanted that same power on the server - who wants to switch languages for the back end? Node.js was the answer to this problem.

There is no DOM in the backend and therefore no way to insert a `<script>` tag to insert your library of choice, so a different solution had to be thought of. This solution was invented by Kevin Dangoor at Mozilla and was initially called ServerJS, but is now better known as CommonJS.

You may have seen code like this:

```javascript
const { STRAWBERRY, APPLE } = require('./fruits');

const myFavouriteFruits = [ STRAWBERRY, APPLE];

module.exports = {
  myFavouriteFruits
};
```

Obviously, this is a very contrived example, but any time you see `require` or `module.exports`, you’re dealing with a CommonJS file.

This is JavaScript’s very first concept of a “module” and was borrowed from other programming languages which already had this idea.

# Also 2009: RequireJS and AMD

It’s worth mentioning here that around the time CommonJS came out, developers who were working in the browser went “we want modules too!” and an in-browser version of a module system was created - this was called RequireJS.

Under the hood, this actually uses the Asynchronous Module Definition (AMD) system - the interesting thing about this is that CommonJS is very much synchronous. Adding asynchronous functionality to the module system makes it great for browsers, where we want to be able to do things asynchronously for performance reasons.

Having never used AMD directly, it always looks weird to me - here’s a little snippet:

```javascript
define(['calculate, alert'], function(calculate, alert) {
  var values = [1, 3, 9];
  var calculation = calculate(values);
  alert('Hello');
  document.getElementById('calculation').innerHTML = calculation;
}
```

It has this dependency injection-like pattern, where `calculate` and `alert` are functions that come from other files (let’s say `calculate.js` and `alert.js` respectively) and are passed into this block so they can be used inside it.

# 2010: NPM joins the table

It’s all happening in JavaScript land! Now that there is a module system, folks want an easy way to add modules to their programs and Node Package Manager (or NPM) is just the thing. NPM worked on the server, but there were other tools around for the client (e.g. Bower). This is when we really started cooking with gas.

For all the controversy around NPM and `node_modules`, it has still made our lives a lot easier and has improved the developer experience no end, making us far more productive than in the early days, when every bit of code had to be hand-rolled.

# 2015: UMD - one module system to rule them all?

With the line between the server and client blurring in JavaScript land, someone decided it would be a good idea to create a “Universal module System” aka UMD. This type of module will try to figure out whether the code is running on the client or the server and act accordingly. Here is a snippet:

```javascript
(function (root, factory) {
  if (typeof define === 'function' && define.amd) {
    define(['exports', 'b'], factory);
  } else if {
    factory(exports, require('b'));
  } else {
    factory((root.myModuleName = {}), root.b);
  }
}(typeof self !== 'undefined' ? self : this, function (exports, b) {
  exports.action = function () {};
}));
```

This comes from the official [UMD repo](https://github.com/umdjs/umd) and basically checks whether it is possible to run code on the client and if so, uses AMD. If not, it uses CommonJS. If neither of those are an option, it uses global variables instead.

# 2015: ECMAScript 6

Unfortunately for UMD, that same year, another module system was announced and this is the one that everyone has kind of stuck with ever since. It’s called ES Modules and is often abbreviated to ESM and was part of the ECMAScript 6 (ES6 or ES2015) standard. This is the friendly neighbourhood `import/export` statement that we’re all used to.

If we rewrite our (very contrived) fruits example from before, we get:

```javascript
import { STRAWBERRY, APPLE } from './fruits';

export const myFavouriteFruits = [ STRAWBERRY, APPLE];
```

And this takes us to the end of our whistle-stop tour of JavaScript module land. ES Modules are here to stay - so much so that they are now being used on the server as well as the client and are compatible with TypeScript. CommonJS, AMD and UMD are all slowly being abandoned for the much friendlier `import` and `export` keywords of ESM.

# The future?

The future is definitely ESM for now, though who knows what else might come along - it feels like this is kind of it though… TypeScript is very much present and compatible with ESM too, so I can’t see it going away any time soon. It’s interesting to think that all of these systems were created to deal with performance issues - perhaps one day the HTTP protocol and browsers will be optimised to such a degree that we won’t need as many of these tools. We can but dream!