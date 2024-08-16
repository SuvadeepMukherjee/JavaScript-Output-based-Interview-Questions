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





###### What's the output?

```js
console.log(String.raw`Hello\nworld`);
```

- A: `Hello world!`
- B: `Hello` 
     `world`
- C: `Hello\nworld`
- D: `Hello\n` 
      `world`

**Answer**:

Answer: C

`String.raw` returns a string where the escapes (`\n`, `\v`, `\t` etc.) are ignored! Backslashes can be an issue since you could end up with something like:

`const path = `C:\Documents\Projects\table.html``

Which would result in:

`"C:DocumentsProjects able.html"`

With `String.raw`, it would simply ignore the escape and print:

`C:\Documents\Projects\table.html`

In this case, the string is `Hello\nworld`, which gets logged.





###### What's the output?

```js
console.log('I want pizza'[0]);
```

- A: `"""`
- B: `"I"`
- C: `SyntaxError`
- D: `undefined`

**Answer**:

Answer: B

In order to get a character at a specific index of a  string, you can use bracket notation. The first character in the string  has index 0, and so on. In this case, we want to get the element with  index 0, the character `"I'`, which gets logged.

Note that this method is not supported in IE7 and below. In that case, use `.charAt()`.