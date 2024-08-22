## Theory about generator functions

Normal functions follow something called a **run-to-completion** model: when we invoke a function, it will always run until it completes , generator functions  don't follow the **run-to-completion** model! 



We create a generator function by writing an asterisk `*` after the `function` keyword.

![generator-1](../assets/generator-1.png)

Generator functions actually work in a completely different way compared to regular functions:

- Invoking a generator function returns a **generator object**, which is an iterator.
- We can use the `yield` keyword in a generator function to "pause" the execution. 

With generator functions, we can write something like this (`genFunc` is short for `generatorFunction`):

```js
function* genFunc() {

  yield "✨";

  console.log("First log!");

  yield "💞";

  console.log("Second log!");

  return "Done!";

}
```

The execution of the generator gets "paused" when it encounters a `yield` keyword. The next time we run the function,  it remembers where it previously paused, and runs from there on! 

The generator object contains a `next` method (on the  prototype chain). This method is what we'll use to iterate the generator object. 

![gen-func-gif1](../assets/gen-func-gif1.gif)