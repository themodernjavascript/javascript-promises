---
title: "Callbacks function errors handling"
permalink: /the-modern-javascript-tutorial/callbacks-function-errors-handling
excerpt: ""
last_modified_at: 2018-06-12T15:58:49-04:00
---

In the previous chapter we didn't consider errors. What if the script loading fails?

Here's an improved version of `loadExternalScript` that tracks loading errors:

```javascript
function loadExternalScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`Script load error for ${src}`));

  document.head.append(script);
}
```

It calls `callback(null, script)` for successful load and `callback(error)` otherwise.

Here's the usage:

```javascript
loadExternalScript('script.js', function(error, script) {
  if (error) {
    // handle error
  } else {
    // script loaded successfully
  }
});
```

It's called the "error-first callback" style.

The convention is:

1. The first argument of `callback` is reserved for an error if it occurs. Then `callback(err)` is called.
2. The second argument (and the next ones if needed) are for the successful result. Then `callback(null, result1, result2...)` is called.

So the callback function is used both for reporting errors and passing back results.
