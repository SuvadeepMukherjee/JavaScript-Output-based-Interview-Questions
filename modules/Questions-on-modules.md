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



###### What's the output?

```js
// module.js
export default () => 'Hello world';
export const name = 'Lydia';

// index.js
import * as data from './module';

console.log(data);
```

- A: `{ default: function default(), name: "Lydia" }`
- B: `{ default: function default() }`
- C: `{ default: "Hello world", name: "Lydia" }`
- D: Global object of `module.js`

**Answer**:

Answer: A

With the `import * as name` syntax, we import *all exports* from the `module.js` file into the `index.js` file as a new object called `data` is created. In the `module.js` file, there are two exports: the default export, and a named export. The default export is a function that returns the string `"Hello World"`, and the named export is a variable called `name` which has the value of the string `"Lydia"`.

The `data` object has a `default` property for the default export, other properties have the names of the named exports and their corresponding values.





###### How can we invoke `sum` in `sum.js` from `index.js?`

```js
// sum.js
export default function sum(x) {
  return x + x;
}

// index.js
import * as sum from './sum';
```

- A: `sum(4)`
- B: `sum.sum(4)`
- C: `sum.default(4)`
- D: Default aren't imported with `*`, only named exports

**Answer**:

Answer: C

With the asterisk `*`, we import all exported values from that file, both default and named. If we had the following file:

```js
// info.js
export const name = 'Lydia';
export const age = 21;
export default 'I love JavaScript';

// index.js
import * as info from './info';
console.log(info);
```

​    The following would get logged:

```
{
  default: "I love JavaScript",
  name: "Lydia",
  age: 21
}
```

​    For the `sum` example, it means that the imported value `sum` looks like this:

```js
{ default: function sum(x) { return x + x } }
```

​    We can invoke this function, by calling `sum.default`