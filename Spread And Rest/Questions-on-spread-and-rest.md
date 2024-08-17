## Questions on Spread and Rest

###### What's the output?

```js
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

**Answer**:

Answer: C

The rest parameter (`...args`) lets us "collect" all remaining arguments into an array. An array is an object, so `ty![Screenshot 2024-08-16 at 10.45.27 PM](/Users/suvadeep/Desktop/Screenshot 2024-08-16 at 10.45.27 PM.png)peof args` returns `"object"`



###### What does this return?

```js
[...'Lydia'];
```

- A: `["L", "y", "d", "i", "a"]`
- B: `["Lydia"]`
- C: `[[], "Lydia"]`
- D: `[["L", "y", "d", "i", "a"]]`

**Answer**:

Answer: A

A string is an iterable. The spread operator maps every character of an iterable to one element.





###### What's the output?



```
const user = { name: 'Lydia', age: 21 };
const admin = { admin: true, ...user };

console.log(admin);
```

​    

- A: `{ admin: true, user: { name: "Lydia", age: 21 } }`
- B: `{ admin: true, name: "Lydia", age: 21 }`
- C: `{ admin: true, user: ["Lydia", 21] }`
- D: `{ admin: true }`

**Answer**:

Answer: B

It's possible to combine objects using the spread operator `...`. It lets you create copies of the key/value pairs of one object, and add them to another object. In this case, we create copies of the `user` object, and add them to the `admin` object. The `admin` object now contains the copied key/value pairs, which results in `{ admin: true, name: "Lydia", age: 21 }`.



###### What's the output?

```js
function getItems(fruitList, ...args, favoriteFruit) {
  return [...fruitList, ...args, favoriteFruit]
}

getItems(["banana", "apple"], "pear", "orange")
```

- A: `["banana", "apple", "pear", "orange"]`
- B: `[["banana", "apple"], "pear", "orange"]`
- C: `["banana", "apple", ["pear"], "orange"]`
- D: `SyntaxError`

**Answer**:

Answer: D

`...args` is a rest parameter. The rest parameter's value is an array containing all remaining arguments, **and can only be the last parameter**! In this example, the rest parameter was the second parameter. This is not possible, and will throw a syntax error.

```js
function getItems(fruitList, favoriteFruit, ...args) {
  return [...fruitList, ...args, favoriteFruit];
}

getItems(['banana', 'apple'], 'pear', 'orange');
```

​    The above example works. This returns the array `[ 'banana', 'apple', 'orange', 'pear' ]`





###### Which of the following options will return `6`?

```js
function sumValues(x, y, z) {
  return x + y + z;
}
```

- A: `sumValues([...1, 2, 3])`
- B: `sumValues([...[1, 2, 3]])`
- C: `sumValues(...[1, 2, 3])`
- D: `sumValues([1, 2, 3])`

**Answer**:

Answer: C

With the spread operator `...`, we can *spread* iterables to individual elements. The `sumValues` function receives three arguments: `x`, `y` and `z`. `...[1, 2, 3]` will result in `1, 2, 3`, which we pass to the `sumValues` function.





**What will be the output**

```js
const arr1 = [1, 2, 3, 4];
const arr2 = [6, 7, 5];
const result = [...arr1, ...arr2];
console.log(result);
```

**Answer**:

- **Output** : [1, 2, 3, 4, 6, 7, 5]
- **Reason** : Spread operator (...) concatenates the two arrays into "result" array.

**What will be the output**

```js
const person1 = { name: 'xyz', age: 21 };
const person2 = { city: 'abc', ...person1 };
console.log(person2);
```

**Answer**:

- **Output** : { city: 'abc', name: 'xyz', age: 21 }
- **Reason** : Spread operator (...) copies all the properties from person1 into person2.