## Questions on Variable declaration

###### What's the output?

```js
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

- A: `{}`
- B: `ReferenceError: greetign is not defined`
- C: `undefined`

**Answer**:

Answer: A

It logs the object, because we just created an empty object on the global object! When we mistyped `greeting` as `greetign`, the JS interpreter actually saw this as:

1. `global.greetign = {}` in Node.js
2. `window.greetign = {}`, `frames.greetign = {}` and `self.greetign` in browsers.
3. `self.greetign` in web workers.
4. `globalThis.greetign` in all environments.

In order to avoid this, we can use `"use strict"`. This makes sure that you have declared a variable before setting it equal to anything.



###### What's the output?

```js
var num = 8;
var num = 10;

console.log(num);  
```

- A: `8`
- B: `10`
- C: `SyntaxError`
- D: `ReferenceError`

**Answer**:

Answer: B

With the `var` keyword, you can declare multiple variables with the same name. The variable will then hold the latest value.

You cannot do this with `let` or `const` since they're block-scoped and therefore can't be redeclared.





