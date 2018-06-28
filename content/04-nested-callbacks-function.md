---
title: "Nested callbacks function"
permalink: /the-modern-javascript-tutorial/nested-callbacks-function
excerpt: "What if you want to load two scripts sequentially..."
last_modified_at: 2018-06-12T15:58:49-04:00
---

Here's a full example with a real script in previous chapters:

```javascript
function loadExternalScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(null, script);
  script.onerror = () => callback(new Error(`Script load error for ${src}`));

  document.head.append(script);
}

loadExternalScript('https://cdnjs.cloudflare.com/ajax/libs/react/16.4.0/cjs/react.production.min.js', function(error, script) {
  if (error) {
    console.log(error);
  } else {
    alert(`Awesome, the ${script.src} is loaded`);
  }
});
```

What if you want to load two scripts sequentially, the first one, and then the second one after it?

The solution would be to put the second `loadExternalScript` call inside the callback, like this:

```javascript
loadExternalScript('script.js', function(error, script) {
  if (error) {
    console.log(error);
  } else {
    alert(`Awesome, the ${script.src} is loaded, let's load one more`);
    
    loadExternalScript('script2.js', function(error, script) {
      if (error) {
        console.log(error);
      } else {
        alert(`Awesome, the second script is loaded`);
      }
    });
  }
});
```

After the outer `loadExternalScript` is complete, the callback initiates the inner one.

What if you want one more script?

```javascript
loadExternalScript('script.js', function(error, script) {
  if (error) {
    console.log(error);
  } else {
    loadExternalScript('script2.js', function(error, script) {
      if (error) {
        console.log(error);
      } else {
        loadExternalScript('script3.js', function(error, script) {
          if (error) {
            console.log(error);
          } else {
            // ...continue after all scripts are loaded
          }
        });
      }
    })
  }
});
```

So, every new action is inside a callback, that’s fine for few actions, but not good for many.
