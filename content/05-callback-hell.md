---
title: "Callback Hell"
permalink: /the-modern-javascript-tutorial/callback-hell
excerpt: "As calls become more nested, the code becomes deeper and increasingly more difficult to manage, that's called Callback Hell..."
last_modified_at: 2018-06-13T15:58:49-04:00
---

For one or maybe two nested calls it looks fine. But for multiple asynchronous actions that follow one after another we'll have code like this:

```javascript
loadExternalScript('script1.js', function(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadExternalScript('script2.js', function(error, script) {
      if (error) {
        handleError(error);
      } else {
        // ...
        loadExternalScript('script3.js', function(error, script) {
          if (error) {
            handleError(error);
          } else {
            // ...continue after all scripts are loaded (*)
          }
        });

      }
    })
  }
});
```

In the code above:

1. We load `script1.js`, then if there’s no error.
2. We load `script2.js`, then if there’s no error.
3. We load `script3.js`, then if there’s no error – do something else `(*)`.

As calls become more nested, the code becomes deeper and increasingly more difficult to manage, that's called "Callback Hell".

We may be able to solve the problem by making every action as a standalone function:

```javascript
loadExternalScript('script1.js', step1);

function step1(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadExternalScript('script2.js', step2);
  }
}

function step2(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...
    loadExternalScript('script3.js', step3);
  }
}

function step3(error, script) {
  if (error) {
    handleError(error);
  } else {
    // ...continue after all scripts are loaded (*)
  }
};
```

Well, there's no deep nesting now, because we made every action a separate top-level function.

It works, but the code looks like a apart spreadsheet. It's difficult to read, we'd like to have a something better.

Luckily, there are other ways to avoid such "Callback Hell". One of the best ways is to use "promises",
