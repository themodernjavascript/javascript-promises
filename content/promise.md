# Promise

Imagine that you're a top singer, and fans ask for your next upcoming single day and night.

To get a relief, you promise to send it to them when it's published. You give your fans a list. They can fill in their coordinates, so that when the song becomes available, all subscribed parties instantly get it. And if something goes very wrong, so that the song won't be published ever, then they are also to be notified.

Everyone is happy: you, because the people don't crowd you any more, and fans, because they won't miss the single.

That was a real-life analogy for things we often have in programming:

1. A "producing code" that does something and needs time. For instance, it loads a remote script. That's a "singer".
2. A "consuming code" wants the result when it's ready. Many functions may need that result. These are "fans".
3. A promise is a special JavaScript object that links them together. That's a "list". The producing code creates it and gives to everyone, so that they can subscribe for the result.

The analogy isn't very accurate, because JavaScript promises are more complex than a simple list: they have additional features and limitations. But still they are alike.

The constructor syntax for a promise object is:

```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```

The function passed to `new Promise` is called executor. When the promise is created, it’s called automatically. It contains the producing code, that should eventually finish with a result. In terms of the analogy above, the executor is a "singer".

The resulting promise object has internal properties:

* `state` – initially is "pending", then changes to "fulfilled" or "rejected",
* `result` – an arbitrary value, initially `undefined`.

When the executor finishes the job, it should call one of:

* `resolve(value)` – to indicate that the job finished successfully:
  * sets `state` to "fulfilled",
  * sets `result` to `value`.
* `reject(error)` – to indicate that an error occurred:
  * sets `state` to `"rejected"`,
  * sets `result` to `error`.

![promise resolve reject](/assets/images/promise-resolve-reject.png)
