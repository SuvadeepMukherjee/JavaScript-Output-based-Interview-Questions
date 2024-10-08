## Questions on Asynchronous Javascript

#### Q1:What's the output?

```js
const foo = () => console.log('First');
const bar = () => setTimeout(() => console.log('Second'));
const baz = () => console.log('Third');

bar();
foo();
baz();
```

- A: `First` `Second` `Third`
- B: `First` `Third` `Second`
- C: `Second` `First` `Third`
- D: `Second` `Third` `First`

**Answer**:

#### Answer: B

We have a `setTimeout` function and invoked it first. Yet, it was logged last.

This is because in browsers, we don't just have the runtime engine, we also have something called a `WebAPI`. The `WebAPI` gives us the `setTimeout` function to start with, and for example the DOM.

After the *callback* is pushed to the WebAPI, the `setTimeout` function itself (but not the callback!) is popped off the stack.

![el1](../assets/el1.png)

Now, `foo` gets invoked, and `"First"` is being logged.

![el2](../assets/el2.png)

`foo` is popped off the stack, and `baz` gets invoked. `"Third"` gets logged.

![el3](../assets/el3.png)

The WebAPI can't just add stuff to the stack whenever it's ready.  Instead, it pushes the callback function to something called the *queue*.

![el4](../assets/el4.png)

This is where an event loop starts to work. An **event loop** looks at the stack and task queue. If the stack is empty, it takes the first thing on the queue and pushes it onto the stack.

![el5](../assets/el5.png)

`bar` gets invoked, `"Second"` gets logged, and it's popped off the stack.

#### Q2:What does the `setInterval` method return in the browser?

```js
setInterval(() => console.log('Hi'), 1000);
```

- A: a unique id
- B: the amount of milliseconds specified
- C: the passed function
- D: `undefined`

**Answer**:

Answer: A

It returns a unique id. This id can be used to clear that interval with the `clearInterval()` function.

### Q3:What does this return?

```js
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, 'one');
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, 'two');
});

Promise.race([firstPromise, secondPromise]).then(res => console.log(res));
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

**Answer**:

Answer: B

When we pass multiple promises to the `Promise.race` method, it resolves/rejects the *first* promise that resolves/rejects. To the `setTimeout` method, we pass a timer: 500ms for the first promise (`firstPromise`), and 100ms for the second promise (`secondPromise`). This means that the `secondPromise` resolves first with the value of `'two'`. `res` now holds the value of `'two'`, which gets logged.

#### Q4:What's the output?

```js
async function getData() {
  return await Promise.resolve('I made it!');
}

const data = getData();
console.log(data);
```

- A: `"I made it!"`
- B: `Promise {<resolved>: "I made it!"}`
- C: `Promise {<pending>}`
- D: `undefined`

**Answer**:

Answer: C

An async function always returns a promise. The `await` still has to wait for the promise to resolve: a pending promise gets returned when we call `getData()` in order to set `data` equal to it.

If we wanted to get access to the resolved value `"I made it"`, we could have used the `.then()` method on `data`:

`data.then(res => console.log(res))`

This would've logged `"I made it!"`

#### Q5:What kind of information would get logged?

```js
fetch('https://www.website.com/api/user/1')
  .then(res => res.json())
  .then(res => console.log(res));
```

- A: The result of the `fetch` method.
- B: The result of the second invocation of the `fetch` method.
- C: The result of the callback in the previous `.then()`.
- D: It would always be undefined.

**Answer**:

Answer: C

The value of `res` in the second `.then` is equal to the returned value of the previous `.then`. You can keep chaining `.then`s like this, where the value is passed to the next handler.

#### Q6:What's the value of output?

```js
const myPromise = () => Promise.resolve('I have resolved!');

function firstFunction() {
  myPromise().then(res => console.log(res));
  console.log('second');
}

async function secondFunction() {
  console.log(await myPromise());
  console.log('second');
}

firstFunction();
secondFunction();
```

- A: `I have resolved!`, `second` and `I have resolved!`, `second`
- B: `second`, `I have resolved!` and `second`, `I have resolved!`
- C: `I have resolved!`, `second` and `second`, `I have resolved!`
- D: `second`, `I have resolved!` and `I have resolved!`, `second`

**Answer**:

Answer: D

With a promise, we basically say *I want to execute  this function, but I'll put it aside for now while it's running since  this might take a while. Only when a certain value is resolved (or  rejected), and when the call stack is empty, I want to use this value.*

We can get this value with both `.then` and the `await` keywords in an `async` function. Although we can get a promise's value with both `.then` and `await`, they work a bit differently.

In the `firstFunction`, we (sort of) put the myPromise function aside while it was running, but continued running the other code, which is `console.log('second')` in this case. Then, the function resolved with the string `I have resolved`, which then got logged after it saw that the callstack was empty.

With the await keyword in `secondFunction`, we literally pause the execution of an async function until the value has been resolved before moving to the next line.

This means that it waited for the `myPromise` to resolve with the value `I have resolved`, and only once that happened, we moved to the next line: `second` got logged.

#### Q7:What's its value?

```js
Promise.resolve(5);
```

- A: `5`
- B: `Promise {<pending>: 5}`
- C: `Promise {<fulfilled>: 5}`
- D: `Error`

**Answer**:

Answer: C

We can pass any type of value we want to `Promise.resolve`, either a promise or a non-promise. The method itself returns a promise with the resolved value (`<fulfilled>`). If you pass a regular function, it'll be a resolved promise with a  regular value. If you pass a promise, it'll be a resolved promise with  the resolved value of that passed promise.

In this case, we just passed the numerical value `5`. It returns a resolved promise with the value `5`.

#### Q8:What's the output?

```js
const myPromise = Promise.resolve('Woah some cool data');

