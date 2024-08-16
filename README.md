

# JavaScript-Output-based-Interview-Questions

**1. What will be the output**

```js
let arr = [1, 2, 3, 4, 5, -6, 7];
arr.length = 0;
console.log(arr);
```

**Answer**: 

<ul>	
	<li><b>Output</b> : [ ]</li>
	<li><b>Reason</b> : The length of the array has been set to 0, so the array becomes empty.</li>
</ul>



**2. What will be the output**

```js
x = 10;
console.log(x);
var x;    
```

**Answer**:

- **Output** : 10
- **Reason** : The declaration of the variable x is hoisted to the top of its scope.

**3. What will be the output**

```js
let a = { x: 1, y: 2 }
let b = a;
b.x = 3;
console.log(a);
console.log(b);
```

**Answer**: 

- **Output** : { x: 3, y: 2 } { x: 3, y: 2 }
- **Reason** : 'a' and 'b' both are pointing to the same reference.

**4. What will be the output**

```js
for(var i = 0; i < 10; i++){
    setTimeout(function(){
      console.log("value is " + i);
  })
}
```

**Answer**:

- **Output** : 10 times, "value is 10"
- **Reason** : "var" has a function scope, and there will be only  one shared binding for the iterations. By the time the setTimeout  function gets executed, the for loop has already completed and the value of the variable i is 10.

**5. What will be the output **

**Answer**:

- **Output** : 10 times "value is" followed by the value of i in each iteration, from 0 to 9
- **Reason** : "let" has a block scope, and a new binding will be  created for each iteration. Here, a new variable i is created and has a  different value for each iteration of the loop.
