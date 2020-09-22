# Spread operator



## Definition and simple example

Used to expand iterable object (e.g. array) to series of arguments.

Example - without spread operator:

```
const sum = (x, y, z) => x + y + z;
const numbers = [1, 2, 3];

const result = sum(numbers[0], numbers[1], numbers[2]);
```

With spread operator:

```
const sum = (x, y, z) => x + y + z;
const numbers = [1, 2, 3];

const result = sum(...numbers);
```

Notice that the whole array (iterable object = `[1, 2, 3]`) is converted into a set of function arguments: `1, 2, 3`.



## Typical usage

### 1. To provide function arguments:

```
const numbers = [1, 2, 3];

result = sum(...numbers);
```

### 2. To define array:

```
const numbers = [1, 2, 3];

const arr = [...numbers];
```

Equivalent to:

```
const arr = [1, 2, 3];
```

### 3. To define object:

```
const obj = {
  a: "a",
  b: 123
};

const cloned = { ...obj };
```

It creates a (shallow) copy of the object (defined in ES2018).



## Advanced: You can use spread operator inside a "normal" definition

Example:

```
const arr3456 = [3, 4, 5, 6];

const arr9 = [1, 2, ...arr3456, 7, 8, 9];

console.log(arr9); // prints: [1, 2, 3, 4, 5, 6, 7, 8, 9];
```



## Advanced: It is easy to change value of existing field(s)

Ordinary JavaScript behavior:

```
const obj = {
  name: "Bond",
  number: 7,
  name: "James Bond", // name field specified again
}

console.log(obj.name); // prints: James Bond
```

When used with spread operator:

```
const oldObj = {
  name: "Bond",
  number: 7,
};

const newObj = {
  ...oldObj,
  name: "James Bond",
};

console.log(newObj.name); // prints: James Bond
```

## Advanced: Order is important

It is executed from left to right.

This doesn't do anything:

```
const orig = {
  character: "Dilbert",
};

const copy = {
  character: "Pointy Haired Boss",
  ...orig
};

console.log(copy);  // prints: { character: "Dilbert" }
```


## Advanced: You can remove fields

You can even use spread operator to remove some fields from the original object:

```
const name = {
  first: "Arthur",
  middle: "Conan",
  last: "Doyle",
};

const { middle, ...nameWithoutMiddle } = name;

console.log(nameWithoutMiddle); // prints: { first: "Arthur", last: "Doyle" }
```

Two variables are "extracted" from the `name` variable. The variable `nameWithoutMiddle` contains all fields from the original variable with the exception of already extracted fields, i.e. the `middle` variable.



## Advanced: Only shallow copy of the object is created

Spread operator only copies "first-level" objects, it doesn't deep copy the whole structure.

Example:

```
const orig = {
  num: 123,
  arr: [7, 8],
};

const clone = { ...orig };

orig.num = 444;
orig.arr[0] = 99;

console.log(orig); // { num: 444, arr: [ 99, 8 ] }
console.log(clone); // { num: 123, arr: [ 99, 8 ]}
```

As you can see, `clone.num` remains 123 even after it is changed in `orig`. However, when `orig.arr[0]` is changed, the `clone.arr[0]` is changed as well. It is because both `arr` references point to the same block of memory, i.e. shallow copy has been used.

If you want to deep-copy this object, you can do it e.g. like this:

```
const orig = {
  num: 123,
  arr: [7, 8],
};

const clone = { ...orig, arr: [...orig.arr] };

console.log(orig); // { num: 444, arr: [ 99, 8 ] }
console.log(clone); // { num: 123, arr: [ 7, 8 ]}
```

This way, first the whole `orig` object is cloned and then the `arr` item is cloned independently. Note the number `7` in the output of the last console.log.

The disadvantage of this approach is that you need to know structure and types of the object.

Another possible solution is to use an external library, e.g. lodash method `cloneDeep` :-)
