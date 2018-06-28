---
title: "Callbacks function"
permalink: /the-modern-javascript-tutorial/callbacks-function
excerpt: "A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine/action..."
last_modified_at: 2018-06-08T15:58:49-04:00
---

> A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine/action.

As an example in real world, let's say, you call your friend and ask him for some information, say, a mutual friend's mailing address that you have lost. Your friend doesn't have this information memorized, so he has to find his address book and look up the address. This might take him a few minutes. There are different strategies for how you can proceed:

* ([Asynchronous](/the-modern-javascript-tutorial/synchronous-and-asynchronous)) You tell your friend to call you back once he has the information. Meanwhile, you can focus all of your attention on the other tasks you need to get done, like folding laundry and washing the dishes.

* ([Synchronous](/the-modern-javascript-tutorial/synchronous-and-asynchronous)) You stay on the phone with him and wait while he is looking.

But many actions in JavaScript are asynchronous.

As an example, take a look at the function `loadExternalScript`:

```javascript
function loadExternalScript(src) {
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}
```

The purpose of the function is to load a new script. When it adds the `<script src="...">` to the document, the browser loads and executes it.

You can call the function something like this:

```javascript
loadExternalScript('external-script.js'); // loads and executes the script
```

The function is called as "asynchronously", because the script loading does not finishes now, but later.

The scripts being load, then the execution continues. While the script is loading, the code below may finish executing, and if the loading takes more time, other scripts may run meanwhile too.

```javascript
loadExternalScript('external-script.js');
// the code below loadExternalScript doesn't wait for the script loading to finish
// other scripts
```

Let's say you want to use the new script after the external script is loaded. It probably declares new functions after `loadExternalScript`.

But if you do that immediately after the `loadExternalScript` call, that wouldn't work:

```javascript
loadExternalScript('external-script.js'); // the script has "function newFunction() {...}"
newFunction(); // no such function
```

Naturally, the browser probably didn't have time to load the script. So the immediate call to the new function fails. For now `loadExternalScript` function doesn't provide a way to track the load completion. The script loads and eventually runs, that's all. But we'd like to know when it happens, to use new functions and variables from that script.

Let's add a callback function as a second argument to `loadExternalScript` that should execute when the script loads:

```javascript
function loadExternalScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;

  script.onload = () => callback(script);

  document.head.append(script);
}
```

Now if you want to call new functions from the script, you should write that in the callback:

```javascript
loadExternalScript('script.js', function() {
  newFunction(); // the callback runs after the script is loaded
  ...
});
```

Here's a full example with a real script:

```javascript
function loadScript(src, callback) {
  let script = document.createElement('script');
  script.src = src;
  script.onload = () => callback(script);
  document.head.append(script);
}

loadScript('https://cdnjs.cloudflare.com/ajax/libs/react/16.4.0/cjs/react.production.min.js', script => {
  alert(`Awesome, the ${script.src} is loaded`);
});
```

That's called a "callback-based" style of asynchronous programming. 

> A function that does something asynchronously should provide a callback argument where we put the function to run after it's complete.
