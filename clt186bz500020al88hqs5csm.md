---
title: "Next.js pages vs app router"
datePublished: Sun Feb 25 2024 08:05:32 GMT+0000 (Coordinated Universal Time)
cuid: clt186bz500020al88hqs5csm
slug: nextjs-pages-vs-app-router
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/6rkJD0Uxois/upload/43eb295a915d0c86b0db7cf88b8d83ef.jpeg
tags: reactjs, comparison, frontend-development, nextjs, app-router, pages-router

---

Next.js v13, released in October 2022, caused a whole load of ruckus in the front end development world. In May of that year, [Next.js had put out a "Layouts RFC"](https://nextjs.org/blog/layouts-rfc) that announced the big paradigm shift that was to come. This is the biggest change to Next.js we'd seen in a while and if you're not sure why the `app` router made everyone go wild, keep reading.

### What is Next.js?

> You can skip this section if you're already aware, but I thought I'd add a bit of info for anyone who hasn't been working in the React ecosystem of late.

Next.js is a React "meta framework", much like Analog is for Angular and Nuxt is for Vue. React itself is a JavaScript library for building user interfaces and does not have things like routing, build tooling, different rendering methods or even opinionated file structuring out of the box. Providing these things means developers can create a fresh React app with Next.js and just start coding without having to do a load of boilerplate work, increasing velocity and generally making everyone happier and more productive from the get-go, or at least that's the idea!

### What is the `pages` router?

The big feature that makes Next.js so attractive to those of us working in React projects is the built-in routing. Up until v13, this was provided with what's called a `pages` router - this works by creating a `pages` directory in your project - every file that's created in here becomes a path on your website:

```plaintext
|_ pages
   |_ product
      |_ [id].tsx
   |_ _app.tsx
   |_ _document.tsx
   |_ index.tsx
```

In this case, your page will have two paths:

* **/** - or the home page; this is powered by the `index.tsx` in the root of the project
    
* **/product/\[id\]** - this is known as a "dynamic route" and any value given after `/product/` gets turned into a variable. For example, going to `/product/1234` will make a variable called `id` available using the `useRouter` hook which will be set to `1234`. This, in turn, will allow you to fetch the data for the given product ID from your API and display the relevant information
    

The `_app.tsx` and `_document.tsx` are files used for the "top-level" of your app - `_document.tsx` is used to amend the default `<html>` tag around your app and `_app.tsx` allows you to change the way Next.js initialises your app and add things like common layouts to all your pages.

> If you want to have a go at playing with this setup, I have a Github repo for that - go to [https://github.com/dana-ciocan/pages-router-test](https://github.com/dana-ciocan/app-router-test) to have a look

#### Pros of the `pages` router

* Creating new routes is straightforward
    
* The mental model of folders and files translates easily into URL paths
    
* This router is very stable as it's been available for years so you shouldn't run into any issues in Production
    

#### Cons of the `pages` router

* **Every** file in this directory becomes a route - this means that any helper files like tests or utility functions have to be stored *away* from the pages they are associated with, causing mental overhead in locating those files and a messy file structure
    
* Data fetching has to be done at the top level in a special function (`getServerSideProps` or `getStaticProps` depending on the rendering model) and passed down to all components - this is at best inconvenient and at worst can create a tangled mess in your code
    
* Having to use `_app.tsx` and `_document.tsx` for app-wide features is painful; these files often become huge and unwieldy and nobody wants to touch them in case it'll break something across the site
    
* You can't use the latest React features (chiefly React Server Components) with it - while this isn't necessarily an issue as your site will still work, it may become one as Next.js more heavily invests in the `app` router and leaves older features behind
    
* You can't use global CSS in child components - you will get an error and will have to scope your CSS using something like CSS modules, even if you know for sure that your CSS is not going to clash (for example, using BEM syntax). This can be very annoying as having to use CSS modules adds overhead in terms of having to use `styles.classname` instead of using the class name directly.
    

### What is the `app` router?

Next.js v13 gave us the `app` router - a new paradigm. But how does it work? Well, instead of creating a `pages` directory, the directory is now called `app`, but the differences don't end there. Looking back at the same routes from the `pages` router section above, these would instead be structured as follows:

```plaintext
|_ app
   |_ product
      |_ [id] 
         |_ page.tsx
   |_ layout.tsx
   |_ page.tsx
```

At first glance, this looks less obvious - what's with the `layout.tsx` file and why do we have two `page.tsx` files? And then there's the extra nesting for the `[id]` directory - "what is the meaning of this?", you might be thinking to yourself.

Well, every `page.tsx` file in this model represents a path on your website. This means that if you have twelve routes, you'll have twelve `page.tsx` files. In this case we have two routes (`/` and `/product/[id]`) and therefore two `page.tsx` files.

The `layout.tsx` file contains global code that will get applied to all your pages and is known as the "root layout" - it is the replacement for `_app.tsx` and `_document.tsx`. Every subdirectory can contain another `layout.tsx` file and it will only get applied to the `page.tsx` files in that directory - all you have to do to create a sub navigation that only applies to product pages is add a `layout.tsx` file to the `products` directory. This is something that is a lot trickier to do in the `pages` router.

> If you want to have a go at playing with this setup, I have a Github repo for that - go to [https://github.com/dana-ciocan/app-router-test](https://github.com/dana-ciocan/app-router-test) to have a look

#### Pros of the `app` router

* Being able to leverage React Server Components will allow developers to have more control over what code is run in the browser and what is run server-side; client-side bundles should be a *lot* smaller with this new paradigm, improving performance significantly
    
* No more doing all your data fetching in the top level page component and having to prop-drill to get it to your UI; data can now be fetched on the server in any React component in your tree and passed down to its children
    
* Nested layouts is the true superpower of the `app` router in my opinion - the fact that adding shared components to a section is now as easy as creating a new `layout.tsx` file is a major improvement over how this would be done previously and provides a lot more flexibility
    
* You can put other files in with your routes! Your file will only become a page on your site if it is named `page.tsx`. This is an absolute *godsend* for those of us who have been working with the `pages` router and struggling to know where to put our test and utility files
    
* Handling metadata is a lot simpler using the `app` router - whereas previously we'd have to use the `<Head>` component to overwrite the default `<head>` tag, now metadata is handled explicitly using either a `metadata` object or a `generateMetadata` function
    
* Global CSS is allowed! It is automatically scoped to the component in which it is imported, so no more having to use CSS modules if you don't want to. This is a benefit I haven't seen mentioned in many places, but it's really useful for things like UI libraries, where you might want to use native CSS with text-based class names instead of having to rely on CSS modules to scope the styles
    

#### Cons of the `app` router

* React Server Components are not 100% bullet proof in Production just yet; there are still issues with them and until these are ironed out, you may have to fall back to using client components (aka React components as they were before this paradigm shift)
    
* There are lots of repeated file names everywhere and this can potentially get a bit confusing - having multiple `page.tsx` files open in your IDE can make it to difficult to know which is which and finding the right file can be trickier, especially in large apps
    

### High level feature comparison

Here is a summary of the features each type of router provides:

| Feature | Pages router | App router |
| --- | --- | --- |
| SEO optimisation | ✅ | ✅ |
| Middleware | ✅ | ✅ |
| Server-side rendering (SSR) | ✅ | ✅ |
| Static site generation (SSG) | ✅ | ✅ |
| `getServerSideProps` | ✅ | ❌ |
| `getStaticProps` | ✅ | ❌ |
| API routes | ✅ | ❌ |
| React Server Components | ❌ | ✅ |
| Nested layouts | ❌ | ✅ |
| Server actions | ❌ | ✅ |
| Route handlers | ❌ | ✅ |
| Explicit handling of metadata | ❌ | ✅ |

Notice that both types of router provide server-side rendering and static site generation (which come with the added SEO benefits), it's just the implementation details that are different. Middleware is also available in both, so you won't miss out on it if you are still on the `pages` router.

### Migration

Given a small app with a few fairly simple routes, a migration could take very little time. It's just moving your routes from one directory to another and restructuring them as you go. No biggie!

However, if you have a large app with a lot of legacy and custom code in it where features have been hand-rolled rather than using the tools Next.js has provided, you could seriously struggle and this could be a labour of several months if not years, especially if you are building features at the same time. This is because you'll have to refactor your codebase before you are even able to consider migrating, which in itself could be tricky to plan as the changes could be high risk given they will affect the entire app.

Migrating from `pages` router to `app` router may not be straightforward, but it can in theory be done piecemeal. The current version of Next.js (v14) supports both in tandem and given how relatively new React Server Components still are, my bet is on it staying like this for some time to come. This means you don't have to do it all in one big go and can hopefully move easier routes over before migrating the more complex ones.

### Why did we need a new router?

Just to make it super clear, both types of router provide the same functionality, just in a different way, with `app` router giving developers more control over exactly how to structure their code and how much code gets sent to the browser at render time. Just because `getServerSideProps` is no more does not mean that server side rendering does not exist in the `app` router. Middleware is also available in both versions and so are all of the other Next.js features we already know and love.

So why on earth did Vercel introduce this paradigm shift? Couldn't they have just stuck with the old reliable and made things easier on all of us?

This is all to do with React Server Components and the desire to buy into that ecosystem. The `app` router and React Server Components are very much intertwined and Vercel are putting all their eggs in that basket in the hope that it will pay off long term. They are clearly seeing a lot of potential in the technology to the point where several people from Meta joined Vercel to help them implement it.

### So, the million dollar question: which should you use?

This largely comes down to how willing you are to be on the bleeding edge. As of writing in February 2024, app router is stable (it has been since v13.4), but React Server Components still aren't **quite** production-ready. If you're willing to use them regardless and deal with the consequences, go for it! What this means is that you may have to get comfy raising issues in Github when you come up against a problem because you might be the first one having it, or using the old client components when you can't find a workaround.

If you're about to build an app in Next.js then you might as well go with the he `app` router as it is the way everything is heading. You just might have to accept that you will have to find workarounds for issues and fall back to using client components if necessary. Alternatively, you could use the `pages` router initially and move over later, but this isn't always going to be straightforward, especially for larger apps as we've seen, so I would still recommend going with the `app` router personally.