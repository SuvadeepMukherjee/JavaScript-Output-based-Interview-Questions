## Questions on increment and decrement operators 

###### What's the output?

```js
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

- A: `1` `1` `2`
- B: `1` `2` `2`
- C: `0` `2` `2`
- D: `0` `1` `2`

**Answer**:

Answer: C

The **postfix** unary operator `++`:

1. Returns the value (this returns `0`)
2. Increments the value (number is now `1`)

The **prefix** unary operator `++`:

1. Increments the value (number is now `2`)
2. Returns the value (this returns `2`)

This returns `0 2 2`.



###### What's the output?

```js
let num = 10;

const increaseNumber = () => num++;
const increasePassedNumber = number => number++;

const num1 = increaseNumber();
const num2 = increasePassedNumber(num1);

console.log(num1);
console.log(num2);
```

- A: `10`, `10`
- B: `10`, `11`
- C: `11`, `11`
- D: `11`, `12`

**Answer**:

Answer: A

The unary operator `++` *first returns* the value of the operand, *then increments* the value of the operand. The value of `num1` is `10`, since the `increaseNumber` function first returns the value of `num`, which is `10`, and only increments the value of `num` afterward.

`num2` is `10`, since we passed `num1` to the `increasePassedNumber`. `number` is equal to `10`(the value of `num1`). Again, the unary operator `++` *first returns* the value of the operand, *then increments* the value of the operand. The value of `number` is `10`, so `num2` is equal to `10`.