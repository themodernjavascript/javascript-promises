---
title: "Promise Chaining"
permalink: /the-modern-javascript-tutorial/promise-chaining
excerpt: "..."
last_modified_at: 2018-07-02T15:58:49-04:00
---

Promises are chainable.

Let's say, you are the kid, and you promise your friend that you will show them the new phone when your mom buy you one.

That's another promise. Let's get started!

```javascript
// 2nd promise
var showOff = function(phone) {
  return new Promise(
    function(resolve, reject) {
      var message = 'Hey friend, I have a new ' +
          phone.color + ' ' + phone.brand + ' phone';

      setTimeout(() => resolve(message), 1000); // fulfilled
    }
  );
};
```

Noted: In this example, you might realize that we didn't call the reject. It's optional. 

And we can shorten this sample like using `Promise.resolve` instead as below:

```javascript
// 2nd promise
var showOff = function (phone) {
  var message = 'Hey friend, I have a new ' +
      phone.color + ' ' + phone.brand + ' phone';

  return Promise.resolve(message);
};
```

Let's chain the promises. You are the kid can only start the `showOff` promise after the `willIGetNewPhone` promise.

```javascript
// call our promise
var askMom = function() {
  willIGetNewPhone
    .then(showOff) // chain goes here
    .then(function(result) {
      console.log(fulfilled); // output: 'Hey friend, I have a new black Samsung phone.'
    })
    .catch(function(error) {
      // oops, mom don't buy it
      console.log(error.message); // output: 'mom is not happy'
    });
};
```
