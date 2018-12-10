## The typeof operator

Congratulations! You now know the basic types of JavaScript. This is a perfect time to introduce an operator that returns the type of a value.

The `typeof` operator accepts one operand and returns a string. This string describes the type of an object.

```
typeof ''         // "string"
typeof 0          // "number"
typeof true       // "boolean"
typeof {}         // "object"
typeof []         // "object"
typeof null       // "object"
typeof undefined  // "undefined"
typeof Symbol()   // "symbol"
```

There is just one problem: arrays, objects, and the `null` value have the same type. It would be great if we could differentiate between them. Fortunately, ES6 solves the array problem:

```
> Array.isArray( [1, 2] )
true
> Array.isArray( {a: 1} )
false
```

Regarding the new value, a simple comparison does the trick:

```
let name = null;

> name === null
true
```

Functions have the type `"function"`:

```
function two() { return 2; }

typeof two
"function"
```
