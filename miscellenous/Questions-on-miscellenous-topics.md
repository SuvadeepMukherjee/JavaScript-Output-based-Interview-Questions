## Questions on Miscellenous Topics

###### What's the output?

```js
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

- A: `1` `2`
- B: `1` `2` `3`
- C: `1` `2` `4`
- D: `1` `3` `4`

**Answer**:

Answer: C

The `continue` statement skips an iteration if a certain condition returns `true`.



###### What's the output?

```js
console.log(typeof typeof 1);
```

- A: `"number"`
- B: `"string"`
- C: `"object"`
- D: `"undefined"`

**Answer**:

#### Answer: B

typeof 1` returns `"number"`. `typeof "number"` returns `"string"





###### Everything in JavaScript is either a...

- A: primitive or object
- B: function or object
- C: trick question! only objects
- D: number or object

**Answer**:

Answer: A

JavaScript only has primitive types and objects.

Primitive types are `boolean`, `null`, `undefined`, `bigint`, `number`, `string`, and `symbol`.

What differentiates a primitive from an object is that  primitives do not have any properties or methods; however, you'll note  that `'foo'.toUpperCase()` evaluates to `'FOO'` and does not result in a `TypeError`. This is because when you try to access a property or method on a  primitive like a string, JavaScript will implicitly wrap the primitive  type using one of the wrapper classes, i.e. `String`, and then immediately discard the wrapper after the expression evaluates. All primitives except for `null` and `undefined` exhibit this behavior.





###### What's the value of `num`?

```js
const num = parseInt('7*6', 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

**Answer**:

Answer: C

Only the first number in the string is returned. Based on the *radix* (the second argument in order to specify what type of number we want to parse it to: base 10, hexadecimal, octal, binary, etc.), the `parseInt` checks whether the characters in the string are valid. Once it  encounters a character that isn't a valid number in the radix, it stops  parsing and ignores the following characters.

`*` is not a valid number. It only parses `"7"` into the decimal `7`. `num` now holds the value of `7`.





###### What's the output ? 

```js
function greeting() {
  throw 'Hello world!';
}

function sayHi() {
  try {
    const data = greeting();
    console.log('It worked!', data);
  } catch (e) {
    console.log('Oh no an error:', e);
  }
}

sayHi();
```

- A: `It worked! Hello world!`
- B: `Oh no an error: undefined`
- C: `SyntaxError: can only throw Error objects`
- D: `Oh no an error: Hello world!`

**Answer**:

Answer: D

With the `throw` statement, we can create custom errors. With this statement, you can throw exceptions. An exception can be a **string**, a **number**, a **boolean** or an **object**. In this case, our exception is the string `'Hello world!'`.

With the `catch` statement, we can specify what to do if an exception is thrown in the `try` block. An exception is thrown: the string `'Hello world!'`. `e` is now equal to that string, which we log. This results in `'Oh an error: Hello world!'`.





###### What's the output?

```js
const name = 'Lydia';
age = 21;

console.log(delete name);
console.log(delete age);
```

- A: `false`, `true`
- B: `"Lydia"`, `21`
- C: `true`, `true`
- D: `undefined`, `undefined`

**Answer**:

Answer: A

The `delete` operator returns a boolean value: `true` on a successful deletion, else it'll return `false`. However, variables declared with the `var`, `const`, or `let` keywords cannot be deleted using the `delete` operator.

The `name` variable was declared with a `const` keyword, so its deletion is not successful: `false` is returned. When we set `age` equal to `21`, we actually added a property called `age` to the global object. You can successfully delete properties from objects this way, also the global object, so `delete age` returns `true`.