# Arrow Functions

## Arrow functions = new way to define a function

Old way to define a function:
```
function func1(param1, param2) {
  console.log("From func 1", param1, param2);
  return 1;
}
```

New way to define a function:
```
const func2 = (param1, param2) => {
  console.log("From func 2", param1, param2);
  return 2;
};
```

Both ways are (almost) the same.

Best practices:
- Use arrow functions when creating functions in classes and React components.


## One-line arrow functions don't need block { }

Complicated syntax:
```
const plus = (a, b) => {
  return a + b;
}
```

Simple syntax:
```
const plus = (a, b) => a + b;
```

## Single parameter doesn't need to be in brackets

With brackets:
```
const power = (num) => num * num;
```

Without brackets:
```
const power = num => num * num;
```

Both ways are correct and the functionality is the same.

Use http://prettier.io to maintain consistent behavior.

## Advanced: Ternary operator can help to make a function syntax simpler

Older, more complicated syntax:
```
function divideOld(a, b) {
  if (b !== 0) {
    return a / b;
  } else {
    return NaN;
  }
}
```

New, simpler syntax (with ternary operator):
```
const divideNew = (a, b) => b !== 0 ? a / b : NaN;
```

## Advanced: It is possible to "chain" functions

E.g. Function that returns another function:

Old way:
```
function generalFunc(greeting) {
  return function inner(name) {
    return greeting + " " + name;
  }
}
```

New way:
```
const generalFunc = (greeting) => (name) => greeting + " " + name;

console.log(generalFunc("Bye")("Marek")); // prints: Bye Marek
```

It can also be used like this:
```
const hiFunc = generalFunc("Hi");
console.log(hiFunc("Radka")); // prints: Hi Radka
console.log(hiFunc("Misa")); // prints: Hi Misa

const helloFunc = generalFunc("Hello");
console.log(helloFunc("Jiri")); // prints: Hello Jiri
```

## Advanced: Non-arrow functions do not bind automatically "this" property

Non-arrow function must be `bind` explicitly:
```
class MyClass {
  constructor(name) {
    this.name = name;
    this.getName = this.getName.bind(this); // try comment this line
  }

  getName() {
    console.log("Name is", this.name);
  }
}

const jakub = new MyClass("Jakub");
jakub.getName();

const dan = new MyClass("Dan");
dan.getName();

const getNameDan = dan.getName;
getNameDan();  // if bind is not present: TypeError: Cannot read property 'name' of undefined
```

Arrow functions do the binding implicitly:
```
class MyClass {
  constructor(name) {
    this.name = name;
    // no explicit binding here
  }

  getName = () => {
    console.log("Name is", this.name);
  };
}

const jakub = new MyClass("Jakub");
jakub.getName();

const dan = new MyClass("Dan");
dan.getName();

const getNameDan = dan.getName;
getNameDan(); // it just works

```
