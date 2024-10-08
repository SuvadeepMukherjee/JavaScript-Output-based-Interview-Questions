## Questions on scoping, shadowing,hoisting,execution context,temporal dead zone

#### Q1. What's the output?

```js
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}

sayHi();
```

- A: `Lydia` and `undefined`
- B: `Lydia` and `ReferenceError`
- C: `ReferenceError` and `21`
- D: `undefined` and `ReferenceError`

**Answer**:

Answer: D

Within the function, we first declare the `name` variable with the `var` keyword. This means that the variable gets hoisted (memory space is set up during the creation phase) with the default value of `undefined`, until we actually get to the line where we define the variable. We  haven't defined the variable yet on the line where we try to log the `name` variable, so it still holds the value of `undefined`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get *initialized*. They are not accessible before the line we declare (initialize) them.  This is called the "temporal dead zone". When we try to access the  variables before they are declared, JavaScript throws a `ReferenceError`.

#### Q2:The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.

- A: true
- B: false
- C: it depends

**Answer**:

Answer: A

The base execution context is the global execution context: it's what's accessible everywhere in your code.

#### Q3:What is the output?

```js
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young.";
  } else {
    const message = "Yay! You're old enough!";
  }

  return message;
}

console.log(checkAge(21));
```

- A: `"Sorry, you're too young."`
- B: `"Yay! You're old enough!"`
- C: `ReferenceError`
- D: `undefined`

**Answer**:

Answer: C

Variables with the `const` and `let` keywords are *block-scoped*. A block is anything between curly brackets (`{ }`). In this case, the curly brackets of the if/else statements. You cannot  reference a variable outside of the block it's declared in, a  ReferenceError gets thrown.

#### Q4:What's the output?

```js
let name = 'Lydia';

function getName() {
  console.log(name);
  let name = 'Sarah';
}

getName();
```

- A: Lydia
- B: Sarah
- C: `undefined`
- D: `ReferenceError`

**Answer**:

Answer: D

Each function has its own *execution context* (or *scope*). The `getName` function first looks within its own context (scope) to see if it contains the variable `name` we're trying to access. In this case, the `getName` function contains its own `name` variable: we declare the variable `name` with the `let` keyword, and with the value of `'Sarah'`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get *initialized*. They are not accessible before the line we declare (initialize) them.  This is called the "temporal dead zone". When we try to access the  variables before they are declared, JavaScript throws a `ReferenceError`.

If we wouldn't have declared the `name` variable within the `getName` function, the javascript engine would've looked down the *scope chain*. The outer scope has a variable called `name` with the value of `Lydia`. In that case, it would've logged `Lydia`.

```js
let name = 'Lydia';

function getName() {
  console.log(name);
}

getName(); // Lydia
```

####   Q5:What's the output?

```js
const randomValue = 21;

function getInfo() {
  console.log(typeof randomValue);
  const randomValue = 'Lydia Hallie';
}

getInfo();
```

- A: `"number"`
- B: `"string"`
- C: `undefined`
- D: `ReferenceError`

**Answer**:

Answer: D

Variables declared with the `const` keyword are not referenceable before their initialization: this is called the *temporal dead zone*. In the `getInfo` function, the variable `randomValue` is scoped in the functional scope of `getInfo`. On the line where we want to log the value of `typeof randomValue`, the variable `randomValue` isn't initialized yet: a `ReferenceError` gets thrown! The engine didn't go down the scope chain since we declared the variable `randomValue` in the `getInfo` function.

#### Q6:**What will be the output**

```js
x = 10;
console.log(x);
var x;
```

**Answer**:

- **Output** : 10
- **Reason** : The declaration of the variable x is hoisted to the top of its scope.

**What will be the output**

```js
let a = 10;
if(true){
   let a = 20;
   console.log(a, "inside");
}
console.log(a, "outside");
```

**Answer**:

- **Output** : 20, "inside" and 10, "outside"
- **Reason** : The variable "a" declared inside "if" has block scope and does not affect the value of the outer "a" variable.

#### Q7:**What will be the output**

```js
var a = "xyz";
var a = "pqr";
console.log(a)
```

**Answer**:

- **Output** : "pqr"
- **Reason** : Both the variables are declared using "var" keyword with the same name "a". The second variable declaration will override  the first variable declaration.

#### Q8:**What will be the output**

```js
console.log(printName());
function printName(){
    return "Hi my name is Bob"
}
```

**Answer**:

- **Output** : Hi my name is Bob
- **Reason** : Regular functions are hoisted to the top. And you can access and call them even before they are declared. 

#### Q9:**What will be the output**

```js
console.log(printName());
const printName = () => {
    return "Hi my name is Bob"
}
```

**Answer**:

- **Output** : ReferenceError: Cannot access 'printName' before initialization
- **Reason** : Arrow functions cannot be accessed before they are initialised. 

#### Q10:**What will be the output**

```js
function hello(){
console.log(name);
console.log(age);
var name = "Alice";
let age = 21;
}
hello();
```

**Answer**:

- **Output** : undefined, ReferenceError: can't access lexical declaration 'age' before initialization"
- **Reason for console.log(name)** : The variable name (declared  with var) is hoisted to the top, so JavaScript knows it exists, but it  hasn't been assigned a value yet, so it prints undefined
- **Reason for console.log(age)** : The variable age (declared  with let) is also hoisted to the top of its scope, but unlike var, it is not initialized until the line where it is declared.

#### Q11:**What will be the output**

```js
var a = 10;
let a = 20;
console.log(a)
```

**Answer**:

- **Output** : SyntaxError: Identifier 'a' has already been declared
- **Reason** : In Javascript, we cannot redeclare a variable with let if it has already been declared in the same scope. 

#### Q12:What's the output?

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

#### Q13:What's the output?

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

#### Q14:What's the output?

```js
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = 'Lydia';
const age = 21;

getPersonInfo`${person} is ${age} years old`;  
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

**Answer**:

Answer: B

If you use tagged template literals, the value of the  first argument is always an array of the string values. The remaining  arguments get the values of the passed expressions!

#### Q15:What's the output?

```js
console.log(`${(x => x)('I love')} to program`);
```

- A: `I love to program`
- B: `undefined to program`
- C: `${(x => x)('I love') to program`
- D: `TypeError`

**Answer**:

Answer: A

Expressions within template literals are evaluated first.  This means that the string will contain the returned value of the  expression, the immediately invoked function `(x => x)('I love')` in this case. We pass the value `'I love'` as an argument to the `x => x` arrow function. `x` is equal to `'I love'`, which gets returned. This results in `I love to program`.
