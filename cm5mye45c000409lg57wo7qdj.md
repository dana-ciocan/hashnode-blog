---
title: "Unlocking OAuth 2.0"
datePublished: Tue Jan 07 2025 20:59:03 GMT+0000 (Coordinated Universal Time)
cuid: cm5mye45c000409lg57wo7qdj
slug: unlocking-oauth-20
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/0TORZQnU0aI/upload/da9fa4a2b727622facde23aa3c3d5f6e.jpeg
tags: github, oauth, nextjs, oauth2

---

OAuth can seem quite complicated and magical when you first encounter it, with the codes and tokens and whatever else is going on. Let me reassure you, it’s actually quite simple! Let’s take a look.

# Why was OAuth first created?

Back in ye olden days (when I was but a wee junior developer), we used to ask users to type a username and password into a form. We’d save that password (hashed, for security - we weren’t complete animals) in a database that belonged to the app we were working on and forgot about it. Passwords were typically only revokable by changing them, but hardly anyone did, meaning that most apps kept hold of their users’ credentials effectively forever. This has some fairly obvious security flaws - passwords are a pretty weak authentication method to start with, but if an attacker gets hold of the user’s password, they can easily cause all kinds of havoc and have full permission to do whatever they like. The longer an app has hold of a password, the more chance there is of a successful attack and those credentials being stolen.

