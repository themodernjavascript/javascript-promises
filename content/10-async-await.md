---
title: "Async/await"
permalink: /the-modern-javascript-tutorial/async-await
excerpt: "Async function is enabled by default in all browsers..."
last_modified_at: 2018-07-04T15:58:49-04:00
---

## Async function

Async function is enabled by default in all browsers. 

Why Async function?

* Make your asynchronous code less.
* Make your asynchronous feel to synchronous code and more readable as it were asynchronous.

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

## Error handling

If a promise resolves normally, then await promise returns the result. But in case of a rejection it throws the error:

```javascript
async function f() {
  await Promise.reject(new Error("Error"));
}
```

```javascript
async function f() {
  throw new Error("Error");
}
```

The promise may take some time before it rejects then throw an error. We can catch that error using `try...catch`:

```javascript
async function f() {
  try {
    let response = await fetch('/no-product');
    let product = await response.json();
  } catch(err) {
    alert(err); // Failed to fetch
  }
}

f();
```

If we don't use `try...catch`, we can append `.catch` to handle it:

```javascript
async function f() {
  let response = await fetch('/no-product');
}

// f() becomes a rejected promise
f().catch(alert); // Failed to fetch
``` 

If we forget to add `.catch` there, then we get an unhandled promise error (and can see it in the console).

Let's take the example from the chapter `promise chaining` & `promise is asynchronous` and rewrite it using async/await.

```javascript
let isMomHappy = true;

let willIGetNewPhone = new Promise(function (resolve, reject) {
  if (isMomHappy) {
    let phone = {
      brand: 'Samsung',
      color: 'black'
    };
    
    setTimeout(() => resolve(phone), 1000); // fulfilled
  } else {
    let reason = new Error('mom is not happy');
    setTimeout(() => reject(reason), 1000); // reject
  }
});

let showOff = function(phone) {
  let message = 'Hey friend, I have a new ' +
      phone.color + ' ' + phone.brand + ' phone';

  return Promise.resolve(message);
};

async function askMom() {
  let answer = await willIGetNewPhone;
  console.log(answer);
  let show = showOff(answer);
  console.log(show);
}

askMom();
```
