## Questions on this keyword

#### Q1:What's the output?

```js
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

- A: `20` and `62.83185307179586`
- B: `20` and `NaN`
- C: `20` and `63`
- D: `NaN` and `63`

**Answer**:Answer: B

Note that the value of `diameter` is a regular function, whereas the value of `perimeter` is an arrow function.

With arrow functions, the `this` keyword refers to its current surrounding scope, unlike regular functions! This means that when we call `perimeter`, it doesn't refer to the shape object, but to its surrounding scope (window for example).

Since there is no value `radius` in the scope of the arrow function, `this.radius` returns `undefined` which, when multiplied by `2 * Math.PI`, results in `NaN`.

#### Q2:What is the output?

```js
var status = '😎';

setTimeout(() => {
  const status = '😍';

  const data = {
    status: '🥑',
    getStatus() {
      return this.status;
    },
  };

  console.log(data.getStatus());
  console.log(data.getStatus.call(this));
}, 0);
```

- A: `"🥑"` and `"😍"`
- B: `"🥑"` and `"😎"`
- C: `"😍"` and `"😎"`
- D: `"😎"` and `"😎"`

**Answer**:

Answer: B

The value of the `this` keyword is dependent on where you use it. In a **method**, like the `getStatus` method, the `this` keyword refers to *the object that the method belongs to*. The method belongs to the `data` object, so `this` refers to the `data` object. When we log `this.status`, the `status` property on the `data` object gets logged, which is `"🥑"`.

With the `call` method, we can change the object to which the `this` keyword refers. In **functions**, the `this` keyword refers to the *the object that the function belongs to*. We declared the `setTimeout` function on the *global object*, so within the `setTimeout` function, the `this` keyword refers to the *global object*. On the global object, there is a variable called *status* with the value of `"😎"`. When logging `this.status`, `"😎"` gets logged.

#### Q3:What's the output?

```js
const person = {
  firstName: 'Lydia',
  lastName: 'Hallie',
  pet: {
    name: 'Mara',
    breed: 'Dutch Tulip Hound',
  },
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  },
};

console.log(person.pet?.name);
console.log(person.pet?.family?.name);
console.log(person.getFullName?.());
console.log(member.getLastName?.());
```

- A: `undefined` `undefined` `undefined` `undefined`
- B: `Mara` `undefined` `Lydia Hallie` `ReferenceError`
- C: `Mara` `null` `Lydia Hallie` `null`
- D: `null` `ReferenceError` `null` `ReferenceError`

**Answer**:

Answer: B

With the optional chaining operator `?.`, we no longer have to explicitly check whether the deeper nested values are  valid or not. If we're trying to access a property on an `undefined` or `null` value (*nullish*), the expression short-circuits and returns `undefined`.

`person.pet?.name`: `person` has a property named `pet`: `person.pet` is not nullish. It has a property called `name`, and returns `Mara`. `person.pet?.family?.name`: `person` has a property named `pet`: `person.pet` is not nullish. `pet` does *not* have a property called `family`, `person.pet.family` is nullish. The expression returns `undefined`. `person.getFullName?.()`: `person` has a property named `getFullName`: `person.getFullName()` is not nullish and can get invoked, which returns `Lydia Hallie`. `member.getLastName?.()`: variable `member` is non-existent therefore a `ReferenceError` gets thrown!

#### Q4:What's the output?

```js
const user = {
	email: "my@email.com",
	updateEmail: email => {
		this.email = email
	}
}

user.updateEmail("new@email.com")
console.log(user.email)
```

- A: `my@email.com`
- B: `new@email.com`
- C: `undefined`
- D: `ReferenceError`

**Answer**:

Answer: A

The `updateEmail` function is an arrow function, and is not bound to the `user` object. This means that the `this` keyword is not referring to the `user` object, but refers to  the global scope in this case. The value of `email` within the `user` object does not get updated. When logging the value of `user.email`, the original value of `my@email.com` gets returned.