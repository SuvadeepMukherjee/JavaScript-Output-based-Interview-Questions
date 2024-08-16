## Variable Hoisting and Temporal Dead Zone 

###### 1. What's the output?

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



###### The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.

- A: true
- B: false
- C: it depends

**Answer**:

Answer: A

The base execution context is the global execution context: it's what's accessible everywhere in your code.



###### What is the output?

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



###### What's the output?

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

​    