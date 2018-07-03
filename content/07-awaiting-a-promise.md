---
title: "Awaiting a Promise"
permalink: /the-modern-javascript-tutorial/awaiting-a-promise
excerpt: "In order to use a promise, we must wait for it to be resolve/fulfilled or rejected..."
last_modified_at: 2018-06-27T15:58:49-04:00
---

In order to use a promise, we must wait for it to be resolve or rejected. The way to do this is using `promise.then` and `promise.catch`

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

Here is an example of either resolving the promise with a successful job completion or rejecting the promise with an error:

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

// call our promise
var askMom = function () {
  willIGetNewPhone.then(function (result) {
    // Yeah, you got a new phone
    console.log(result); // output: { brand: 'Samsung', color: 'black' }
  }).catch(function (error) {
    // Oops, mom don't buy it
    console.log(error.message); // output: 'mom is not happy'
  });
};

askMom();
```

* We have a function call `askMom`. In this function, we will execute our promise `willIGetNewPhone`.
We want to take some action once the promise is resolved or rejected, we use `.then` and `.catch` to handle our action.
* We have function(result) { ... } in `.then`. What is the value of result? The result value is exactly the value you pass in your promise resolve(your_success_value). Therefore, it will be phone in our case.
* We have function(error){ ... } in `.catch`. What is the value of error? As you can guess, the error value is exactly the value you pass in your promise reject(your_fail_value). Therefore, it will be reason in our case.

Further Reading

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="_blank"} - The mozilla developer network has great documentation on promises.
