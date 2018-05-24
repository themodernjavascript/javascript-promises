# Callbacks

Many actions in JavaScript are asynchronous.

For instance, take a look at the function `loadScript(src)`:

```javascript
function loadScript(src) {
  let script = document.createElement('script');
  script.src = src;
  document.head.append(script);
}
```