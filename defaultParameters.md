# Default parameters

## Default values

Old way of checking parameters and setting a default value:

```
const printFrequency = (value, unit) => {
  if (typeof unit === "undefined") {
    unit = "Hz";
  }

  console.log(value + " " + unit);
}
```

New way with default parameters:

```
const printFrequency = (value, unit = "Hz") => {
  console.log(value + " " + unit);
}
```

Both functions can be called like this:

```
printFrequency(120);  // the second parameter is not specified = undefined
printFrequency(130, "Hz");
printFrequency(14, "kHz")
```

## Advanced: Last parameters should have default values

Typically, default values are defined for the last parameters in the function.

```
const someDefault(x, y = 1, z) {
  console.log(x, y, z);
}

someDefault();        // prints: undefined, 1, undefined
someDefault(3);       // prints: 3, 1, undefined
someDefault(4, 5);    // prints: 4, 5, undefined
someDefault(7, 8, 9); // prints: 7, 8, 9
```

There is no way to specify only x and z during the function call.
