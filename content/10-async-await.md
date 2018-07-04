---
title: "Async/await"
permalink: /the-modern-javascript-tutorial/async-await
excerpt: "..."
last_modified_at: 2018-07-04T15:58:49-04:00
---

## Async function

Async function is enabled by default in all browsers. 

Why Async function?

* Async function make your asynchronous code less.
* Async function make your asynchronous feel to synchronous code and more readable as it were asynchronous.

The syntax of `async function` is:

```javascript
async function name([param[, param[, ... param]]]) {
  statements
}
```

Async function always returns a promise. If the code has return `<non-promise>` in it, then JavaScript automatically wraps it into a resolved promise with that value.

For an example, the code below returns a resolved promise with the result of 1:

```javascript
async function f() {
  return "Hi async function!";
}

f().then(console); // Hi async function!
```

Then we could return a promise, that would be the same as:

```javascript
async function f() {
  return Promise.resolve("Hi async function!");
}

f().then(console); // Hi async function!
```

There's another `await operator` is used to wait for `a Promise`. It can only be used inside an async function.

## Await

The syntax of `await operator` is:

```javascript
let value = await promise;
```

The keyword await makes JavaScript wait until that promise settles and returns its result.

The await expression causes async function execution to pause until a Promise settles and returns its result.

If the value of the expression following the await operator is not a promise, it's converted to a resolved Promise.

Here's an example with a promise that resolves in 1 second:

```javascript
async function f() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done"), 1000);
  });

  let result = await promise; // Wait till the promise resolves (line: 6)

  alert(result);
}

f();
```

The function execution pauses at the line (6) and resumes when the promise settles, and returns its result. So the code above shows "done" in one second.

Let's take showOff() example from the chapter `promise chaining` and `promise is asynchronous`, rewrite it using async/await.
