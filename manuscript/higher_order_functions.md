## Higher order functions

In this section, you will learn about higher order functions. An important cornerstone of functional programming is higher order functions. If you want to write programs in mostly functional style, it is inevitable that you master the basics of higher order functions. 

First, you will learn the simple definition of higher order functions. 

I will make sure you remember the definition by showing you some higher order functions you may already be using.

We will conclude this article by implementing a higher order function example.


### What are higher order functions?

> Higher order functions are functions that accept function arguments or return a function.

The or in this definition is not in an exclusive sense.

We learned in the previous section that JavaScript functions are values. Therefore, functions can be passed to other functions, and they can also be return values of functions.

This is all the theory you need to understand higher order functions. The name *higher order function* seems scary at first, but there is really nothing scary about it: we just pass functions as arguments or return them as return values.

Note that you may know many higher order functions already, especially if you went through my JavaScript mini course.

```
setTimeout( () => console.log('done'), 1000 );
```

[ninja-inline id="542"]

A great example for higher order functions is setTimeout. The first argument of `setTimeout` is a function, so `setTimeout` is a higher order function.

```
document.querySelector( '.js-submit' )
   .addEventListener( 'click', submitCallback );
```

When adding events to a DOM node, the function registering the event is a higher order function.

Both `setTimeout` and `addEventListener` are higher order functions, because they have function arguments. Let's now see an example that returns a function.

Context binding returns a function with a bound `this` value. Therefore, `bind` is a higher order function.

```
const area = function() {
    return this.width * this.height;
};

const boundArea = area.bind( { width: 2, height: 3 } );

boundArea();
```

Technically, `bind` is a method of the `area` object through the prototype chain inheritance. We can always rewrite method calls in a form, where `bind` is a standalone function, and `area` is an argument:

```
const bind = function( f, ...args ) {
    return f.bind( ...args );
}

const boundArea = bind( area, { width: 2, height: 3 } );
```

After the rewrite, we can clearly see that `bind` not only accepts a function argument, but it also returns a function.


### Writing higher order functions

We may also want to write a higher order function ourself to demonstrate its usage.

Suppose that your task is to format integer values representing cents to currencies. The request includes some customization, such as specifying the currency symbol, and the decimal separator.

