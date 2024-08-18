## Questions on Arrays

#### Q1:What's the output?

```js
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, null x 7, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, empty x 7, 11]`
- D: `SyntaxError`

**Answer**:

Answer: C

When you set a value to an element in an array that  exceeds the length of the array, JavaScript creates something called  "empty slots". These actually have the value of `undefined`, but you will see something like:

[1, 2, 3, empty x 7, 11]

depending on where you run it (it's different for every browser, node, etc.)

#### Q2:What's the output?

```js
[[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2],
);
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

**Answer**:

Answer: C

`[1, 2]` is our initial value. This is the value we start with, and the value of the very first `acc`. During the first round, `acc` is `[1,2]`, and `cur` is `[0, 1]`. We concatenate them, which results in `[1, 2, 0, 1]`.

Then, `[1, 2, 0, 1]` is `acc` and `[2, 3]` is `cur`. We concatenate them, and get `[1, 2, 0, 1, 2, 3]`

#### Q3:What's the output ?

```js
[1, 2, 3].map(num => {
  if (typeof num === 'number') return;
  return num * 2;
});
```

- A: `[]`
- B: `[null, null, null]`
- C: `[undefined, undefined, undefined]`
- D: `[ 3 x empty ]`

**Answer**:

Answer: C

When mapping over the array, the value of `num` is equal to the element it’s currently looping over. In this case, the  elements are numbers, so the condition of the if statement `typeof num === "number"` returns `true`. The map function creates a new array and inserts the values returned from the function.

However, we don’t return a value. When we don’t return a value from the function, the function returns `undefined`. For every element in the array, the function block gets called, so for each element we return `undefined`.

#### Q4:What's the output?

```js
[1, 2, 3, 4].reduce((x, y) => console.log(x, y));
```

- A: `1` `2` and `3` `3` and `6` `4`
- B: `1` `2` and `2` `3` and `3` `4`
- C: `1` `undefined` and `2` `undefined` and `3` `undefined` and `4` `undefined`
- D: `1` `2` and `undefined` `3` and `undefined` `4`

**Answer**:

Answer: D

The first argument that the `reduce` method receives is the *accumulator*, `x` in this case. The second argument is the *current value*, `y`. With the reduce method, we execute a callback function on every element in the array, which could ultimately result in one single value.

In this example, we are not returning any values, we are simply logging the values of the accumulator and the current value.

The value of the accumulator is equal to the previously returned value of the callback function. If you don't pass the optional `initialValue` argument to the `reduce` method, the accumulator is equal to the first element on the first call.

On the first call, the accumulator (`x`) is `1`, and the current value (`y`) is `2`. We don't return from the callback function, we log the accumulator, and the current values: `1` and `2` get logged.

If you don't return a value from a function, it returns `undefined`. On the next call, the accumulator is `undefined`, and the current value is `3`. `undefined` and `3` get logged.

On the fourth call, we again don't return from the callback function. The accumulator is again `undefined`, and the current value is `4`. `undefined` and `4` get logged.

#### Q5: What's the output?

```js
function addToList(item, list) {
  return list.push(item);
}

const result = addToList('apple', ['banana']);
console.log(result);
```

- A: `['apple', 'banana']`
- B: `2`
- C: `true`
- D: `undefined`

**Answer**:

Answer: B

The `.push()` method returns the *length* of the new array! Previously, the array contained one element (the string `"banana"`) and had a length of `1`. After adding the string `"apple"` to the array, the array contains two elements, and has a length of `2`. This gets returned from the `addToList` function.

The `push` method modifies the original array. If you wanted to return the *array* from the function rather than the *length of the array*, you should have returned `list` after pushing `item` to it.

#### Q6:What is the output?

```js
const myLifeSummedUp = ['☕', '💻', '🍷', '🍫'];

for (let item in myLifeSummedUp) {
  console.log(item);
}

for (let item of myLifeSummedUp) {
  console.log(item);
}
```

- A: `0` `1` `2` `3` and `"☕"` `"💻"` `"🍷"` `"🍫"`
- B: `"☕"` `"💻"` `"🍷"` `"🍫"` and `"☕"` `"💻"` `"🍷"` `"🍫"`
- C: `"☕"` `"💻"` `"🍷"` `"🍫"` and `0` `1` `2` `3`
- D: `0` `1` `2` `3` and `{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

**Answer**:

Answer: A

With a *for-in* loop, we can iterate over **enumerable** properties. In an array, the enumerable properties are the "keys" of  array elements, which are actually their indexes. You could see an array as:

`{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

Where the keys are the enumerable properties. `0` `1` `2` `3` get logged.

With a *for-of* loop, we can iterate over **iterables**. An array is an iterable. When we iterate over the array, the variable  "item" is equal to the element it's currently iterating over, `"☕"` `"💻"` `"🍷"` `"🍫"` get logged.

#### Q7:What is the output?

```js
const list = [1 + 2, 1 * 2, 1 / 2];
console.log(list);
```

- A: `["1 + 2", "1 * 2", "1 / 2"]`
- B: `["12", 2, 0.5]`
- C: `[3, 2, 0.5]`
- D: `[1, 1, 1]`

**Answer**:

Answer: C

Array elements can hold any value. Numbers, strings,  objects, other arrays, null, boolean values, undefined, and other  expressions such as dates, functions, and calculations.

The element will be equal to the returned value. `1 + 2` returns `3`, `1 * 2` returns `2`, and `1 / 2` returns `0.5`.

#### Q8:What's the output?

```js
let newList = [1, 2, 3].push(4);

console.log(newList.push(5));
```

- A: `[1, 2, 3, 4, 5]`
- B: `[1, 2, 3, 5]`
- C: `[1, 2, 3, 4]`
- D: `Error`

**Answer**:

Answer: D

The `.push` method returns the *new length* of the array, not the array itself! By setting `newList` equal to `[1, 2, 3].push(4)`, we set `newList` equal to the new length of the array: `4`.

Then, we try to use the `.push` method on `newList`. Since `newList` is the numerical value `4`, we cannot use the `.push` method: a TypeError is thrown.

#### Q9:Which of these methods modifies the original array?

```js
const emojis = ['✨', '🥑', '😍'];

emojis.map(x => x + '✨');
emojis.filter(x => x !== '🥑');
emojis.find(x => x !== '🥑');
emojis.reduce((acc, cur) => acc + '✨');
emojis.slice(1, 2, '✨');
emojis.splice(1, 2, '✨');
```

- A: `All of them`
- B: `map` `reduce` `slice` `splice`
- C: `map` `slice` `splice`
- D: `splice`

**Answer**:

Answer: D

With `splice` method, we modify the original  array by deleting, replacing or adding elements. In this case, we  removed 2 items from index 1 (we removed `'🥑'` and `'😍'`) and added the ✨ emoji instead.

`map`, `filter` and `slice` return a new array, `find` returns an element, and `reduce` returns a reduced value.

#### Q10:What's the output?

```js
let num = 1;
const list = ['🥳', '🤠', '🥰', '🤪'];

console.log(list[(num += 1)]);
```

- A: `🤠`
- B: `🥰`
- C: `SyntaxError`
- D: `ReferenceError`

**Answer**:

Answer: B

With the `+=` operator, we're incrementing the value of `num` by `1`. `num` had the initial value `1`, so `1 + 1` is `2`. The item on the second index in the `list` array is 🥰, `console.log(list[2])` prints 🥰.

#### Q11:What's the output?

```js
const groceries = ['banana', 'apple', 'peanuts'];

if (groceries.indexOf('banana')) {
  console.log('We have to buy bananas!');
} else {
  console.log(`We don't have to buy bananas!`);
}
```

- A: We have to buy bananas!
- B: We don't have to buy bananas
- C: `undefined`
- D: `1`

**Answer**:

Answer: B

We passed the condition `groceries.indexOf("banana")` to the if-statement. `groceries.indexOf("banana")` returns `0`, which is a falsy value. Since the condition in the if-statement is falsy, the code in the `else` block runs, and `We don't have to buy bananas!` gets logged.

#### Q12:What's the output?

```js
const emojis = ['🥑', ['✨', '✨', ['🍕', '🍕']]];

console.log(emojis.flat(1)); 
```

- A: `['🥑', ['✨', '✨', ['🍕', '🍕']]]`
- B: `['🥑', '✨', '✨', ['🍕', '🍕']]`
- C: `['🥑', ['✨', '✨', '🍕', '🍕']]`
- D: `['🥑', '✨', '✨', '🍕', '🍕']`

**Answer**:

Answer: B

With the `flat` method, we can create a new,  flattened array. The depth of the flattened array depends on the value  that we pass. In this case, we passed the value `1` (which we didn't have to, that's the default value), meaning that only the arrays on the first depth will be concatenated. `['🥑']` and `['✨', '✨', ['🍕', '🍕']]` in this case. Concatenating these two arrays results in `['🥑', '✨', '✨', ['🍕', '🍕']]`.

#### Q13:Which of the options result(s) in an error?

```js
const emojis = ['🎄', '🎅🏼', '🎁', '⭐'];

/* 1 */ emojis.push('🦌');
/* 2 */ emojis.splice(0, 2);
/* 3 */ emojis = [...emojis, '🥂'];
/* 4 */ emojis.length = 0;
```

- A: 1
- B: 1 and 2
- C: 3 and 4
- D: 3

**Answer**:

Answer: D

The `const` keyword simply means we cannot *redeclare* the value of that variable, it's *read-only*. However, the value itself isn't immutable. The properties on the `emojis` array can be modified, for example by pushing new values, splicing them, or setting the length of the array to 0.

#### Q14:What's the output?

```js
const fruit = ['🍌', '🍊', '🍎']

fruit.slice(0, 1)
fruit.splice(0, 1)
fruit.unshift('🍇')

console.log(fruit)
```

- A: `['🍌', '🍊', '🍎']`
- B: `['🍊', '🍎']`
- C: `['🍇', '🍊', '🍎']`
- D: `['🍇', '🍌', '🍊', '🍎']`

**Answer**:

Answer: C

First, we invoke the `slice` method on the  fruit array. The slice method does not modify the original array, but  returns the value that it sliced off the array: the banana emoji. Then, we invoke the `splice` method on the fruit array. The splice method does modify the original array, which means that the fruit array now consists of `['🍊', '🍎']`. At last, we invoke the `unshift` method on the `fruit` array, which modifies the original array by adding the provided value,  ‘🍇’ in this case,  as the first element in the array.  The fruit array  now consists of `['🍇', '🍊', '🍎']`.

#### Q15:**What will be the output**

```js
let arr = [1, 2, 3, 4, 5, -6, 7];
arr.length = 0;
console.log(arr);
```

**Answer**:

- **Output** : [ ]
- **Reason** : The length of the array has been set to 0, so the array becomes empty.

#### Q16:**What will be the output**

```js
console.log([11, 2, 31] + [4, 5, 6]);
```

**Answer**:

- **Output** : "11,2,314,5,6"
- **Reason** : The + operator is used for both addition and string concatenation. When you try to concatenate two arrays using the +  operator, the arrays are converted to strings and then concatenated  together. In this case, the arrays [11, 2, 31] and [4, 5, 6] are  converted to strings as "11,2,31" and "4,5,6" respectively. Then, the  two strings are concatenated, resulting in "11,2,314,5,6".

#### Q17**What will be the output**

```js
console.log('apple'.split(''));
```

**Answer**:

- **Output** : [ 'a', 'p', 'p', 'l', 'e' ]
- **Reason** : split method is used to split a string into an array of substrings based on a specified separator. 

#### Q18:**What will be the output**

```js
const arr = [2,3,5,2,8,10,5];
console.log(arr.indexOf(5))
```

**Answer**:

- **Output** : 2
- **Reason** : indexOf method returns the index of the first occurrence of the specified element in the array. 

#### Q19:**What will be the output**

```js
const array = [8, 18, 28, 38];
const result = array.map(element => element + 2)
               .filter((element) => element > 25);
console.log(result);
```

**Answer**:

- **Output** : [ 30, 40 ]
- **Reason** : The code increments each element in the array by 2 using map and filters out elements greater than 25 using filter.

#### Q20:**What will be the output**

```js
function checkValue(value){
    var result = Array.isArray(value);
    console.log(result);
}
checkValue([1,2,3]);
```

**Answer**:

- **Output** : true
- **Reason** : Array.isArray() method is used to check if the provided value is an array.

#### Q21:**What will be the output**

```js
const arr = [10, -1, 2];
arr.sort((a, b) => a - b);
console.log(arr);
```

**Answer**:

- **Output** : [-1, 2, 10]
- **Reason** : The compare function (a, b) => a - b sorts the numbers numerically in ascending order.

#### Q22:**What will be the output**

```js
const arr = [11, 0, '', false, 2, 1];
const filtered = arr.filter(Boolean);
console.log(filtered);
```

**Answer**:

- **Output** : [11, 2, 1]
- **Reason** : filter(Boolean) removes all falsy values (0, ""  (empty string), false, null, undefined, and NaN) from the array and  keeps truthy ones.
