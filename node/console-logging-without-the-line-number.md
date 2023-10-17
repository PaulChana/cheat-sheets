# Disable line number in console.log

```javascript
console.print = function (...args) {
    queueMicrotask (console.log.bind (console, ...args));
}
```

#node #javascript