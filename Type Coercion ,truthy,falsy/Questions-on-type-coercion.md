## Questions on Type Coercion

###### What's the output?

```js
+true;
!'Lydia';
```

- A: `1` and `false`
- B: `false` and `NaN`
- C: `false` and `false`

**Answer**:

Answer: A

The unary plus tries to convert an operand to a number. `true` is `1`, and `false` is `0`.

The string `'Lydia'` is a truthy value. What we're actually asking, is "Is this truthy value falsy?". This returns `false`.



###### What's the output?

```js
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `true`

**Answer**:

Answer: C

`new Number()` is a built-in function  constructor. Although it looks like a number, it's not really a number:  it has a bunch of extra features and is an object.

When we use the `==` operator (Equality operator), it only checks whether it has the same *value*. They both have the value of `3`, so it returns `true`.

However, when we use the `===` operator (Strict equality operator), both value *and* type should be the same. It's not: `new Number()` is not a number, it's an **object**. Both return `false.`



###### What's the output?

```js
function sum(a, b) {
  return a + b;
}

sum(1, '2');
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

**Answer**:

Answer: C

JavaScript is a **dynamically typed language**: we don't specify what types certain variables are. Values can  automatically be converted into another type without you knowing, which  is called *implicit type coercion*. **Coercion** is converting from one type into another.

In this example, JavaScript converts the number `1` into a string, in order for the function to make sense and return a value. During the addition of a numeric type (`1`) and a string type (`'2'`), the number is treated as a string. We can concatenate strings like `"Hello" + "World"`, so what's happening here is `"1" + "2"` which returns `"12"`.



###### Which of these values are falsy?

```js
0;
new Number(0);
('');
(' ');
new Boolean(false);
undefined;
```

- A: `0`, `''`, `undefined`
- B: `0`, `new Number(0)`, `''`, `new Boolean(false)`, `undefined`
- C: `0`, `''`, `new Boolean(false)`, `undefined`
- D: All of them are falsy

**Answer**:

Answer: A

There are 8 falsy values:

- `undefined`
- `null`
- `NaN`
- `false`
- `''` (empty string)
- `0`
- `-0`
- `0n` (BigInt(0))

Function constructors, like `new Number` and `new Boolean` are truthy.



###### What's the output?

```js
!!null;
!!'';
!!1;
```

- A: `false` `true` `false`
- B: `false` `false` `true`
- C: `false` `true` `true`
- D: `true` `true` `false`

**Answer**:

Answer: B

`null` is falsy. `!null` returns `true`. `!true` returns `false`.

`""` is falsy. `!""` returns `true`. `!true` returns `false`.

`1` is truthy. `!1` returns `false`. `!false` returns `true`.





###### What's the output?

```js
console.log(3 + 4 + '5');
```

- A: `"345"`
- B: `"75"`
- C: `12`
- D: `"12"`

**Answer**:

Answer: B

Operator associativity is the order in which the compiler  evaluates the expressions, either left-to-right or right-to-left. This  only happens if all operators have the *same* precedence. We only have one type of operator: `+`. For addition, the associativity is left-to-right.

`3 + 4` gets evaluated first. This results in the number `7`.

`7 + '5'` results in `"75"` because of coercion. JavaScript converts the number `7` into a string, see question 15. We can concatenate two strings using the `+`operator. `"7" + "5"` results in `"75"`.



###### What's the output?

```js
console.log(Number(2) === Number(2));
console.log(Boolean(false) === Boolean(false));
console.log(Symbol('foo') === Symbol('foo'));
```

- A: `true`, `true`, `false`
- B: `false`, `true`, `false`
- C: `true`, `false`, `true`
- D: `true`, `true`, `true`

**Answer**:

Answer: A

Every Symbol is entirely unique. The purpose of the  argument passed to the Symbol is to give the Symbol a description. The  value of the Symbol is not dependent on the passed argument. As we test  equality, we are creating two entirely new symbols: the first `Symbol('foo')`, and the second `Symbol('foo')`. These two values are unique and not equal to each other, `Symbol('foo') === Symbol('foo')` returns `false`.