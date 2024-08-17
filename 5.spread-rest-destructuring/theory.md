## Theory on destructuring

#### Q1:What will be the output ? 

```js
const [firstName, lastName, town] = ["Suvadeep", "Mukherjee", "Khatra"];

console.log(firstName, lastName, town);
```

**Answer**:

The output will be `"Suvadeep","Mukherjee","Khatra"`

#### Q2:What will be the output ? 

```js
const [firstName, ...otherInfo] = ["Suvadeep", "Mukherjee", "Khatra"];

console.log(firstName, otherInfo);
```

**Answer**:

The output will be ` Suvadeep [ 'Mukherjee', 'Khatra' ]` 

#### Q3:What will be the output ? 

```js
const [, , town] = ["Suvadeep", "Mukherjee", "Khatra"];

console.log(town);
```

**Answer**:

The output will be `Khatra`

#### Q4:What will be the output ? 

```js
const [firstName = "Sovon", town = "Khatra"] = ["Suvadeep"];

console.log(firstName, town);
```

**Answer**:

The output will be `Suvadeep Khatra`

#### Q5:What will be the output ? 

```js
let firstName = "Suvadeep";

let lastName = "Mukherjee";

[firstName, lastName] = [lastName, firstName];

console.log(firstName, lastName);
```

**Answer**:

The output will be `Mukherjee Suvadeep`

###### Q6:What will be the  output  ? 

```js
const profile = ["Suavdeep", "Mukherjee"];

function getUserBio([firstName, lastName]) {

  return `My name is ${firstName} ${lastName}.`;

}

console.log(getUserBio(profile));
```

**Answer**:

The output will be : `My name is Suavdeep Mukherjee.`

#### Q7:What will be the output ? 

```js
const profile = ["Khatra", "Male", ["Suvadeep", "Mukherjee"]];

function getUserBio([town, , [userName]]) {

  return `${userName} lives in ${town}`;

}

console.log(getUserBio(profile));
```

**Answer**:

The output will be `Suvadeep lives in Khatra`

#### Q8:What will it return ? 

```js
function getUserBio([firstName] = []) {
  console.log(
    "Do something else that does not need the destructuring parameter."
  );
  return `My name is ${firstName}.`;
}
```

**Answer**:

It will return `My name is undefined`

#### Q9:What will be logged to the console ? 

```js
const {

  firstName: fName,

  lastName: lname,

  town: village,

} = {

  firstName: "Suvadeep",

  lastName: "Mukherjee",

  town: "khatra",

};

console.log(fName, lname, village);
```

**Answer**:

The output will be `Suvadeep Mukherjee khatra`

#### Q10:What will be logged to the console ? 

```js
const { firstName, lastName, town } = {

  firstName: "Suvadeep",

  lastName: "Mukherjee",

  town: "Khatra",

};

console.log(firstName, lastName, town);
```

**Answer**:

The output will be `Suvadeep Mukherjee Khatra`

