## Array-Like Objects

In JavaScript, there are some objects that are not arrays, but they are like arrays. Some examples of these objects is the `arguments` object of functions:

```
function variableArguments() {
    return arguments;
}

const args = variableArguments( 1, 2, 3, 4 );

console.log( args )
// Arguments(4) [1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]
```

Array methods in array-like objects are not defined:

```
> args.map
undefined

> args.push
undefined
```

In old versions of JavaScript, before the spread operator was invented in ES6, this was the only way to write a variable number of arguments. In newer versions of JavaScript, the use of the `arguments` object is discouraged. Use rest parameters instead. In the below example, `args` is a real array:

```
function variableArguments2( ...args ) {
    return args;
}

const args2 = variableArguments2( 1, 2, 3, 4 );

console.log( args2 );
// [1, 2, 3, 4]
```

In general, an array-like object looks like the following:

```
const A = {
    0: 'value0',
    1: 'value1',
    length: 2
}
```

In this object, `A[1]` returns `value1`. `A.length` returns `2`.

Array-like objects are not real arrays, because they don't have some array properties and operations such as: `map`, `reduce`, `filter`, `slice`, `splice`,n`push`, `pop`, `append`, `concat`, `join` etc.

The reason why the above methods are not available for array-like objects is that they inherit from `Object.prototype`, not from `Array.prototype`. Proof:

```
A.constructor
ƒ Object() { [native code] }
B.constructor
ƒ Array() { [native code] }
``` 

Array-like objects can be converted to an array in many ways:

- `Array.from( args )`,
- `Object.values( args )`,
- `[...args]`.

Before ES6, due to using array-like objects, functional programming techniques such as currying were harder to understand. 

When using variable number of arguments, use rest parameters.

Remember, `Array.isArray` determines if a reference points at an array or an array-like object:

```
const A = {
    0: 'value0',
    1: 'value1',
    length: 2
}

Array.isArray( A );                // false
Array.isArray( Array.from( A ) );  // true
```
