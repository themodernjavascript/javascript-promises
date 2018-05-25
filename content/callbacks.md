## Introduction Callbacks

Many actions in JavaScript are asynchronous.

For instance, take a look at the function `loadScript(src)`:

```javascript
function loadScript(src) {
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}
```

The purpose of the function is to load a new script. When it adds the `<script src="...">` to the document, the browser loads and executes it.

We can use it like this:

```javascript
loadScript('my-script.js'); // loads and executes the script
```

The function is called "asynchronously", because the action (script loading) finishes not now, but later.

The call initiates the script loading, then the execution continues. While the script is loading, the code below may finish executing, and if the loading takes time, other scripts may run meanwhile too.

```javascript
loadScript('my-script.js');

// the code below loadScript doesn't wait for the script loading to finish
// ... code goes here
```

Now let's say we want to use the new script when it loads. It probably declares new functions, so we'd like to run them.

But if we do that immediately after the `loadScript(...)` call, that wouldn’t work:

```javascript
loadScript('my-script.js'); // the script has "function newFunction() {…}"

newFunction(); // no such function!
```

Naturally, the browser probably didn’t have time to load the script. So the immediate call to the new function fails. As of now, `loadScript` function doesn’t provide a way to track the load completion. The script loads and eventually runs, that’s all. But we’d like to know when it happens, to use new functions and variables from that script.

Let's add a `callback` function as a second argument to `loadScript` that should execute when the script loads:

```javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(script);

  document.head.append(script);
}
```

Now if we want to call new functions from the script, we should write that in the callback:

```javascript
loadScript('my-script.js', function() {
  // the callback runs after the script is loaded
  newFunction(); // so now it works
  ...
});
```

That`s the idea: the second argument is a function (usually anonymous) that runs when the action is completed.

Here`s a runnable example with a real script:

```javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;
  script.onload = () => callback(script);
  document.head.append(script);
}

loadScript('https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js', script => {
  alert(`Cool, the ${script.src} is loaded`);
  alert( _ ); // function declared in the loaded script
});
```

That's called a "callback-based" style of asynchronous programming. A function that does something asynchronously should provide a callback argument where we put the function to run after it’s complete.

Here we did it in `loadScript`, but it's a general approach.

# Callback in callback

How to load two scripts sequentially, the first one, and then the second one after it?

The natural solution would be to put the second `loadScript` call inside the callback, like this:

```javascript
loadScript('my-script.js', function(script) {
  alert(`Cool, the ${script.src} is loaded, let's load one more`);

  loadScript('my-script2.js', function(script) {
    alert(`Cool, the second script is loaded`);
  });
});
```

After the outer `loadScript` is complete, the callback initiates the inner one.

What if we want one more script...?

```javascript
loadScript('/my/script.js', function(script) {
  loadScript('/my/script2.js', function(script) {
    loadScript('/my/script3.js', function(script) {
      // ...continue after all scripts are loaded
    });
  })
});
```

So, every new action is inside a callback. That's fine for few actions, but not good for many, so we'll see other variants soon.
