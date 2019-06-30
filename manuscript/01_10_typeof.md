## The typeof operator

In some cases, we may want to check the type of a value we hold in a variable. To perform this task, we will introduce the typeof operator.

Let's recall the concept of an *operator* and an *operand*:

A> We perform *operations* on data of given type. These operations are symbolized by an *operator* such as `+`, `-`, `*`, `/`. The data we perform operations on are called the *operands* of the operation.

For instance, in the `2 * 3` operation, the multiplication sign (`*`) is the operator, and the operands are `2` and `3`.

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

Regarding the `null` value, a simple comparison does the trick:

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

### Exercises - typeof operator

**Exercise 39**: Without executing the code, determine the values of the following variables:

```
let a = typeof '';
let b = typeof a;
let c = typeof x;
let d = typeof 25;
let e = typeof null;
let f = typeof 25 + ' ';
let g = typeof (NaN === NaN);
let h = typeof null;
let i = '' + 1;
let j = typeof i;
```