If the *template literal* return value is not familiar to you, read my article on [strings and template literals](http://www.zsoltnagy.eu/strings-and-template-literals-in-es6/).

```
const formatCurrency = function( 
    currencySymbol,
    decimalSeparator  ) {
    return function( value ) {
        const wholePart = Math.trunc( value / 100 );
        let fractionalPart = value % 100;
        if ( fractionalPart < 10 ) {
            fractionalPart = '0' + fractionalPart;
        }
        return `${currencySymbol}${wholePart}${decimalSeparator}${fractionalPart}`;
    }
}

> getLabel = formatCurrency( '$', '.' );

> getLabel( 1999 )
"$19.99"

> getLabel( 2499 )
"$24.99"
```

`formatCurrency` returns a function with a fixed currency symbol and decimal separator. 

We pass the formatter a value, then format this value by extracting its whole part and the fractional part. Notice that I used the ES6 math extension *trunc* to truncate the result. 

The return value of this function is constructed by a template literal, concatenating the currency symbol, the whole part, the decimal separator, and the fractional part.

The currency symbol and the decimal separator are not passed to the returned function, they are fixed values.

We can pass integer values to the `getLabel` function, and we get a formatted representation back.

Therefore, the `formatCurrency` higher order function returned a usable formatter function. 


### The undesirable forEach and map-reduce-filter

Some higher order functions are useful for handling arrays in JavaScript. In fact, when writing code in mostly functional style, we often use these functions instead of loops. These functions are:

- `map`,
- `reduce`,
- `filter`.

You may rightfully ask, why I haven't mentioned the `forEach` method? After all, we are talking about loops, aren't we?

The problem with `forEach` is that it is a completely useless function in functional programming. When writing code in purely functional style, it makes no sense using `forEach`. Let's see a simple example:

```
const values = [1, 2, 3, 3, 5];
let sum = 0;

values.forEach( v => { sum += v; } );

console.log( sum );
```

The `forEach` helper iterates over `values` and calls its first argument on each value in the array. The main effect of this `forEach` call is that `undefined` is returned. From this perspective, it does not matter what is in the function body. When we execute the function body `sum += v`, a *side-effect* is created, modifying the context outside the scope of the `forEach` helper.

Pure functional programming is *side-effect free*. The `forEach` helper of arrays does not return any usable value. Therefore, the only reason to use `forEach` is to rely on side-effects inside the callback of `forEach`.

> In tech interviews, I often look puzzled when candidates declare that they are going to use functional programming, so instead of the `for` loop, they use a `forEach` helper. Don't walk into this trap.

There are better functions to manipulate arrays.

You can achieve the same result with `reduce`:

```
const values = [1, 2, 3, 3, 5];
const sum = values.reduce( (accumulator, v) => accumulator + v, 0 );
console.log( sum ); // 14
```

Reduce is a higher order function with a function argument. This function argument is executed on each element of the array. It takes an accumulator variable and one value from the array. The return value of this function argument is the new value of the accumulator. This new value will be used in the next call belonging to the next element.

Let's print the state of the accumulator variable and the upcoming array value in each iteration:

```
const values = [1, 2, 3, 3, 5];
const sum = values.reduce( (accumulator, v) => {
    const result = accumulator + v;
    console.log( `accumulator, v, result: ${ accumulator }, ${ v }, ${ result }` );
    return result;
}, 0 );
```

The following values are printed to the console:

```
accumulator, v, result: 0, 1, 1
accumulator, v, result: 1, 2, 3
accumulator, v, result: 3, 3, 6
accumulator, v, result: 6, 3, 9
accumulator, v, result: 9, 5, 14
```

That's all you need to know about reduce. You will soon get an exercise, where you will be able to use it in practice.

Our next function is `map`. Map is a higher order function that takes each element of an array, transforms it using a callback function, and returns an array of the transformed values. 

For instance, we can get different powers of `2` using the following expression:

```
> [0, 1, 2, 3, 4].map( v => 2 ** v );
[1, 2, 4, 8, 16]
```

Remember, the `**` is the exponential operator introduced in `ES2016`. Read `2 ** v` as "two to the power of v".

Let's now construct the first 50 powers of `2`. Assuming that we don't want to construct an array of 51 elements by hand, we could just take an array with `null` elements:

```
new Array( 51 ).fill( null )
```

The `map` function's callback may accept a second argument, which is the index of the current element of the array:

```
> new Array( 51 ).fill( null ).map( (item, index) => index )
(51) [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]
```

We just have one step left: instead of returning `index`, we need to return `2 ** index`.

```
> new Array( 51 ).fill( null ).map( (item, index) => 2 ** index )
(51) [1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576, 2097152, 4194304, 8388608, 16777216, 33554432, 67108864, 134217728, 268435456, 536870912, 1073741824, 2147483648, 4294967296, 8589934592, 17179869184, 34359738368, 68719476736, 137438953472, 274877906944, 549755813888, 1099511627776, 2199023255552, 4398046511104, 8796093022208, 17592186044416, 35184372088832, 70368744177664, 140737488355328, 281474976710656, 562949953421312, 1125899906842624]
```

I have some software developer friends who know at least the first 20 values by heart. They would still use `map` to create this array though, because it's faster than writing these digits down.

The third higher order array function is `filter`. We may want to throw away some elements from an array and return an array that only keeps the rest of the elements.

For instance, suppose we want to throw away all the negative elements from an array:

```
> [-1, 5, 2, -4, -2, 2].filter( v => v >= 0);
[5, 2, 2]
```

`array.filter( f )` keeps those elements in filter for which `f( element )` returns a truthy value.

If you don't know what a truthy value is, check out [this article](http://www.zsoltnagy.eu/javascript-tutorial-for-absolute-beginners/).

### Chaining map-reduce-filter

Map and filter return arrays.

Map, reduce, and filter operate on arrays.

Therefore, we can chain any sequence of map and filter calls after each other, and we may even place a reduce call at the end.

For instance, suppose you have an array of strings, and you are interested in finding the length of the longest string that starts with `a`.

We can find the solution using the following steps:

1. Filter the elements that don't start with `a`.
2. Map the elements to their lengths.
3. Reduce these lengths to their maximum.

```
const words = ['ab', 'abc', 'bcde'];

words
    .filter( w => w.startsWith( a ) )
    .map( w => w.length )
    .reduce( (acc, v) => Math.max( acc, v ), 0 );
```

Side note: technically, we don't need to use reduce to take the maximum of an array. We could have just written:

```
Math.max( ...wordLengths );
```

If you are ready for more, read [this blog post](http://www.zsoltnagy.eu/translating-sql-queries-using-map-reduce-filter-in-javascript/) for a map-reduce-filter exercise. You will have to translate an SQL statement to map-reduce-filter calls.

### Summary

Higher order functions are functions that accept a function argument or return a function.

You may be using many higher order functions already, possibly without thinking about them. Just think about `setTimeout`, event listener callbacks, or the `bind` function.

Some higher order functions such as `map`, `reduce`, and `filter` help you process arrays easier.
