# Variable Declaration (var, let, const)

## Variables don't have types

Any type can be assigned to a variable:

```
let count = 0;
console.log(count);

count = 7; // the same variable
console.log(count);

count = "Pareto Principle";
console.log(count);
```

## Best Practices:
- Use `let` or `const`
- Don't use `var` or no declaration

Example:
```
let hi = "hi";    // ok
const pi = 3.14;  // ok

var myVar = 7;  // bad
anyVar = "aa";  // bad
```

## Variable can store a reference to a function

This is not probably surprising, variable can store a reference to a function:

```
function myFunc1() {
  console.log("From myFunc1");
}

function myFunc2() {
  console.log("From myFunc2");
}

myFunc1();  // prints: From myFunc1
myFunc2();  // prints: From myFunc2

let yourFunc = myFunc2;
yourFunc(); // prints: From myFunc2
```


## Advanced: Var - potential problems: hoisting

Variable defined using `var` can be used before its definition (it is called hoisting):

```
console.log(myVar); // prints: undefined

var myVar = [1, 2];

console.log(myVar); // prints: [1, 2]
```

It is not possible to do this with `let` or `const`:

```
console.log(myConst); // prints: ReferenceError: Cannot access 'myConst' before initialization

const myConst = 5;

console.log(myConst); // prints: 5
```


## Advanced: Var - potential problems: scope

Scope of variable defined using `var` is not unique. Note there are 2 variables `i` defined:

```
var i = 0;

for (var i = 0; i < 10; i++) {
  console.log(i);
}

console.log(i); // prints 10 !
```

When defined using `let`, 2 separate scopes are created:

```
let j = 0;

for (let j = 0; j < 10; j++) {
  console.log(j);
}

console.log(j); // prints 0
```

## Advanced: Content of constant array can be modified

Array is represented by a **reference**, i.e. when the array is constant, the reference cannot be changed.
However, the content of the array can be changed:

```
const arr = ["a", "b", "c"];

arr.push("d"); // ok

console.log(arr); // prints ["a", "b", "c", "d"]

arr = ["e", "f"]; // error
```