(async () => {
  try {
    console.log(await myPromise);
  } catch {
    throw new Error(`Oops didn't work`);
  } finally {
    console.log('Oh finally!');
  }
})();
```

- A: `Woah some cool data`
- B: `Oh finally!`
- C: `Woah some cool data` `Oh finally!`
- D: `Oops didn't work` `Oh finally!`

**Answer**:

Answer: C

In the `try` block, we're logging the awaited value of the `myPromise` variable: `"Woah some cool data"`. Since no errors were thrown in the `try` block, the code in the `catch` block doesn't run. The code in the `finally` block *always* runs, `"Oh finally!"` gets logged.

#### Q9:What's the output?

```js
const myPromise = Promise.resolve(Promise.resolve('Promise'));

function funcOne() {
  setTimeout(() => console.log('Timeout 1!'), 0);
  myPromise.then(res => res).then(res => console.log(`${res} 1!`));
  console.log('Last line 1!');
}

async function funcTwo() {
  const res = await myPromise;
  console.log(`${res} 2!`)
  setTimeout(() => console.log('Timeout 2!'), 0);
  console.log('Last line 2!');
}

funcOne();
funcTwo();
```

- A: `Promise 1! Last line 1! Promise 2! Last line 2! Timeout 1! Timeout 2!`
- B: `Last line 1! Timeout 1! Promise 1! Last line 2! Promise2! Timeout 2! `
- C: `Last line 1! Promise 2! Last line 2! Promise 1! Timeout 1! Timeout 2!`
- D: `Timeout 1! Promise 1! Last line 1! Promise 2! Timeout 2! Last line 2!`

**Answer**:

Answer: C

First, we invoke `funcOne`. On the first line of `funcOne`, we call the *asynchronous* `setTimeout` function, from which the callback is sent to the Web API. (see my article on the event loop [here](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif).)

Then we call the `myPromise` promise, which is an *asynchronous* operation. Pay attention, that now only the first then clause was added to the microtask queue.

Both the promise and the timeout are asynchronous  operations, the function keeps on running while it's busy completing the promise and handling the `setTimeout` callback. This means that `Last line 1!` gets logged first, since this is not an asynchonous operation.

Since the callstack is not empty yet, the `setTimeout` function and promise in `funcOne` cannot get added to the callstack yet.

In `funcTwo`, the variable `res` gets `Promise` because `Promise.resolve(Promise.resolve('Promise'))` is equivalent to `Promise.resolve('Promise')` since resolving a promise just resolves it's value. The `await` in this line stops the execution of the function until it receives the  resolution of the promise and then keeps on running synchronously until  completion, so `Promise 2!` and then `Last line 2!` are logged and the `setTimeout` is sent to the Web API. If the first then clause in `funcOne` had its own log statement, it would be printed before `Promise 2!`. Howewer, it executed silently and put the second then clause in microtask queue. So, the second clause will be printed after `Promise 2!`.

Then the call stack is empty. Promises are *microtasks* so they are resolved first when the call stack is empty so `Promise 1!` gets to be logged.

Now, since `funcTwo` popped off the call stack, the call stack is empty. The callbacks waiting in the queue (`() => console.log("Timeout 1!")` from `funcOne`, and `() => console.log("Timeout 2!")` from `funcTwo`) get added to the call stack one by one. The first callback logs `Timeout 1!`, and gets popped off the stack. Then, the second callback logs `Timeout 2!`, and gets popped off the stack.

#### Q10:What's the output?

```js
const promise1 = Promise.resolve('First')
const promise2 = Promise.resolve('Second')
const promise3 = Promise.reject('Third')
const promise4 = Promise.resolve('Fourth')

const runPromises = async () => {
	const res1 = await Promise.all([promise1, promise2])
	const res2  = await Promise.all([promise3, promise4])
	return [res1, res2]
}

runPromises()
	.then(res => console.log(res))
	.catch(err => console.log(err))
```

- A: `[['First', 'Second'], ['Fourth']]`
- B: `[['First', 'Second'], ['Third', 'Fourth']]`
- C: `[['First', 'Second']]`
- D: `'Third'`

**Answer**:

Answer: D

