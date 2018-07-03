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

As an example in real life "Imagine that you are a kid. Your mom promises you that she will get you a new phone in next week."

### States

You don't know if you will get that phone until next week. Your mom can either really buy you a brand new phone, or stand you up and withhold the phone if she is not happy :(.

A promise state can be in one of the 3 states below:

* `pending` - The initial state of a promise (You don't know if you will get that phone until next week).
* `resolved` - The state of a promise representing a successful operation (Your mom really buy you a brand new phone).
* `rejected` - The state of a promise representing a failed operation (You don't get a new phone because your mom is not happy).

### Results

A promise result can be in one of the 3 result below:

* `undefined` - The initial result of a promise.
* `value` or `error` - An arbitrary value of your choosing.

### Process Schema

![Promise Resolve Reject](/assets/images/promise-resolve-reject.jpg)

## Example

Here is an example of the `factory function` resolving the promise with a successful job completion or rejecting the promise with an error:

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
```

* We use `new Promise` to construct the promise.
* We give the constructor a `factory function` which does the actual work.
* This `factory function` is called immediately with two arguments: `resolve` and `reject`

The code is expressive in itself:

* We have a boolean `isMomHappy`, to define if mom is happy.
* We have a promise `willIGetNewPhone`. The promise can be either resolved (if mom get you a new phone) or rejected(mom is not happy, she doesn't buy you one).

## Summary

The `factory function` should do a job (something that takes time usually) and then call resolve or reject to change the state of the corresponding Promise object.

Further Reading

* [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise){:target="_blank"} - The mozilla developer network has great documentation on promises.
