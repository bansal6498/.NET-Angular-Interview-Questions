## var vs let
| Feature | var | let |
|---------|---------|------------|
| **Scope**| Function Scoped | Block Scoped |
| **Hoisting**| Variables are hoisted and initialized to undefined.| Variables are hoisted but not initialized |
| **Re-Declaration**| Can be redeclared within the same scope | Can't be redeclared |
| **Temporal Dead Zone**| Doesn't have a Temporal Dead Zone| Has a temporal Dead Zone |
## Event Loop
-   JS is single-threaded but uses **event loop** to handle async tasks.
-   Queue (callbacks, promises) → Event Loop → Call Stack.
-   Ensures non-blocking execution.
## == vs ===
-   == → Loose equality (performs type coercion).
-   === → Strict equality (no coercion).
```js
"5" == 5  // true
"5" === 5 // false
```
## Closures
Function remembers variables from its lexical scope even after outer function execution ends.
#### Example
```js
function outer() {
  let count = 0;
  return function inner() {
    return ++count;
  }
}
const counter = outer();
counter(); // 1
counter(); // 2
```
## Hoisting
-   Variables (`var`) and functions are **hoisted** to the top of their scope.
-   `var` hoisted with **undefined**, `let/const` hoisted but in **temporal dead zone**.
## Synch vs Async JS
-   **Synchronous** → Executes line by line, blocking.
-   **Asynchronous** → Doesn’t block, uses callbacks, promises, async/await.
## Promises vs async/await
-   **Promise** → Handles async results (`then/catch`).
-   **async/await**→ Cleaner syntax, built on top of Promises.
```js
async function getData() {
  const data = await fetch(...);
}
```
## map(), forEach(), filter(), reduce()
-   **map** → Transforms array, returns new array.
-   **forEach** → Iterates, no return value.
-   **filter** → Returns subset matching condition.
-   **reduce** → Accumulates to a single value.
## Debounce vs Throttle
-   **Debounce** → Delay execution until after a pause in events.
-   **Throttle** → Execute at most once in a given interval.
## this keyword
-   In object → Refers to object.
-   In function → undefined in strict mode, else global object.
-   In arrow function → Lexically bound (inherits from parent).
```js
const obj = {
  name: "JS",
  normal: function() { console.log(this.name); },
  arrow: () => console.log(this.name)
};
obj.normal(); // "JS"
obj.arrow();  // undefined
```
