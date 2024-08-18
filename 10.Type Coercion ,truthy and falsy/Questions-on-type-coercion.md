## Questions on Type Coercion

#### Q1:What's the output?

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

#### Q2:What's the output?

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

#### Q3:What's the output?

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

#### Q4:Which of these values are falsy?

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

#### Q5:What's the output?

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

#### Q6:What's the output?

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

#### Q7:What's the output?

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

#### Q8:Which option is a way to set `hasName` equal to `true`, provided you cannot pass `true` as an argument?

```js
function getName(name) {
  const hasName = //
}
```

- A: `!!name`
- B: `name`
- C: `new Boolean(name)`
- D: `name.length`

**Answer**:

Answer: A

With `!!name`, we determine whether the value of `name` is truthy or falsy. If the name is truthy, which we want to test for, `!name` returns `false`. `!false` (which is what `!!name` practically is) returns `true`.

By setting `hasName` equal to `name`, you set `hasName` equal to whatever value you passed to the `getName` function, not the boolean value `true`.

`new Boolean(true)` returns an object wrapper, not the boolean value itself.

`name.length` returns the length of the passed argument, not whether it's `true`.

#### Q9:What's the value of output?

```js
// 🎉✨ This is my 100th question! ✨🎉

const output = `${[] && 'Im'}possible!
You should${'' && `n't`} see a therapist after so much JavaScript lol`;
```

- A: `possible! You should see a therapist after so much JavaScript lol`
- B: `Impossible! You should see a therapist after so much JavaScript lol`
- C: `possible! You shouldn't see a therapist after so much JavaScript lol`
- D: `Impossible! You shouldn't see a therapist after so much JavaScript lol`

**Answer**:

Answer: B

`[]` is a truthy value. With the `&&` operator, the right-hand value will be returned if the left-hand value is a truthy value. In this case, the left-hand value `[]` is a truthy value, so `"Im'` gets returned.

`""` is a falsy value. If the left-hand value is falsy, nothing gets returned. `n't` doesn't get returned.

#### Q10:What's the value of output?

```js
const one = false || {} || null;
const two = null || false || '';
const three = [] || 0 || true;

console.log(one, two, three);
```

- A: `false` `null` `[]`
- B: `null` `""` `true`
- C: `{}` `""` `[]`
- D: `null` `null` `true`

**Answer**:

Answer: C

With the `||` operator, we can return the first truthy operand. If all values are falsy, the last operand gets returned.

`(false || {} || null)`: the empty object `{}` is a truthy value. This is the first (and only) truthy value, which gets returned. `one` is equal to `{}`.

`(null || false || "")`: all operands are falsy values. This means that the last operand, `""` gets returned. `two` is equal to `""`.

`([] || 0 || "")`: the empty array`[]` is a truthy value. This is the first truthy value, which gets returned. `three` is equal to `[]`.

#### Q11:What's the output?

```js
const name = 'Lydia Hallie';

console.log(!typeof name === 'object');
console.log(!typeof name === 'string');
```

- A: `false` `true`
- B: `true` `false`
- C: `false` `false`
- D: `true` `true`

**Answer**:

Answer: C

`typeof name` returns `"string"`. The string `"string"` is a truthy value, so `!typeof name` returns the boolean value `false`. `false === "object"` and `false === "string"` both return`false`.

