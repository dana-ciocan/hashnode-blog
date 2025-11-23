---
title: "TIL: how to display markdown files in Next.js"
seoTitle: "How to display markdown files in Next.js"
seoDescription: "Learn how to display markdown files using Next.js' app router easily and efficiently with this step-by-step guide"
datePublished: Sun Nov 23 2025 08:46:05 GMT+0000 (Coordinated Universal Time)
cuid: cmibh440g000502l2dotd5c3m
slug: how-to-display-markdown-files-in-nextjs
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/OyCl7Y4y0Bk/upload/49e0b54bb4d37ad77c211a3feb679e04.jpeg
tags: markdown, nextjs, app-router

---

> This article is part of a new [”Today I learned” series](https://danaciocan.com/series/til), where I share thing I learned that you might find useful too

I want to learn how to use Next.js’ app router because I’m about to start using it in anger at work and I want to be ready. So I started thinking about how I would rewrite this blog in it. I might end up using the end result, I might not, we’ll see - it’s just a good practice opportunity more than anything.

Hashnode lets me export all my articles as markdown files, so it makes sense to see whether Next.js can display markdown. Turns out, it can and it’s super easy! Let me show you how…

# Create a new app router project

If you’ve already got one, you can skip this step. If not, do the following:

1. Open your terminal and type `npx create-next-app`
    
2. Vercel’s `create-next-app` utility will ask you a bunch of questions:
    
    1. **What is your project name?** enter a name, or leave blank for the `my-app` default
        
    2. **Would you like to use the recommended Next.js defaults?** you can say yes to this but I always say no because I like having control, so if you want to do that too, select “No, customize settings”
        
    3. **Would you like to use TypeScript?** select yes (we shouldn’t be using JavaScript for new projects in this day and age)
        
    4. **Which linter would you like to use?** your preference here; I selected Biome because I’ve not used it before and I’d like to try it out
        
    5. **Would you like to use React Compiler?** I selected “no” because a blog is very static and won’t require memoization
        
    6. **Would you like to use Tailwind CSS?** I selected “no” but it’s not relevant for this example so feel free to choose whatever you’d like
        
    7. **Would you like your code inside a** `src/` **directory?** I said “yes” here because it’s what I’m used to
        
    8. **Would you like to use App Router?** this is the biggie - select “yes” here
        
    9. **Would you like to customize the import alias (\`@/\*\` by default)?** select “no” - it’s not important for our example
        
3. Your project should be created in a directory matching the name of your app 🎉
    
4. Open your new shiny app in your favourite IDE
    

# Install the markdown dependencies

We need to install `@mdx-js/loader` ([Webpack loader](https://www.npmjs.com/package/@mdx-js/loader)), `@next/mdx` ([Next.js plugin for MDX](https://www.npmjs.com/package/@next/mdx)) and `@types/mdx` ([type definitions](https://www.npmjs.com/package/@types/mdx), so this works with TypeScript).

Here’s the install command for those modules - just copy/paste this into your VS Code terminal and hit enter:

```bash
npm install @mdx-js/loader @next/mdx @types/mdx
```

> The Vercel documentation says you should install `@mdx-js/react` as well, but the [NPM page](https://www.npmjs.com/package/@mdx-js/react) for this module says it’s not needed, so let’s not add an unnecessary dependency!

# Update the Next.js config

We need to update our Next.js config to display markdown files:

```typescript
// Import the Next.js markdown plugin
import createMDX from "@next/mdx";

/** @type {import('next').NextConfig} */
const nextConfig = {
  // Add the .md and .mdx extensions so Next.js can handle them
  pageExtensions: ["js", "jsx", "md", "mdx", "ts", "tsx"],
};

// Make sure the markdown plugin runs on .md and .mdx files
const withMDX = createMDX({
  extension: /\.(md|mdx)$/,
});

// Add the MDX config to your Next.js config
export default withMDX(nextConfig);
```

Simple! Onto the next step.

# Add an `mdx-components.tsx` file

In your application root (if you opted to have a `src` directory, it’ll go in there), add a file called `mdx-components.tsx` with the following contents:

```typescript
import type { MDXComponents } from 'mdx/types'
 
const components: MDXComponents = {}
 
export function useMDXComponents(): MDXComponents {
  return components
}
```

This defines a function `useMDXComponents` that will render all the content in your markdown files, converting it to HTML as it goes.

This file will let you do things like replace HTML elements with React components or add classnames to the auto-generated HTML elements, but we don’t need to worry about that for now.

# Put your markdown files in the `/app` directory

Now that all the setup is done, you can add your markdown files to the `/app` directory - I grabbed the very first post I ever did on this blog and put it in an `introduction` folder - you’ll have to name the markdown file `page.md` to match the app router’s filename rules. So in my case, my markdown file lives at `/src/app/introduction/page.md`.

Now run your local dev server by running `npm run dev` and go to `http://localhost:3000/introduction` (or wherever you put your file) and you should see your markdown file in all its glory:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1763887385844/c7123f0e-59c1-4e80-b770-56fd5b7aa5ae.png align="center")

It’s not pretty, because it needs styling etc, but it works! How cool is that?