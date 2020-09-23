# Destructuring

## Destructuring - simple example

Destructuring is a way to unpack values from array or object to variables.

Consider this object for the following examples:

```
const person = {
  first: "Forrest",
  middle: "Alexander",
  last: "Gump",
};
```

Old way to print the first name:
```
const first = person.first; // new variable "first" is defined and initialized
console.log("First name is", first);
```

New way (i.e. destructuring expression used) to print the first name:
```
const { first } = person;   // new variable "first" is defined and initialized
console.log("First name is", first);
```

OK, the new approach doesn't seem so much better in this simple example.



## Destructuring from array

We can do this:

```
const point = [11.2, 23.5, 67.89];

const [x, y, z] = point;  // 3 variables "x", "y", "z" defined and initialized

console.log("X =", x);
```


## More complex object

It is possible to unpack a value from a deeper level in an object:

```
const movie = {
  name: "Forrest Gump",
  year: 1994,
  producer: {
    name: {
      first: "Robert",
      middle: "Lee",
      last: "Zemeckis",
    },
  },
  mainCharacter: {
    name: {
      first: "Forrest",
      middle: "Alexander",
      last: "Gump",
    },
  },
};

const {
  producer: {
    name: { first, last },
  },
} = movie; // 2 variables "first" and "last" are defined and initialized

console.log(`Producer: ${first} ${last}`); // prints: Producer Robert Zemeckis
```


## Advanced: Renaming variables

Consider the same `movie` variable. But we would like to print both main character and producer names.
We cannot simply destructure them because it would create 2 duplicate `first` (and `last`) variables.

Fortunately, we can rename variables:

```
const movie = {
  name: "Forrest Gump",
  year: 1994,
  director: {
    name: {
      first: "Robert",
      middle: "Lee",
      last: "Zemeckis",
    },
  },
  mainCharacter: {
    name: {
      first: "Forrest",
      middle: "Alexander",
      last: "Gump",
    },
  },
};

const {
  name,
  director: {
    name: { first: directorFirst, last: directorLast },
  },
  mainCharacter: {
    name: { first: mainCharacterFirst, last: mainCharacterLast },
  },
} = movie;

console.log(`Movie: ${name}
Director: ${directorFirst} ${directorLast}
Main Character: ${mainCharacterFirst} ${mainCharacterLast}`);
```


## Advanced: Undefined items

If the item doesn't exist, `undefined` value is assigned. Which is fine:

```
const obj = {
  text: "Text Item"
};

const {name} = obj;

console.log(name); // prints: undefined
```

However, if we try to destructure an item from a deeper level of the object, the path to this item must exist, otherwise an error occurs:

```
const products = {
  electronics: {
    computer: "Commodore Amiga",
  },
};

const {
  electronics: { computer },
} = products;

console.log(computer); // prints: Commodore Amiga

const {
  sport: { shoes },
} = products;

console.log(shoes); // prints: Type Error: Cannot read property 'shoes' of undefined
```


## Advanced: Default values

It is possible to assign a default value to a new variable. It is assigned instead of `undefined`.

```
const zoo = {
  sector1: "elephant",
  sector2: "giraffe",
};

const { sector1 = "not found", sector7 = "not found" } = zoo;

console.log("Sector 1:", sector1); // prints: Sector 1: elephant
console.log("Sector 7:", sector7); // prints: Sector 7: not found
```


## Advanced: Easy way to exchange 2 variables

Define an array and destructure it in a different order:

```
let a = 1;
let b = 2;

[a, b] = [b, a];

console.log(a); // prints 2
```