Things clearly needed to change, so in 2010, a new way of delegating access to applications was devised: [OAuth 1.0](https://datatracker.ietf.org/doc/html/rfc5849) was born. This was very much a community effort, which was great, but meant that it didn’t *quite* meet the wider needs of everyone developing for the internet. The Internet Engineering Taskforce (IETF) took the OAuth 1.0 spec and revised it to create [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749), which came out two years later, in 2012. The changes were fairly drastic - even though OAuth 2.0 was inspired by OAuth 1.0, the two are definitely not backwards compatible. In this blog post, we’re only going to take a look at OAuth 2.0, as this is the most widely used OAuth mechanism today.

# How does OAuth 2.0 improve security?

Instead of asking a user to type their password and having that app store the password away for future use, OAuth 2.0 adds an extra layer for authorisation between the app and the end user. The app sends the user to an authorisation layer, which abstracts away all this logging in business that we would have had to handle ourselves in the past. Once the user has successfully logged in, the authorisation layer will return what’s called an “authorisation code”, which the app then exchanges for a token behind the scenes. This token is effectively a key, which the app is then able to use as proof that the user has granted it permission to do whatever it needs to do.

You can liken this process checking into a hotel - you go to the check-in desk (authorisation layer) and give them your your name and other check-in details (credentials) and they check their system to make sure you’ve booked (kind of like an authorisation code I guess? though the metaphor is falling apart a bit here) and then give you a hotel key (token). This key will *only* let you access certain areas of the hotel like your room, the gym and perhaps the dining room for your free breakfast, which represents the permissions that have been granted.

# OAuth 2.0 terminology

Before we look at how OAuth 2.0 works in practice, we should cover off some terminology. I find that the official terms in the spec don’t really match the way I tend to think about them, so it’s good to clear this up before we start really delving in.

The OAuth 2.0 spec mentions four roles:

1. **resource owner** - the official description of this is “an entity capable of granting access to a protected resource”. In most cases though, we will be thinking of this as our end user, who is wanting to use a particular feature and needs to grant the app access to it by way of entering a username and password, and probably some two factor authentication mechanism
    
2. **client** - I think this name is quite confusing, as this actually refers to the *application* making requests on behalf of the resource owner (aka user) with their permission. This can be any kind of application - website, mobile app, desktop app, whatever. OAuth makes a lot of use of “client ID” and “client secret” values and this is where knowing what this is comes in handy
    
3. **resource server** - this is the server hosting the “protected resources” aka the API that the client wants to use to show data to the resource owner. This server is capable of accepting and responding to resource requests using “access tokens” rather than passwords (more about these later)
    
4. **authorisation server** - this stitches everything together. It manages access to the resource server (aka API) it is protecting. The client has to send the user over to the authorisation server to log in, which means it never gets their password.
    

Let’s look at some real world examples of all of this stuff.

# Practical example: OAuth 2.0 in a Next.js app

Nothing solidifies these ideas more in my mind than a practical example - hopefully this will be helpful for you too. I’ve been working on trying to get Github login to work on a Next.js app for a side project and I thought this would be a great way to illustrate how OAuth 2.0 works.

## Registering your client

Before you can use OAuth 2.0 with your client application, you will need to register it with the authorisation server that you want to use. In Github’s case, they have the concept of “Github apps”, which you can set up by doing the following:

1. Log onto Github
    
2. Click on your profile icon in the top right-hand corner of the screen
    
3. Click on the *Settings* cog in the drop-down menu
    
4. Click on the very bottom item in the left-hand menu - *Developer Settings*
    
5. Click on the *New Github app* button
    
6. Fill in the details of your app - because I’m developing on my local machine using Next.js, I used `http://localhost:3000` as my homepage URL
    
7. By default, webhooks are enabled, but I just switched them off while trying this out
    
8. Hit the green *Create Github app* button and you’re done!
    

Now you have an authorisation server to use to get your tokens.

## Adding a login link

> **Note:** there are more “out of the box” ways of doing this, like [Next Auth](https://next-auth.js.org/), that are less fiddly and better if you’re using this in an actual project. However, these kinds of tools abstract a lot of the authentication process away to make things easier, so I’m using this more “manual” method just to show you what’s going on behind the scenes.

To kick off the authentication process, we’ll want to send our user to Github to log in. This is very simple to do and requires only a small amount of code:

```xml
<a href={`https://github.com/login/oauth/authorize?client_id=${process.env.GITHUB_CLIENT_ID}`}>Login with GitHub</a>
```

You’ll need to pop the above snippet on your page somewhere, and then add a new entry to your `.env` file for `GITHUB_CLIENT_ID`:

```javascript
GITHUB_CLIENT_ID=<insert your Github Client ID>
```

The client ID is there so Github knows which of the client applications it’s being asked to log in to. This is how you find it:

1. Log onto Github
    
2. Click on your profile icon in the top right-hand corner of the screen
    
3. Click on the *Settings* cog in the drop-down menu
    
4. Click on the very bottom item in the left-hand menu - *Developer Settings*
    
5. Click on the app you created in the “Registering your client” step
    
6. Under the *About* section, you’ll see an app ID and a client ID - you’ll want to copy the client ID into your `.env` file
    

Now that this is done, when you click on the login button, you should get taken directly to Github to log in, or if you’re already logged in, you’ll get sent straight back to your app.

If everything has gone to plan, you should get sent back to your callback URL (if you didn’t specify one, you’ll get sent to your app’s homepage) and you’ll notice a `?code` query parameter on the end of your URL.

This code is what we’re going to use to get our access token - our hotel key if you will.

## Getting the access token

Now that we have a code, we can take that code to the authorisation server and exchange it for an access token. For this step, we’ll need to add a callback URL - you can do this as follows:

1. Log onto Github
    
2. Click on your profile icon in the top right-hand corner of the screen
    
3. Click on the *Settings* cog in the drop-down menu
    
4. Click on the very bottom item in the left-hand menu - *Developer Settings*
    
5. Click on the app you created in the “Registering your client” step
    
6. Add the following to your callback URL field: `http://localhost:3000/api/auth/login/callback`
    

You can use a different route here if you like, just know that we’re going to add a route handler because we’ll need to take the `code` query parameter and use it to request an access token. This needs to be done on the server rather than the client side for security reasons.

In the case of my app, I’ve added a route handler under `src/app/api/auth/login/callback` with the following code:

```typescript
import { cookies } from 'next/headers'
import { type NextRequest, NextResponse } from 'next/server'

export async function GET(request: NextRequest) {
  const code = request.nextUrl.searchParams.get('code');
  const url = `https://github.com/login/oauth/access_token?client_id=${process.env.GITHUB_CLIENT_ID}&client_secret=${process.env.GITHUB_CLIENT_SECRET}&code=${code}`;

  try {
    const response = await fetch(url, {
      method: 'POST',
      headers: {
        "Accept": "application/json",
      },
    });
    if (!response.ok) {
      throw new Error(`Response status: ${response.status}`);
    }

    const json = await response.json();
    const cookieStore = await cookies();
    cookieStore.set('access_token', json.access_token);

    return new NextResponse(`Access token: ${json.access_token}`);
  } catch (error) {
    console.error((error as Error)?.message);
  }
}
```

Here we are getting the code from the query parameters, then compiling the URL to request the access token by combining the URL `https://github.com/login/oauth/access_token` with the query parameters that are required to get the token:

* **client ID** - the ID you grabbed from your Github app earlier
    
* **client secret** - the secret you grabbed from your Github app earlier
    
* **code** - this is the code we got from Github in the first step
    

Then we make a POST request to Github’s authorisation layer to get the access token and voila! In this very contrived example I am simply displaying the access token on the page, but obviously you would never do this in real life.

# Want to see the code?

I’ve got you covered! I’ve set up a [Github repository for this example](https://github.com/dana-ciocan/github-auth-example), so that you can see exactly how this all works in practice without having to type it all out by hand. You can even run it - there are instructions in the README.