## Questions on Strings

###### What's the output?

```js
const name = 'Lydia Hallie';
console.log(name.padStart(13));
console.log(name.padStart(2));
```

A: `"Lydia Hallie"`, `"Lydia Hallie"`

B: `" Lydia Hallie"`, `" Lydia Hallie"` (`"[13x whitespace]Lydia Hallie"`, `"[2x whitespace]Lydia Hallie"`)

C: `" Lydia Hallie"`, `"Lydia Hallie"` (`"[1x whitespace]Lydia Hallie"`, `"Lydia Hallie"`)

**Answer**:

Answer: C

With the `padStart` method, we can add padding to the beginning of a string. The value passed to this method is the *total* length of the string together with the padding. The string `"Lydia Hallie"` has a length of `12`. `name.padStart(13)` inserts 1 space at the start of the string, because 12 + 1 is 13.

If the argument passed to the `padStart` method is smaller than the length of the array, no padding will be added.





###### What's the output?

```js
console.log('🥑' + '💻');
```



- A: `"🥑💻"`
- B: `257548`
- C: A string containing their code points
- D: Error

**Answer**:

Answer: A

With the `+` operator, you can concatenate strings. In this case, we are concatenating the string `"🥑"` with the string `"💻"`, resulting in `"🥑💻"`.