(If we wanted to check whether the type was (un)equal to a certain type, we should've written `!==` instead of `!typeof`)

#### Q12:What's the output?

```js
let count = 0;
const nums = [0, 1, 2, 3];

nums.forEach(num => {
	if (num) count += 1
})

console.log(count)
```

- A: 1
- B: 2
- C: 3
- D: 4

**Answer**:

Answer: C

The `if` condition within the `forEach` loop checks whether the value of `num` is truthy or falsy. Since the first number in the `nums` array is `0`, a falsy value, the `if` statement's code block won't be executed. `count` only gets incremented for the other 3 numbers in the `nums` array, `1`, `2` and `3`. Since `count` gets incremented by `1` 3 times, the value of `count` is `3`.

#### Q13:**What will be the output**

```js
let f = "8";
let a = 1;
console.log((+f)+a+1);
```

**Answer**:

- **Output** : 10
- **Reason** : The expression (+f) is a shorthand way to convert the string value of f to a number. Therefore, (+f) evaluates to 8.

**What will be the output**

```js
console.log(5 < 6 < 7);
```

**Answer**:

- **Output** : true
- **Reason** : In JavaScript, the < operator evaluates  expressions from left to right. First, the expression 5 < 6 is  evaluated, resulting in true because 5 is less than 6. Then, the  expression true < 7 is evaluated. In this case, JavaScript performs  type coercion and converts true to the number 1. Therefore, the  expression becomes 1 < 7, which is true.

#### Q14:**What will be the output**

```js
console.log(7 > 6 > 5);
```

**Answer**:

- **Output** : false
- **Reason** : In JavaScript, the > operator evaluates  expressions from left to right. First, the expression 7 > 6 is  evaluated, resulting in true because 7 is greater than 6. Then, the  expression true > 5 is evaluated. In this case, JavaScript performs  type coercion and converts true to the number 1. Therefore, the  expression becomes 1 > 5, which is false.

#### Q15:**What will be the output**

```js
console.log(0 == false);
console.log(1 == true);
```

**Answer**:

- **Output** : true, true
- **Reason** : The == operator converts operands to a common type  before making the comparison. In both the cases, the boolean value will  be converted to a number, i.e., false is converted to 0 and true is  converted to 1. So, the expression 0 == false is equivalent to 0 == 0  and 1 == true is equivalent to 1 == 1.

#### Q16:**What will be the output**

```js
console.log(10 + "5");
console.log("5" + 10);
```

**Answer**:

- **Output** : 105, 510
- **Reason** : Since one operand is a string, the + operator performs string concatenation. 

#### Q17:**What will be the output**

```js
console.log(10 - "5");
console.log("5" - 10);
```

**Answer**:

- **Output** : 5, -5
- **Reason** : In JavaScript, when the subtraction operator - is  used, the operands are converted to numbers before performing the  subtraction 

#### Q18:**What will be the output**

```js
const arr1 = [1,2,3];
const arr2 = [1,2,3];
const str = "1,2,3";

console.log(arr1 == str);
console.log(arr1 == arr2);
```

**Answer**:

- **Output** : true, false
- **Reason for console.log(arr1 == str)** : Javascript compiler  performs type conversion. In this case, it converts the array arr1 and  the string str to their string representations and then compares them.
- **Reason for console.log(age)** : In Javascript arrays are  objects and objects are compared by reference. In this case, arr1 and  arr2 are pointing to 2 different memory locations

#### Q19:**What will be the output**

```js
var x = 0;
var y = 10;
if(x){
  console.log(x);
}
if(y){
  console.log(y);
}
```

**Answer**:

- **Output** : 10
- **Reason** : x = 0 is falsy and doesn't trigger the console.log(x), while y = 10 is truthy and triggers the console.log(y).

#### Q20:What is unary plus operator ? 

**Answer**: The Unary plus(+) operator precedes its operand and evaluates to its operand but attempts to convert it into a number if it isnt already 

Usage with numbers : 

```js
const x = 1;
const y = -1;

console.log(+x);
// 1
console.log(+y);
// -1
```

Usuage with Non Numbers :

```js
true  // 1
+false // 0
+null  // 0
+[]    // 0
+function (val) { return val; } // NaN
+1n    // throws TypeError: Cannot convert BigInt value to number
```

If it cannot parse a particular value, it will evaluate to `NaN`. Unlike other arithmetic operators, which work with both numbers and BigInts, using the `+` operator on BigInt values throws a `TypeError`.

#### Q21:Rules of Type Coercion ? 

**Answer**:

The rules governing type coercion in JavaScript include:

1. Any `numbers, boolean values` are converted to strings in where  strings are expected, such as `concatenation with strings` or `when using  string functions`.
2. `Non-numeric` values are converted to numbers in where numbers are required, such as `arithmetic operations or comparisons.`
3. `Values` are converted to booleans where booleans are expected, such as `logical operations or conditional statements.`
4. If a conversion is not possible, it results in `NaN` (Not-a-Number), typically in arithmetic operations involving non-numeric values.

#### Q22:What are the 8 falsy values ? 

**Answer**:

There are 8 falsy values:

- `undefined`
- `null`
- `NaN`
- `false`
- `''` (empty string)
- `0`
- `-0`
- `0n` (BigInt(0))