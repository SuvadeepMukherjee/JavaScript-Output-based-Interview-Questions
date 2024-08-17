## Closures 

###### Q:What's the output?

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` and `0 1 2`
- B: `0 1 2` and `3 3 3`
- C: `3 3 3` and `0 1 2`

**Answer**:

Answer: C

Because of the event queue in JavaScript, the `setTimeout` callback function is called *after* the loop has been executed. Since the variable `i` in the first loop was declared using the `var` keyword, this value was global. During the loop, we incremented the value of `i` by `1` each time, using the unary operator `++`. By the time the `setTimeout` callback function was invoked, `i` was equal to `3` in the first example.

In the second loop, the variable `i` was declared using the `let` keyword: variables declared with the `let` (and `const`) keyword are block-scoped (a block is anything between `{ }`). During each iteration, `i` will have a new value, and each value is scoped inside the loop.



###### What is the output?

```js
const add = () => {
  const cache = {};
  return num => {
    if (num in cache) {
      return `From cache! ${cache[num]}`;
    } else {
      const result = num + 10;
      cache[num] = result;
      return `Calculated! ${result}`;
    }
  };
};

const addFunction = add();
console.log(addFunction(10));
console.log(addFunction(10));
console.log(addFunction(5 * 2));
```

- A: `Calculated! 20` `Calculated! 20` `Calculated! 20`
- B: `Calculated! 20` `From cache! 20` `Calculated! 20`
- C: `Calculated! 20` `From cache! 20` `From cache! 20`
- D: `Calculated! 20` `From cache! 20` `Error`

**Answer**:

Answer: C

The `add` function is a *memoized*  function. With memoization, we can cache the results of a function in  order to speed up its execution. In this case, we create a `cache` object that stores the previously returned values.

If we call the `addFunction` function again  with the same argument, it first checks whether it has already gotten  that value in its cache. If that's the case, the cache value will be  returned, which saves execution time. Otherwise, if it's not cached, it  will calculate the value and store it afterward.

We call the `addFunction` function three times with the same value: on the first invocation, the value of the function when `num` is equal to `10` isn't cached yet. The condition of the if-statement `num in cache` returns `false`, and the else block gets executed: `Calculated! 20` gets logged, and the value of the result gets added to the cache object. `cache` now looks like `{ 10: 20 }`.

The second time, the `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.

The third time, we pass `5 * 2` to the function which gets evaluated to `10`. The `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.



**What will be the output**

```js
for(var i = 0; i < 10; i++){
    setTimeout(function(){
      console.log("value is " + i);
  })
}
```

**Answer**:

- **Output** : 10 times, "value is 10"
- **Reason** : "var" has a function scope, and there will be only  one shared binding for the iterations. By the time the setTimeout  function gets executed, the for loop has already completed and the value of the variable i is 10.

**What will be the output**

```js
for(let i = 0; i < 10; i++){
    setTimeout(function(){
      console.log("value is " + i);
  })
}
```

**Answer**:

- **Output** : 10 times "value is" followed by the value of i in each iteration, from 0 to 9
- **Reason** : "let" has a block scope, and a new binding will be  created for each iteration. Here, a new variable i is created and has a  different value for each iteration of the loop.