---
title: "Troubleshooting tree-shaking"
datePublished: Mon Nov 06 2023 08:19:41 GMT+0000 (Coordinated Universal Time)
cuid: clommsz0k000009jg7nr95c2u
slug: troubleshooting-tree-shaking
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/t3ofrCzqtes/upload/ed15f92a3e12186001b08ce4087d0748.jpeg
tags: javascript, typescript, tree-shaking, component-libraries, es-modules

---

I have spent the last couple of months working on making a UI library (specifically a collection of React components for reuse in other projects) tree-shakeable. In that time, I felt like I read almost every article on tree-shaking that exists on the internet and yet some important tips were missing, leading to me not being able to find a solution to my problem. To address this gap, I thought I'd write my own post, walking you through what I found.

If you don't know what tree-shaking is, there are some wonderful articles out there - try these on for size:

* [https://www.smashingmagazine.com/2021/05/tree-shaking-reference-guide/](https://www.smashingmagazine.com/2021/05/tree-shaking-reference-guide/)
    
* [https://webpack.js.org/guides/tree-shaking/](https://webpack.js.org/guides/tree-shaking/)
    
* [https://blog.theodo.com/2021/04/library-tree-shaking/](https://blog.theodo.com/2021/04/library-tree-shaking/)
    

This post will not go into this as there's already plenty of info out there. This is for people who are in the middle of writing a library and finding that they're just not able to get their project to tree-shake. It's basically the article I wish I'd found when I started this journey!

### Are you outputting ESM?

One of the most important things to get right is to make sure your code outputs [ES Module format aka "JavaScript Modules"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules). None of the other JavaScript module formats (CommonJS, UMD, AMD etc.) will allow a bundler to tree-shake.

What this means is setting up your library's build tool so that it converts whatever you are writing (be it JavaScript, TypeScript or whatever else) into ES Modules code that can be used by consumers.

There are many ways to do this, but I would recommend a tool that is specifically touted as an ESM bundler or compiler i.e.:

* [Rollup](https://rollupjs.org/guide/en/)
    
* [esbuild](https://esbuild.github.io/)
    
* [SWC](https://swc.rs/)
    

You could even just let the TypeScript Compiler (tsc) or Babel transpile the code - whatever you prefer!

> I did try Webpack for this step as well but found it extremely cumbersome, then found out later that ESM support has been experimental in it since 2016, so in my opinion it's best avoided for transpiling your library and used for bundling your consuming app instead.

Most developers (me included) think that converting to ESM is all you need to create a tree-shakeable library, but things are a bit different when your library isn't just plain first-party JavaScript and I couldn't get the consuming app to tree-shake, no matter how hard I tried. If this is you, read on!

### Do you have any side effects in your code?

If you do, this could be preventing your library from tree-shaking.

From the [Webpack documentation](https://webpack.js.org/guides/tree-shaking/#mark-the-file-as-side-effect-free):

> A "side effect" is defined as code that performs a special behavior when imported, other than exposing one or more exports. An example of this are polyfills, which affect the global scope and usually do not provide an export.

This is a very specific example and you're unlikely to be writing your own polyfills, but you could otherwise accidentally be adding side effects. If the code in your library affects anything outside its own scope, you have a side effect and you'll need to address it.

This includes:

* Setting global variables
    
* Setting attributes on `window`
    
* Amending a JavaScript `prototype`
    

I'm sure there are other examples, but hopefully, you get the gist. Make sure you just expose your library's functions and don't do anything that has the potential to change things in your consuming app.

### No, really, do you have any side effects?

I dismissed side effects as an issue initially because none of the code in our library was messing around with things outside of its own scope.

The big gotcha here is that the bundler in your consuming app may think a third-party library is producing side effects and decide not to drop any of the files it's mentioned in out of an abundance of caution.

I finally managed to figure this out after discovering the ES lint plugin [eslint-plugin-tree-shaking](https://www.npmjs.com/package/eslint-plugin-tree-shaking) - as soon as I installed it, all mentions of a certain third-party library we were using went red and the error mentioned, you guessed it, side effects.

This is when it suddenly clicked: Webpack (the bundler in the consuming app) thought this third-party library was introducing side effects and was pulling in the whole library just to make sure nothing could go wrong.

Bundlers like Webpack will honour the `sideEffects: false` directive if you include it in your `package.json` so that ended up being the solution - as soon as I added this line, the consuming app only pulled in the bits of the library that were actually being used. This is akin to telling the bundler "oh, this thing you're worrying about, just ignore it" though so definitely more of an escape hatch than a real solution.

I checked the third-party library and could not see any side effects being introduced, so have used this technique for now, but we are considering whether it would be better to build our own version of this third-party library (it's not very complicated) to be able to say our library is tree-shakeable to our future consumers with confidence.

The lesson here is to be careful with introducing any third-party libraries - even if the code you're adding through them is side effect-free *now*, there is no guarantee for the future and every time the maintainers release an update, you will have to check it again. The only time I'd feel comfortable introducing a third-party library now is if tree-shaking was a top-tier feature for the library's contributors to maintain.

### Other things to be aware of

There were definitely some other issues that slowed down progress for me and I thought I'd mention them in case it rings a bell for any of you:

* **Using non-JavaScript files** - we had CSS files in our project (it's a React-based UI component library), which definitely made things more difficult for us. It meant that tree-shaking tooling like [agadoo](https://www.npmjs.com/package/agadoo) (a CLI tool for checking whether your library will tree-shake) wasn't able to check the code because it doesn't have support for CSS (it uses Rollup with no plugins under the hood). In the end, the [ES lint plugin](https://www.npmjs.com/package/eslint-plugin-tree-shaking) gave us the tooling we needed to check whether our library was tree-shakeable instead
    
* **Using postCSS** - we want to be able to use the latest CSS features and transpile them to widely available CSS at build time. Unfortunately, this caused us a whole bunch of grief because most build tools assume you want to inject the code in the `<head>` tag and we definitely didn't want to do that. I found that [esbuild](https://esbuild.github.io/) was able to handle what we needed, which was just to transpile every CSS file using postCSS and leave the directory structure intact
    

Okay, that's it from me - I hope this article has been useful for you. It's one of my first here on Hashnode so if you do leave any feedback, please be kind!