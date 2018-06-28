---
title: "Promise"
permalink: /the-modern-javascript-tutorial/promise
excerpt: "The core idea of a promises is that promise represents the result of an asynchronous operation..."
last_modified_at: 2018-06-24T15:58:49-04:00
---

## What is Promise?

> The core idea of a promises is that promise represents the result of an asynchronous operation. 

## Constructor Syntax

```javascript
let promise = new Promise(function(resolve, reject) {
  // executor
});
```

The function passed to `new Promise` is called the executor. When the promise is created, this executor function runs automatically. That should eventually produce a result.

The resulting promise object has 2 internal properties are `state` and `result`.

### States

A promise state can be in one of the 3 states below:

* `Pending` - The initial state of a promise.
* `Fulfilled` - The state of a promise representing a successful operation.
* `Rejected` - The state of a promise representing a failed operation.

### Results

A promise result can be in one of the 3 result below:

* `undefined` - The initial result of a promise.
* `value` or `error` - An arbitrary value of your choosing.

### Process Schema

![Promise Resolve Reject](/assets/images/promise-resolve-reject.jpg)

## Example

Here is an example of the `factory function` resolving the promise with a successful job completion.

```javascript
let promise = new Promise(function(resolve, reject) {
  // function is executed automatically when the promise is constructed

  // after 1 second, the job is done with the result "done"
  setTimeout(() => resolve("done"), 1000);
});
```

* We use `new Promise` to construct the promise.
* We give the constructor a `factory function` which does the actual work.
* This `factory function` is called immediately with two arguments: `resolve` and `reject`

After one second of processing the `factory function` calls resolve("done") to produce the result:

![Promise Resolve Done](/assets/images/promise-resolve.png)

And here is an example of the `factory function` rejecting the promise with an error:

```javascript
let promise = new Promise(function(resolve, reject) {
  // after 1 second, the job is finished with an error
  setTimeout(() => reject(new Error("error")), 1000);
});
```

![Promise Resolve Done](/assets/images/promise-reject.png)

## Summary

The `factory function` should do a job (something that takes time usually) and then call resolve or reject to change the state of the corresponding Promise object.

Further Reading

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="_blank"} - The mozilla developer network has great documentation on promises.