---
title: "Awaiting a Promise"
permalink: /the-modern-javascript-tutorial/awaiting-a-promise
excerpt: "In order to use a promise, we must wait for it to be resolve/fulfilled or rejected..."
last_modified_at: 2018-06-27T15:58:49-04:00
---

In order to use a promise, we must wait for it to be resolve/fulfilled or rejected. The way to do this is using `promise.then` and `promise.catch`

If a promise is pending, `promise.then/catch` handlers wait for the result. Otherwise, if a promise has already settled, they execute immediately.

Some tasks may require time and sometimes finish immediately. The good thing is the `promise.then` handler is guaranteed to run in both cases.

The syntax of `.then` is:

```javascript
promise.then(
  function(result) { /* handle a successful result */ },
  function(error) { /* handle an error */ }
);
```

1. The first argument of `promise.then` is a function that runs when the Promise is resolved, and receives the result.
2. The second argument of .then is a function that runs when the Promise is rejected, and receives the error.

Here is an example of the resolving the promise with a successful job completion:

```javascript
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => resolve("done"), 1000);
});

// resolve runs the first function in .then
promise.then(
  result => alert(result), // shows "done" after 1 second
  error => alert(error) // doesn't run
);
```

And here is an example of the rejecting the promise with an error:

```javascript
let promise = new Promise(function(resolve, reject) {
  setTimeout(() => reject(new Error("error")), 1000);
});

// reject runs the second function in .then
promise.then(
  result => alert(result), // doesn't run
  error => alert(error) // shows "Error: error" after 1 second
);
```

If you want to execute only in successful completions, then you can provide only one function argument to `promise.then`:

```javascript
let promise = new Promise(resolve => {
  setTimeout(() => resolve("done"), 1000);
});

promise.then(alert); // shows "done!" after 1 second
```

If you want to execute only in errors, then you can use `null` as the first argument: `promise.then(null, errorHandlingFunction)`. Or you can use `promise.catch(errorHandlingFunction)`, which is exactly the same using:

```javascript
let promise = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("error")), 1000);
});

// promise.catch(f) is the same as promise.then(null, f)
promise.catch(alert); // shows "Error: error" after 1 second
```

Further Reading

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="_blank"} - The mozilla developer network has great documentation on promises.