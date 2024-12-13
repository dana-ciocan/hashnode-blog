---
title: "Closures in JavaScript"
datePublished: Sat Sep 14 2024 15:38:29 GMT+0000 (Coordinated Universal Time)
cuid: cm12bawgv000i08l8b4hk1lto
slug: closures-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/PB80D_B4g7c/upload/96897f314368a486cd6ddf3c41554efb.jpeg
tags: javascript, coding, closures-in-javascript

---

JavaScript has some pretty interesting advanced concepts that take a while to get your head around when you first encounter them. One of these concepts is closures and my hope is to explain this one in simple terms from the ground up, so you can understand closures and know when or if they are appropriate to use.

> Given that TypeScript is eventually compiled down to JavaScript, these concepts still apply in that world too, so it's worth knowing about them even if you don't technically use JavaScript directly in your work.

Let's delve into closures!

## Why have I never heard of closures before?

> Obviously you can skip this bit if you have!

Don't worry if you've been coding for a while and have never heard this term before, or have heard it mentioned but don't know what on earth it is. Closures are hard to grasp because although we actually use them all the time in JavaScript, we're not necessarily aware of it. It's not like you ever define a closure explicitly in your code, so how are you meant to know about its existence?

So you can rest assured that you haven't missed something that you were "supposed" to know - this is quite an advanced JavaScript topic. That being said, let's dive in and figure it out together!

## So what the heck is a closure?

I have been struggling with how to explain this for the entire time I've been writing this post, honestly. It's really hard to explain what closures are without also explaining why they're useful and the best way to do that is with examples. The best article I've found on closures is the [w3schools](https://www.w3schools.com/js/js_function_closures.asp) one, which builds up context and knowledge gradually. I'm going to steal their idea but explain it in my own unique style - let me know what you think!

Okay, so let's start with a basic idea. You've built a virtual pet shop website and you want to count how many times a user has fussed a virtual animal so that you can make them look happier the more love they get. You're starting with just one dog, so you can keep track of the number of times the dog's been fussed using one variable:

```javascript
var numFusses = 0;
function fussDog() {
  numFusses = numFusses + 1;
}
fussDog(); // The dog has now had 1 fuss - numFusses = 1
fussDog(); // The dog has now had 2 fusses - numFusses = 2
```

Now let's say you want to add a cat into the mix. Suddenly, using just one global variable no longer works:

```javascript
var numFusses = 0;
function fussDog() {
  numFusses = numFusses + 1;
}
function fussCat() {
  numFusses = numFusses + 1;
}
fussDog(); // The dog has now had 1 fuss - numFusses = 1
fussCat(); // The cat has now had 1 fuss - numFusses = 2 :(
```

Now `numFusses` just represents the **total** number of fusses rather than the amount of love each animal has had individually.

How could you solve this issue? You could try putting the variable `numFusses` inside the function and return it once you've finished incrementing:

```javascript
function fussDog() {
  var numFusses = 0;
  numFusses = numFusses + 1;
  return numFusses;
}
function fussCat() {
  var numFusses = 0;
  numFusses = numFusses + 1;
  return numFusses;
}
fussDog(); // The dog has now had 1 fuss - returns 1
fussCat(); // The cat has now had 1 fuss - returns 1
fussDog(); // The dog has now had 2 fusses - returns 1???
```

That's not quite right - you'll notice that no matter how many times you call `fussDog()` or `fussCat()` we'll get back `1` - this is because every time the function is called, the `numFusses` variable is reset to zero.

Let's try something else - how about a nested function?

```javascript
function fussDog() {
  let numFusses = 0;
  function fuss() {
    numFusses+= 1;
  }
  fuss(); // increments numFusses to 1
  fuss(); // increments numFusses to 2
  return numFusses; // returns 2
}
```

We know that the state is maintained inside a function, so `numFusses` would not get reset. The only annoying thing is that there's no way to call the internal `fuss()` function from anywhere but inside `fussDog()` which makes things super awkward for us as we can't call it when the user clicks on something for example.

This is exactly where closures come to the rescue! Let's set one up:

```javascript
const fussAnimal = function () {
  let numFusses = 0;
  return function () {
    numFusses += 1;
    return numFusses;
  }
};

const fussDog = fussAnimal();
const fussCat = fussAnimal();

fussDog(); // returns 1
fussCat(); // returns 1
fussDog(); // returns 2!!
```

Inside `fussAnimal`, which is a generic version of our fussing function, we set `numFusses` to zero. Then we return a function that manipulates that `numFusses` variable.

Now we create new variables called `fussDog` and `fussCat` that just store the functions `fussAnimal` returns to us so we can easily tell which one is which. Thanks to closures, each one will have its own private version of `numFusses` that they're able to keep track of separately! Hooray, the day is saved!

Obviously this is quite a contrived example, but hopefully it's a memorable one and will help you remember how closures work.

## Why do closures exist in JavaScript?

Closures exist because of the type of language JavaScript is - that is, a functional language that treats functions as "first-class citizens". What does that mean, you might wonder? Well, it means that you can do the following with functions:

* Pass them as arguments
    
* Return them from other functions
    
* Assign them to variables
    

Now, if the first language you ever learned was JavaScript, you may well take this for granted and I don't blame you! Plus it turns out a lot of modern languages are set up this way - Python, Rust, Kotlin, Swift, PHP, I could go on... So it's likely you've been working with languages like this your entire career!

What you've learn about closures here will apply to all those other languages too so it's a really transferable skill

## Why use closures today?

ES6, the new version of JavaScript that came out in 2015, has largely made closures obsolete. We can now instantiate classes with private variables instead of having to use closures to do the same thing in a more complicated way. So why would you ever need to use them?

I'm going to be honest here and say that the majority of the time, you can use a different kind of syntax that is easier to read by other developers so you probably want to avoid closures if you can help it. You might encounter them in legacy code though and there are still some people out there who like to use them. Though if I see a pull request with a closure in it, I tend to encourage the author to rewrite it personally! There are better ways nowadays.

Saying that, the topic of closures often comes up in the good old technical interview, so it's worth knowing how to explain them just in case you get asked about it while looking for your next role.

> I hope this blog post has helped you understand closures - if you have any questions, do comment and I'll do my best to answer them