The `Promise.all` method runs the passed promises in parallel. If one promise fails, the `Promise.all` method *rejects* with the value of the rejected promise. In this case, `promise3` is rejected with the value `"Third"`. We’re catching the rejected value in the chained `catch` method on the `runPromises` invocation to catch any errors  within the `runPromises` function. Only `"Third"` gets logged, since `promise3` is rejected with this value.

#### Q11:**What will be the output**

```js
function hello() {
  console.log("1");
    setTimeout(() => {
        console.log("2");
    })
  console.log("3");
}
hello();
```

**Answer**;

- **Output** : "1" followed by "3", and then after a small delay, "2"
- **Reason** : console.log("1") statement logs "1" to the console. Then setTimeout() function is set to execute the callback function in  the next event loop iteration and logs "3" to the console.

#### Q12:Predict the output ? 

```js
const promise = new Promise((resolve, reject) => {
  reject(Error('Error occurred'));
});

promise.catch(error => console.log(error.message));
promise.catch(error => console.log(error.message));
```

**Answer**:

`Error occurred`

`Error occurred`

#### Q13:Guess the output 

```js
console.log("start");

const promise1 = new Promise((resolve, reject) => {

  console.log(1);

});

console.log("end");
```

**Answer**:

start 1 end

#### Q14:What is the output of this code snippet ? 

```js
function performTask() {

  return new Promise(function (resolve, reject) {

    reject();

  });

}

let taskPromise = performTask();

taskPromise

  .then(function () {

    console.log("Success 1");

  })

  .then(function () {

    console.log("Success 2");

  })

  .then(function () {

    "Success 3";

  })

  .catch(function () {

    console.log("Error 1");

  })

  .then(function () {

    console.log("Success 4");

  });
```

**Answer**:

`Error 1`

`Success 4`

#### Q15:Given the following code, what will be the final output ? 

```js
const promise = new Promise((resolve) => {
  resolve(1);
});

promise.then((value) => {
  console.log(value);
  return value + 1;
}).then((value) => {
  console.log(value);
  throw new Error('Something went wrong');
}).catch((error) => {
  console.error(error.message);
});
```

**Answer**:

```
1
2
Something went wrong
```

#### Q16:What is the output of the following code ? 

```js
var promise = new Promise(function(resolve, reject){
    setTimeout(function() {
        resolve('Resolved!');
    }, 1000);
});

promise.then(function(value) {
    console.log(value)
});
```

**Answer**:

`Resolved`

#### Q17:What is the output of the following code ? 

```js
let promise = new Promise(function (resolve, reject) {

  setTimeout(() => resolve(1), 1000);

});

promise

  .then(function (result) {

    console.log(result);
    return result + 2;

  })

  .then(function (result) {

    console.log(result);

    return result * 2;

  })

  .then(function (result) {

    console.log(result);

    return result * 2;

  });
```

**Answer**:

```
1
2
4
```

#### Q18:What is the output of the following code ? 

```js
console.log('Start');
setTimeout(() => {
 console.log('Timeout');
}, 0);
Promise.resolve().then(() => {
 console.log('Promise resolved');
});
console.log('End');
```

**Answer**:

Start End Promise resolved Timeout

#### Q19:What is the output of this code snippet ? 

```js
let firstTask = new Promise(function(resolve, reject) {
  setTimeout(resolve, 500, 'Task One');
});

let secondTask;

let thirdTask = new Promise(function(resolve, reject) {
  setTimeout(resolve, 1200, 'Task Three');
});

let fourthTask = new Promise(function(resolve, reject) {
  setTimeout(reject, 300, 'Task Four');
});

let fifthTask = new Promise(function(resolve, reject) {
  setTimeout(resolve, 1000, 'Task Two');
});

let combinedPromise = Promise.all([firstTask, secondTask, thirdTask, fourthTask, fifthTask]);

combinedPromise
  .then(function(data) {
    data.forEach(function(value) {
      console.log('Result:', value);
    });
  })
  .catch(function(error) {
    console.error('Error:', error);
  });
```

**Answer**:

Error: Task Four

#### Q20:What is the output of the following code ? 

```js
const promise1 = new Promise(resolve => setTimeout(resolve, 100, 'One'));
const promise2 = new Promise(resolve => setTimeout(resolve, 200, 'Two'));

Promise.race([promise1, promise2])
  .then(value => console.log(value))
  .catch(error => console.error(error));
```

**Answer**:

`One`

#### Q21:What is the output of the following code ? 

```js
const promise1 = Promise.resolve(1);
const promise2 = new Promise(resolve => setTimeout(resolve, 200, 2));
const promise3 = new Promise((resolve, reject) => setTimeout(reject, 100, 'Error'));

Promise.all([promise1, promise2, promise3])
  .then(values => console.log(values))
  .catch(error => console.error(error));
```

**Answer**:

Error

#### Q22:What is the output of the following code ? 

```js
Promise.resolve(1)
  .then(value => {
    console.log(value);
    return Promise.resolve(2);
  })
  .then(value => console.log(value));
```

**Answer**:

1 2

