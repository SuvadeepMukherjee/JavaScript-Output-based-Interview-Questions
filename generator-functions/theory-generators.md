## Theory about generator functions

Normal functions follow something called a **run-to-completion** model: when we invoke a function, it will always run until it completes , generator functions  don't follow the **run-to-completion** model! 



We create a generator function by writing an asterisk `*` after the `function` keyword.

![generator-1](../assets/generator-1.png)

Generator functions actually work in a completely different way compared to regular functions:

- Invoking a generator function returns a **generator object**, which is an iterator.
- We can use the `yield` keyword in a generator function to "pause" the execution. 