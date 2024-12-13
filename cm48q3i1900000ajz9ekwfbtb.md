---
title: "Exploring new JavaScript array methods"
datePublished: Tue Dec 03 2024 17:18:22 GMT+0000 (Coordinated Universal Time)
cuid: cm48q3i1900000ajz9ekwfbtb
slug: exploring-new-javascript-array-methods
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/BqJAbXk2Fuw/upload/deab2e9bdb33ce8e2055c6f2f9e4781b.jpeg
tags: javascript, arrays, array-methods

---

I stumbled upon some really useful new(ish) array methods in the JavaScript spec that I hadn’t encountered before. Some of them seem pretty nifty, so I thought I’d write a little blog post to share them with you. Let’s go oldest to newest and chat through these.

# Array.prototype.findLast()

> Available in all latest browsers since August 2022

This array method will find the value of the last element in the array that satisfies a given condition. It does this by iterating through the array in reverse order. If none of the elements in the array satisfy the condition, it will return `undefined`.

You can think of this as the opposite to `find()`, which will find the value of the *first* element in the array that satisfies the given condition.

As an example, imagine you have an array of dogs:

```javascript
const dogs = ['chihuahua', 'retriever 1', 'husky', 'samoyed', 'retriever 2'];
```

You need to grab (or retrieve, if you will!) the very last retriever in the array because they need a bath, so you call:

```javascript
dogs.findLast(breed => breed.includes('retriever'));
// returns 'retriever 2'
```

So why is it useful? Hopefully you can already see why this would be handy, in spite of my very contrived example. Sometimes you need to get the last element rather than the first element that meets a certain condition and having to write custom code to handle this every time feels cumbersome. Instead, there is a built-in method ready to go that you can reach for. Also, using this method should be more performant in this case.

For more details, see [the MDN article on `findLast`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast).

# Array.prototype.findLastIndex()

> Available in all latest browsers since August 2022

This array method will find the *index* of the last element in the array that satisfies a given condition. It does this by iterating through the array in reverse order. If none of the elements in the array satisfy the condition, it will return `-1`.

You can think of this as the opposite to `findIndex()`, which will find the index of the *first* element in the array that satisfies the given condition.

Back to our example, above, if we change `findLast()` to `findLastIndex()`, we’ll get the index of “retriever 2” rather than its value:

```javascript
const dogs = ['chihuahua', 'retriever 1', 'husky', 'samoyed', 'retriever 2'];

dogs.findLastIndex(breed => breed.includes('retriever'));
// returns 4
```

So why is it useful? If you need to find the index of the last element in an array that meets a given condition, this one will be useful - previously you probably would have had to reverse the array and then use `findIndex()` and now you won’t have to! Also, using this method should be more performant in this case.

For more details, see [the MDN article on `findLastIndex`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex).

# Array.prototype.toSorted()

> Available in all latest browsers since July 2023

This is the sibling function to `sort()`. The difference between the two is:

* **sort** - sorts the array in place - the original array is forever altered
    
* **toSorted** - makes a copy of the array and sorts it - the original array stays unaltered
    

This can be useful if you do not want to alter the original ordering of the array you’re trying to sort.

```javascript
const dogs = ['chihuahua', 'retriever 1', 'husky', 'samoyed', 'retriever 2'];

const sortedDogs = dogs.toSorted();

console.log(sortedDogs);
// ['chihuahua', 'husky', 'retriever 1', 'retriever 2', 'samoyed']

console.log(dogs);
// ['chihuahua', 'retriever 1', 'husky', 'samoyed', 'retriever 2']
```

For more details, see [the MDN article on `toSorted`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toSorted).

# Array.prototype.toReversed()

> Available in all latest browsers since July 2023

This is the sibling function to `reverse()`. The difference between the two is:

* **reverse** - reverses the array in place - the original array is forever altered
    
* **toReversed** - makes a copy of the array and reverses its ordering - the original array stays unaltered
    

This can be useful if you do not want to alter the original ordering of the array you’re trying to reverse.

```javascript
const dogs = ['chihuahua', 'retriever 1', 'husky', 'samoyed', 'retriever 2'];

const reversedDogs = dogs.toReversed();

console.log(reversedDogs);
// ['samoyed', 'retriever 2', 'retriever 1', 'husky', 'chihuahua']

console.log(dogs);
// ['chihuahua', 'retriever 1', 'husky', 'samoyed', 'retriever 2']
```

For more details, see [the MDN article on `toReversed`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toReversed).

# Array.prototype.toSpliced()

> Available in all latest browsers since July 2023

This is the sibling function to `splice()`. The difference between the two is:

* **splice** - removes, replaces or adds new elements to an array in place - the original array is forever altered
    
* **toSpliced** - makes a copy of the array and removes, replaces or adds new elements to it - the original array stays unaltered
    

This can be useful if you do not want to alter the original ordering of the array you’re trying to splice.

This is probably my most favourite of these methods - I *still* forget that `splice()` alters the original array when I use it, so having this to reach for instead will be handy and will hopefully help me remember…

For more details, see [the MDN article on `toSpliced`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toSpliced).

# Array.prototype.with()

> Available in all latest browsers since July 2023

As with a lot of these methods, this is a “copy” version of something else. Can you guess of what though? Because I certainly couldn’t… It turns out that:

```javascript
dogs.with(0, 'rottweiler');
```

Is the sibling function of:

```javascript
dogs[0] = 'rottweiler';
```

Would you have guessed that? Because I did not!

As with the previous examples, `with()` will create a copy of the `dogs` array rather than replacing the element in the *original* array, which can be handy in certain situations.

For more details, see [the MDN article on `with`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/with).

# Array.fromAsync()

> Available in all latest browsers since January 2024

This method also (kind of) has a sibling - `Array.from()`. You can use `Array.from()` to create an array from something that isn’t quite an array but something like it, like a string, map or set. I have frequently used it to convert a `NodeList` returned by a query selector to an array for example.

The `Array.fromAsync()` method is a little different in that it was specifically created to deal with asynchronous objects like, say, promises. You may think “this sounds similar to `Promise.all()` and you’d be right, but there are a few key differences:

* **Array.fromAsync():** will wait for each object to yield sequentially and will wait for one value to be retrieved before getting the next one
    
* **Promise.all():** will wait for each object to yield concurrently and will retrieve all values in advance and will await them all
    

I am not exactly clear about the use cases for `Array.fromAsync()` yet as I haven’t used it out in the wild and could not find much about it in my research. If you’ve used it, please let me know what you used it for and what you think!

For more details, see [the MDN article on `fromAsync`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/fromAsync).