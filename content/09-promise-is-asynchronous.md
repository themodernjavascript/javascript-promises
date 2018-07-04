---
title: "Promise is Asynchronous"
permalink: /the-modern-javascript-tutorial/promise-is-asynchronous
excerpt: "Promise is asynchronous..."
last_modified_at: 2018-07-02T15:58:49-04:00
---

> Promise is asynchronous. 

Let's log a message before and after we call the promise as below:

```javascript
// call our promise
var askMom = function () {
  console.log('before asking Mom'); // Log before
  willIGetNewPhone
    .then(showOff)
    .then(function (result) {
      console.log(result);
    })
    .catch(function (error) {
      console.log(error.message);
    });
  console.log('after asking mom'); // Log after
}
```

What is the sequence of expected output? You may expect:

1. before asking Mom
2. Hey friend, I have a new black Samsung phone.
3. after asking mom

However, the actual output sequence is:

1. before asking Mom
2. after asking mom
3. Hey friend, I have a new black Samsung phone.

Why? Because life (or JS) waits for no man.
You, the kid, wouldn't stop playing while waiting for your mom promise (the new phone). Don't you?

That's something we call asynchronous, the code will run without blocking or waiting for the result. Anything that need to wait for promise to proceed, you put that in `.then`.
