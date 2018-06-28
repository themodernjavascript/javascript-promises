---
title: "Synchronous and Asynchronous"
permalink: /the-modern-javascript-tutorial/synchronous-and-asynchronous
excerpt: "In JavaScript we often need to deal with asynchronous behavior..."
last_modified_at: 2018-06-08T15:58:49-04:00
---

In JavaScript we often need to deal with asynchronous behavior, which can be confusing for programmers who only have experience with synchronous code. I will explain what asynchronous code is, some of the difficulties of using asynchronous code, and ways of handling these difficulties.

## Synchronous

> In synchronous, if you have two lines of code (L1 followed by L2), then L2 cannot begin running until L1 has finished executing.

You can imagine this as if you are in a line of people waiting to buy train tickets. You can't begin to buy a train ticket until all the people in front of you have finished buying theirs. Similarly, the people behind you can't start buying their tickets until you have bought yours.

## Asynchronous

> In asynchronous, you can have two lines of code (L1 followed by L2), where L1 schedules some task to be run in the future, but L2 runs before that task completes.

You can imagine this as if you are eating at a sit-down restaurant. Other people order their food. You can also order your food. You don't have to wait for them to receive their food and finish eating before you order. Similarly, other people don't have to wait for you to get your food and finish eating before they can order. Everybody will get their food as soon as it is finished cooking.

The sequence in which people receive their food is often correlated with the sequence in which they ordered food, but these sequences do not always have to be identical. For example, if you order a steak, and then I order a glass of water, I will likely receive my order first, since it typically doesn't take as much time to serve a glass of water as it does to prepare and serve a steak.

Note that asynchronous does not mean the same thing as concurrent or multi-threaded. JavaScript can have asynchronous code, but it is generally single-threaded. This is like a restaurant with a single worker who does all of the waiting and cooking. But if this worker works quickly enough and can switch between tasks efficiently enough, then the restaurant seemingly has multiple workers.

## Examples

The `setTimeout` function is probably the simplest way to asynchronously schedule code to run in the future:

```javascript
// Say "Hello."
console.log("Hello.");
// Say "Goodbye" two seconds from now.
setTimeout(function() {
  console.log("Goodbye!");
}, 2000);
// Say "Hello again!"
console.log("Hello again!");
```

If you are only familiar with synchronous code, you might expect the code above to behave in the following way:

* Say "Hello".
* Do nothing for two seconds.
* Say "Goodbye!"
* Say "Hello again!"

But setTimeout does not pause the execution of the code. It only schedules something to happen in the future, and then immediately continues to the next line.

* Say "Hello."
* Say "Hello again!"
* Do nothing for two seconds.
* Say "Goodbye!"
