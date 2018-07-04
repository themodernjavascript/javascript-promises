---
title: "Promise Chaining"
permalink: /the-modern-javascript-tutorial/promise-chaining
excerpt: "Promise is chainable..."
last_modified_at: 2018-07-02T15:58:49-04:00
---

> Promise is chainable.

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
    .then(showOff) // Chain goes here
    .then(function(result) {
      console.log(fulfilled); // Output: 'Hey friend, I have a new black Samsung phone.'
    })
    .catch(function(error) {
      // Oops, mom don't buy it
      console.log(error.message); // Output: 'mom is not happy'
    });
};
```

So far so good, let's return to the problem mentioned in the preview chapter: [callbacks](/content/05-callback-hell.md).

For an example, loading scripts. let’s use this feature with loadExternalScript to load scripts one by one, in sequence:

```javascript
loadExternalScript("script.js")
  .then(function(script) {
    return loadExternalScript("script2.js");
  })
  .then(function(script) {
    return loadExternalScript("script3.js");
  })
  .then(function(script) {
    // Use functions declared in scripts
    // to show that they indeed loaded
    one();
    two();
    three();
  });
```

Here each `loadExternalScript` call returns a promise, and the next `.then` runs when it resolves. Then it initiates the loading of the next script. So scripts are loaded one after another.

We can add more asynchronous actions to the chain. Please note that code is still "flat", it grows down, not to the right. There are no signs of "Callback Hell".
