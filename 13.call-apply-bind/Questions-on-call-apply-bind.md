## Questions on call-apply-bind

#### Q1:What's the output?

```js
const person = { name: 'Lydia' };

function sayHi(age) {
  return `${this.name} is ${age}`;
}

console.log(sayHi.call(person, 21));
console.log(sayHi.bind(person, 21));
```

- A: `undefined is 21` `Lydia is 21`
- B: `function` `function`
- C: `Lydia is 21` `Lydia is 21`
- D: `Lydia is 21` `function`

**Answer**:

Answer: D

With both, we can pass the object to which we want the `this` keyword to refer to. However, `.call` is also *executed immediately*!

`.bind.` returns a *copy* of the function, but with a bound context! It is not executed immediately.