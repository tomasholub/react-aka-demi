# Template literals


## Template literals can be used as ordinary strings

Old string definition:

```
console.log("That's the older way.");
console.log('You can use apostrofe too');
```

Using template literals:

```
console.log(`This is the new way.`);
```

## Multiline strings

Old way how to define string with several lines:

```
const a = "This is the first line\n" +
  "And this is the second line.\n" +
  "And third";
```

The new way using template literal:

```
const b = `This is the first line
And this is the second line.
And third`;
```

Note that we don't need to use `\\n`.

Also note that each space or tab character or is important, i.e. there is no space in front of the second and third line. As a result, indentation seems incorrect.


## Template literal can contain an expression

```
console.log(`3 * 5 = ${3 * 5}`);  // prints: 3 * 5 = 15
```

### It is often used to print variable values:

```
const a = 17;
console.log(`The current value is ${a}.`);  // prints: The current value is 17.
```

### Complicated strings can be constructed more elegantly:

Old way:

```
const greeting = "Hi";
const name = "Tomas";

console.log("I would like to say: " + greeting + ", " + name);
```

New way:

```
const greeting = "Hi";
const name = "Tomas";

console.log(`I would like to say: ${greeting}, ${name}`);
```

### Another example

```
const amount = 10;

console.log(`You have ${amount === 0 ? "no" : amount} coin${amount === 1 ? "" : "s"}.`);
```

The possible results are in the following table:

| amount | printed |
| ------ | ------- |
| 0 | You have no coins. |
| 1 | You have 1 coin. |
| 2 | You have 2 coins. |
| 3 | You have 3 coins. |
| etc. | ... |



## Advanced: Tagged templates

You can specify your own function to parse template literals.

It is e.g. used by "styled components".

Example:

```
let currentPerson = "Radim";
let currentGift = "dog";

const giveGift = (strings, person, gift) => {
  const str0 = strings[0]; // I would like to give
  const str1 = strings[1]; // a
  const str2 = strings[2]; // .

  if (person === "Tomáš") {
    return "Don't give anything to Tomáš, he doesn't deserve it."
  }

  return `${str0}${person}${str1}${gift}${str2}`;
}

const result = giveGift`I would like to give ${person} a ${gift}.`;

console.log(result); // prints: I would like to give Radim a dog.
```

Note how the "function" is being called, i.e. in front of the string literal.
