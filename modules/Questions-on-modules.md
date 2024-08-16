## Questions on modules



###### What's the output?

```js
// counter.js
let counter = 10;
export default counter;
```

```js
// index.js
import myCounter from './counter';

myCounter += 1;

console.log(myCounter);
```

- A: `10`
- B: `11`
- C: `Error`
- D: `NaN`

**Answer**:

Answer: C

An imported module is *read-only*: you cannot modify the imported module. Only the module that exports them can change its value.

When we try to increment the value of `myCounter`, it throws an error: `myCounter` is read-only and cannot be modified.



###### What's the output?

```js
// index.js
console.log('running index.js');
import { sum } from './sum.js';
console.log(sum(1, 2));

// sum.js
console.log('running sum.js');
export const sum = (a, b) => a + b;
```

- A: `running index.js`, `running sum.js`, `3`
- B: `running sum.js`, `running index.js`, `3`
- C: `running sum.js`, `3`, `running index.js`
- D: `running index.js`, `undefined`, `running sum.js`

**Answer**:

Answer: B

With the `import` keyword, all imported modules are *pre-parsed*. This means that the imported modules get run *first*, and the code in the file that imports the module gets executed *after*.

This is a difference between `require()` in CommonJS and `import`! With `require()`, you can load dependencies on demand while the code is being run. If we had used `require` instead of `import`, `running index.js`, `running sum.js`, `3` would have been logged to the console.