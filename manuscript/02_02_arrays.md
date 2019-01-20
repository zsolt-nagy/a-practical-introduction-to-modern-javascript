## Using Arrays in JavaScript

You have learned the basics of JavaScript arrays in the introductory section. We will now work on extending your knowledge by learning more features of arrays. These features are described as array methods. We will group these array features by use case:

- creating and deleting arrays
- checking if a variable contains an array
- convert an array to a string: the `toString` method,
- find the location of an element of an array: the `indexOf`, `lastIndexOf`, and `contains` methods,
- the `split` string method and the `join` array method,
- slicing: the `slice` and `splice` array methods,
- `map`, `reduce`, `filter`, `find`, `findIndex`,
- `every` and `some`,
- adding and removing single elements: `push`, `pop`, `shift`, `unshift`
- concatenating arrays: `concat`,
- sorting arrays: `sort`,
- reversing arrays: `reverse`.

### Creating arrays

The `new` operator can be used to create arrays. We can specify the length of the array that is to be created:

```
const A = new Array(5);
// [empty × 5]

A[0]
// undefined

A[999]
// undefined
```

The values of the newly created array are written as `empty`. When accessing an empty element, or accessing an element outside the boundaries of the array, we get `undefined`.

The need may arise to fill all values of an array with values. The fill array method does the trick:

```
A.fill( 'a' )
// ["a", "a", "a", "a", "a"]
```

The length of the array can be modified at any time. The `fill` method takes the length into consideration:

```
A.length = 3
A.fill( 'b' )
// ["b", "b", "b"]
```

If you want to fill your array with different values that depend on the index of the array, you can use the `map` method. You will learn about the `map` method soon. Until then, let me reveal one example, foreshadowing the capabilities of `map`.

**Example**: the correct syntax of creating an array containing 1000 numbers from `1` to `1000` is as follows:

```
const oneToThousand = 
    new Array( 1000 )
        .fill( null )
        .map( (element, index) => index+1 );
```

Explanation:
- we create an array of length `1000`.
- we have to fill this array with any value to indicate that these values can be accessed and transformed
- we take each element of the array, and replace it with their index, incremented by `1`.

### The toString method

The `toString` method applied on an array works as follows:

- `toString` transfers each element of the array to a string value,
- the stringified values are joined by a comma.

Examples:

```
> [1, 2].toString()
"1,2"

> [undefined, null, {}, [], 1, '', 's', NaN].toString()
",,[object Object],,1,,s,NaN"
```

The values `underfined`, `null`, `[]`, `''` become empty strings. The `NaN` value becomes `"NaN"`.

### Checking if a variable contains an array

Before ES2015, this was a hard exercise, because arrays have the type `"object"`, and the array check had to look for typical properties and operations of arrays. These checks were never 100% reliable.

Since ES2015, the `Array.isArray` method can be used:

```
const a = [];
const b = { 0: 'a', length: 1 };

Array.isArray( a );  // true
Array.isArray( b );  // false
```

### Splitting and joining

A string can be split into an array of substrings using the `split` method. The argument of `split` determines how splitting is performed:

```
const values = 'first,second,third';

values.split( ',' )
(3) ["first", "second", "third"]
```

The `join` method joins values together to form one string, and inserts a spearator in-between them:

```
["first", "second", "third"].join( ';' )
// returns "first;second;third"

[1, 2, 3, 4, 5].join( '---*---' )
// returns "1---*---2---*---3---*---4---*---5"

[1, 2, 3, 4, 5].join( ',' )
// returns "1,2,3,4,5"

[1, 2, 3, 4, 5].join()
// returns "1,2,3,4,5"
```

In the absence of an argument, `join` uses a comma to join the values of its array.

### The slice method

The `slice` method copies a *slice* of an array. The slice is specified by its arguments. Both arguments of `slice` are optional:

```
A.slice( begin, end )

// begin: the first index to be sliced
// end: the first index not to be sliced
```

Let's see some examples:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

arr.slice( 1, 3 );
// returns: ["b", "c"] (indices 1 and 2)

arr.slice( 1 );
// returns: ["b", "c", "d", "e"] (starting at index 1)

arr.slice( 5 );
// returns: [] (there are no elements at or above index 5)

arr.slice( 2, 2 );
// returns: [] (the second argument is not greater than the 
// first, which implies an empty slice)

arr.slice();
// returns: ["a", "b", "c", "d", "e"]
```

You may ask why `slice` can accept zero arguments. The answer lies in the nature of *shallow cloning*:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

const shallowClone = arr.slice();

shallowClone[1] = 'X';

console.log( shallowClone );
// returns: ["a", "X", "c", "d", "e"]

console.log( arr );
// returns: ["a", "b", "c", "d", "e"]
```

Shallow cloning creates a new array with different elements that have the same values.

During my tech interviews, I sometimes see the following erroneous solution:

```
const A = ['a', 'b', 'c', 'd', 'e'];

const B = A;

B[1] = 'X';

console.log( A );
// returns: ["a", "X", "c", "d", "e"]
```

Remember, `A` and `B` are *references* to the exact same array. You can reach the same values both from `A` and from `B`. Instead of `B = A`, some of my candidates should have written `B = A.slice()`.

You may ask the question, why can't we just call the *shallow copying* operation *cloning* or *copying*? The answer lies in how reference types are treated. Arrays and objects contain references. During shallow cloning, only these references are copied:

```
const A = [{value: 1}, {value: 2}];
const B = A.slice();
B[0] = {value: 'X'};
B[1].value = 'Y';

console.log( B )
// returns: [{value: 'X'}, {value: 'Y'}]

console.log( A )
// returns: [{value: '1'}, {value: 'Y'}]
```

During cloning, we would expect to keep the contents of `A` intact. However, `slice` only performs shallow cloning, which is cloning on top level only. Therefore, `B` was constructed with new references that were not in `A`, but these references point at the same objects `{value: 1}` and `{value: 2}`. As long as you redirect the references to new objects such as `{value: 'X'}`, there are no problems with shallow cloning. However, as soon as you want to access the contents inside these references, you can see that the actual object content is shared between `A` and `B`.

I wrote a full article on shallow and deep copying here: [Cloning Objects in JavaScript](http://www.zsoltnagy.eu/cloning-objects-in-javascript/).

### The splice method

The `splice` method is used to manipulate the contents of an array in place. You can add, remove, or modify elements using `splice`.

The `splice` array extension accepts a variable number of arguments:

```
A.splice( start, deleteCount, ...newItems )
```

- `start`: the index at which the change occurs
- `deleteCount`: the number of elements to remove starting at index `start`. If this argument is missing, all elements starting at `start` are deleted
- `...newItems`: a variable number of elements to be added to the array at position `start`.

Many JavaScript integrated development environments help you with the parametrization in case you forgot them. 

Return value: an array containing the deleted elements.

Side-effect: the original array is modified. Elements are deleted from and/or added to the array.

**Example 1**: remove all elements starting at index `2`:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

arr.splice( 2 ); // returns: ["c", "d", "e"]

console.log( arr )
// prints: [ 'a', 'b' ]
```

**Example 2**: remove the third and the fourth element of the array:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

arr.splice( 2, 2 ); // returns: ["c", "d"]

console.log( arr )
// prints: [ 'a', 'b', 'e' ]
```

**Example 3**: insert the elements `'X'` and `'Y'` after the third element of the array:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

arr.splice( 3, 0, 'X', 'Y' ); // returns: []

console.log( arr )
// prints: ["a", "b", "c", "X", "Y", "d", "e"]
``` 

**Example 4**: replace the second, third, and fourth elements of the array with `'B'`, `'C'`, `'D'`:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

arr.splice( 1, 3, 'B', 'C', 'D' ); // returns: ["b", "c", "d"]

console.log( arr )
// prints: ["a", "B", "C", "D", "e"]
```

**Example 5**: solve Examples 1-4 using the spread operator and destructuring, without mutating the original array. Create a different destructuring assignment for each solution:

```
const arr = ['a', 'b', 'c', 'd', 'e'];

// 1. remove all elements starting at index `2`
const [a1, b1] = arr;
const solution1 = [a1, b1];

// 2. remove the third and the fourth element of the array
const [a2, b2,,,e2] = arr;
const solution2 = [a2, b2, e2];  

// 3. insert 'X' and 'Y' after the third element of the array
const [a3, b3, c3, ...rest] = arr;
const solution3 = [a3, b3, c3, 'X', 'Y', ...rest];

// 4. replace the second, third, and fourth elements of the 
// array with `'B'`, `'C'`, `'D'`
const [a4,,,,e4] = arr;
const solution4 = [a4, 'B', 'C', 'D', e4];
```

Splice is useful when the array is large and you may have to modify elements of the array at a large index.

### indexOf, lastIndexOf, contains

Sometimes we may want to find the first or the last index of an element in an array:

```
const arr = [1, 2, 3, 2, 1];

arr.indexOf( 1 )      // returns 0
arr.lastIndexOf( 1 )  // returns 4
```

You can also examine the first index of an element that is greater than or equal to the second argument passed to `indexOf`:

```
arr.indexOf( 1, 0 )  // reutnrs 0
arr.indexOf( 1, 1 )  // returns 4
```

Similarly, you can retrieve the last index of an element that is smaller than or equal to the second argument passed to `lastIndexOf`:

```
arr.lastIndexOf( 1, 4 )   // returns 4
arr.lastIndexOf( 1, 3 )   // returns 0
```

Both `indexOf` and `lastIndexOf` returns `-1` if its first argument is not found in the array or array segment:

```
arr.indexOf( 1, 5 )  // returns -1
arr.lastIndexOf( 4 ) // returns -1
```

> Before ES2016, a typical use case for `indexOf` was to determine if an array *contains* a value. Since ES2016, this operation is performed using the more semantic `includes` method.

```
// ES2015 or earlier
if ( arr.indexOf( value ) !== -1 ) {
    // do something
} 

// since ES2016
if ( arr.includes( value ) ) {
    // do something
}
```

The `A.includes( value )` method returns:

- `true` if `value` is in `A`,
- `false` otherwise.


### Map, reduce, filter, find

This is an introductory section introducing some array methods that will be used later in the *Higher order functions* section of the functional programming chapter. The objective of this section is to define these functions.

Suppose an array `arr` is given with the value `[1, 2, 3, 4, 5]`.

Map takes each element of the array, and applies a function on them one by one. For instance, suppose we have a `times2` function that multiplies each element of the array by `2`:

```
const arr = [1, 2, 3, 4, 5];

function times2( input ) {
    return 2 * input;
}
```

The execution of `map` is as follows:

```
arr.map( times2 ) // becomes
[1, 2, 3, 4, 5].map( times2 )  // becomes:
[times2(1), times2(2), times2(3), times2(4), times2(5)] // becomes:
[2*1, 2*2, 2*3, 2*4, 2*5] // becomes:
[2, 4, 6, 8, 10]
```

As creating the `times2` function takes a lot of lines to write, it makes more sense to simply use an arrow function:

```
const arr = [1, 2, 3, 4, 5];
const result = arr.map( x => 2*x ); // returns [2, 4, 6, 8, 10]
```

The above expression is equivalent to defining the `times2` function and applying it on the array using `map`.

The `map` array extension accepts a function that may have two arguments, specifying the mapped element and its index:

```
const fruits = ['apple', 'pear', 'banana'];
const result = fruits.map( (item, index) => [index, item] );
// result becomes: [[0, 'apple'], [1, 'pear'], [2, 'banana']]
```

Note that the above result can also be described using the `entries` method:

```
const fruits = ['apple', 'pear', 'banana'];
const result = [...fruits.entries()];
```

You may ask why it is necessary to write `[...fruits.entries()]` instead of just `fruits.entries()`. The answer is, because `fruits.entries()` returns an array iterator that is also an iterable object. This iterable can be iterated using the spread operator, resulting in elements. The array brackets consume these values, resulting in an array. You don't have to understand these concepts at this stage, this is advanced JavaScript. If you are interested in the details, check out my article [ES6 Iterators and Generators](http://www.zsoltnagy.eu/es6-iterators-and-generators-in-practice/), and check out the [exercises](http://www.zsoltnagy.eu/es6-iterators-and-generators-6-exercises-and-solutions/) belonging to the article.

Similarly to `map`, `filter` also returns an array, but it uses a function that returns booleans. Suppose we have a function that returns `true` only for even numbers. The role of `filter` is to keep those elements of the array for which the function passed to it returns `true`:

```
const arr = [1, 2, 3, 4, 5];
arr.filter( x => x % 2 === 0 ) // returns [2, 4]
arr.filter( x => x % 2 !== 0 ) // returns [1, 3, 5]
```

The `find` method is a special case for `filter`: it returns the first element found.

```
const arr = [1, 2, 3, 4, 5];
arr.find( x => x % 2 === 0 ) // returns 2
```

Throughout my practice as a job interviewer, I have seen countless examples of trying to break out of the `forEach` helper method. It is not possible, because `forEach` does not terminate. Suppose we have the following code printing the first even value from `arr`:

```
const arr = [1, 2, 3, 4, 5];
for ( let i = 0; i < arr.length; ++i ) {
    if ( arr[i] % 2 === 0 ) {
        console.log( arr[i] );
        return;
    }
}
```

Some applicants I interviewed were obsessed with using the `forEach` helper claiming that they do *functional programming*. In reality, the following code is not only erroneous, but it has nothing to do with functional programming:

```
// WARNING! ERRONEOUS CODE!
const arr = [1, 2, 3, 4, 5];
arr.forEach( x => {
    if ( x % 2 === 0 ) {
        console.log( x );
        return;  // This statement only returns from the inner function
    }
});
```

The above code is not equivalent to the code with the `for` loop. This is because `forEach` executes its function argument on each member of the array, regardless of what this function argument returns.

My candidates were looking for the `find` method:

```
const arr = [1, 2, 3, 4, 5];
console.log( arr.find( x => x % 2 === 0 ) );  // prints 2
```

The function passed to `find` may contain a second argument, the index of the array:

```
const fruits = ['apple', 'pear', 'banana'];
fruits.find( (item, index) => index%2 === 0 );
// returns "apple"
```

The `findIndex` method works like `find`, except that instead of the item, it returns the index corresponding to the element found. 

```
const fruits = ['apple', 'pear', 'banana'];

fruits.findIndex( (item, index) => index%2 === 0 );
// returns 0

fruits.findIndex( x => x === 'banana' )
// returns 2
```

Reduce creates a value from an array, applying a function on it that accumulates a value. Instead of the arrow function notation, I will rather use the more verbose form for easier understandability:

```
const arr = [1, 2, 3, 4, 5];

const reducer = function( accumulator, value ) {
    console.log( 'accumulator: ', accumulator, 'value: ', value );
    return accumulator * value;
}
```

If you call `reduce` with just the `reducer` function as the only argument, `reduce` takes the first element of the array as an accumulator value, and it starts the reduction with the second element of the array:

```
console.log( arr.reduce( reducer ) )
accumulator:  1 value:  2
accumulator:  2 value:  3
accumulator:  6 value:  4
accumulator:  24 value:  5
120
```

You can also initialize the accumulator by passing a second argument to `reduce`:

```
console.log( arr.reduce( reducer, 1 ) )
accumulator:  1 value:  1
accumulator:  1 value:  2
accumulator:  2 value:  3
accumulator:  6 value:  4
accumulator:  24 value:  5
120
```

The reduction was performed in 5 steps, not 4. 

### The every and some methods

Often times we may have to check if

- every element of an array satisfy a condition,
- there exists at least one element that satisfies a condition.

The `every` and `some` methods perform these checks.

Example:

```
const numbers = [3, 39, 42, 51];

const allAreEven = numbers.every( n => n % 2 === 0 );
// returns false

const allAreDivisibleByThree = numbers.every( n => n % 2 === 0 );
// returns true

const atLeastOneIsOdd = numbers.some( n => n % 2 !== 0 );
// returns true
```

### Adding and removing single array elements

Suppose an array `A` is given:

- `A.push( ...elements )` inserts `...elements` to the back of the array, modifying the original array. The new length of the array is returned.
- `A.pop()` removes the last element from array `A` and returns this removed element. 
- `A.unshift( ...elements )` inserts `...elements` to the front of the array, modifying the original array. The new length of the array is returned.
- `A.shift()` removes the first element (head) from array `A` and returns this removed element.

The `...elements` argument list can contain any number of arguments. The most common use case is one argument.

Example:

```
const A = ['a', 'b', 'c'];

A.push( 'X' );     // returns 4
console.log( A );  // prints ['a', 'b', 'c', 'X']

A.pop();           // returns 'X'
console.log( A );  // prints ['a', 'b', 'c']

A.unshift( 'X' );  // returns 4
console.log( A );  // prints ['X', 'a', 'b', 'c']
```

The spread operator and destructuring helps you express the same operations without the use of `push`,  `shift`, and `unshift`. 

```
// A.push( element )
A = [...A, element]

// A.unshift( element )
A = [element, ...A]

// A.shift()
[,...A] = A
```

The `pop` method can only be expressed with destructuring if we know the size of the array, and we denote each element with a variable:

```
// A.pop(), where A.length is 3:
[a, b] = A;
A = [a, b];
```

We only expressed `pop` for the sake of the exercise, because `pop` is a lot more semantic than these destructuring assignments.

Note that performance-wise `push`, `pop` are expected to be better, however, the difference is not major for small arrays. 

```
console.time( 'push_pop' );
for ( let i = 0; i < 1000000; ++i ) {
    let A = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    A.push( 10 );
    A.pop();
}
console.timeEnd( 'push_pop' );
console.time( 'spread' );
for ( let i = 0; i < 1000000; ++i ) {
    let A = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    A = [...A, 10];
    A.pop();
}
console.timeEnd( 'spread' );

VM229:7 push_pop: 68.93310546875ms
VM229:14 spread: 489.0859375ms
```

The output is the time elapsed between executing `console.time` and `console.timeEnd` on the same label.

The `shift` and `unshift` operations may perform worse than simple destructuring for small arrays.

```
console.time( 'unshift_shift' );
for ( let i = 0; i < 1000000; ++i ) {
    let A = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    A.unshift( 0 );
    A.shift();
}
console.timeEnd( 'unshift_shift' );
console.time( 'spread' );
for ( let i = 0; i < 1000000; ++i ) {
    let A = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    A = [0, ...A];
    [,...A] = A;
}
console.timeEnd( 'spread' );
VM282:7 unshift_shift: 176.8681640625ms
VM282:14 spread: 145.7060546875ms
```

As the size of the array grows, we may end up with times shifting in favor of `shift` and `unshift`:

```
console.time( 'unshift_shift' );
for ( let i = 0; i < 1000000; ++i ) {
    let A = new Array(1000).fill('a');
    A.unshift( 0 );
    A.shift();
}
console.timeEnd( 'unshift_shift' );
console.time( 'spread' );
for ( let i = 0; i < 1000000; ++i ) {
    let A = new Array(1000).fill('a');
    A = [0, ...A];
    [,...A] = A;
}
console.timeEnd( 'spread' );
VM319:7 unshift_shift: 7177.94873046875ms
VM319:14 spread: 18837.948974609375ms
```

The `push` and `unshift` methods may receive a variable number of arguments:

```
const A = [4, 5, 6];
A.push( 7, 8, 9 );       // returns 6
A.unshift( 0, 1, 2, 3 ); // returns 10

console.log( A );
// prints [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Array concatenation and the `concat` method

Suppose two arrays are given:

```
const A = [1, 2, 3];
const B = ['apple', 'pear'];
```

An obvious way to concatenate two arrays is to use the spread operator:

```
const AB = [...A, ...B];
// [1, 2, 3, "apple", "pear"]
```

The `concat` method is a generally more efficient way to perform the same concatenation:

```
A.concat( B )
(5) [1, 2, 3, "apple", "pear"]
A 
(3) [1, 2, 3]
B 
(2) ["apple", "pear"]
```

As you can see, `concat`  does not mutate the original array `A`.

We can supply multiple arrays in the argument list of `concat`:

```
const A = [1, 2];
A.concat( [3, 4], [5, 6], [], [7, 8] );

console.log( A );
// prints [1, 2, 3, 4, 5, 6, 7, 8]
```

Another way to concatenate arrays is to use `push`:

```
const A = [1, 2];
const B = [3, 4];
const C = [5, 6];
A.push( ...B, ...C );

console.log( A );
// prints [1, 2, 3, 4, 5, 6]
```

Notice that using `push` modifies the original array `A`.


### The `sort` method

The `sort` method sorts the values in an array:

```
const arr = [2, 5, 1, 3, 4];
arr.sort();

console.log( arr ); // [1, 2, 3, 4, 5]
```

Sorting is performed in place, *mutating* (changing the values inside) the original array. The `sort` method also returns a reference to the sorted array:

```
const arr = [2, 5, 1, 3, 4];
arr.sort()
// [1, 2, 3, 4, 5]
```

For strings, sorting is performed lexicographically based on unicode values:

```
const words = ['Frank', 'ate', 'apples'];
console.log( words.sort() )
```

The reason why `Frank` is before `ate` is that the character code value of `F` is lower than the character code value of `a`:

```
'F'.codePointAt(0)
70
'a'.codePointAt(0)
97
```

If the first character of both strings are equal, the upcoming characters are examined. As the code of `p` is smaller than the code of `t`, the order can be determined.

Unfortunately, the default `sort` implementation treats numbers as strings:

```
[12, 122, 21].sort()
// returns: [12, 122, 21]
```

We know that 122 is smaller than 21, but according to their string values, `21` has to be larger than both `12` and `122` due to their first character.

Another problem comes with the treatment of accented characters that occur in many languages. For instance:

```
['o', 'ö', 'u', 'ü'].sort()
// returns: ["o", "u", "ö", "ü"]
```

It is evident that `ö` should come right after `o`, but the character codes don't respect this order.

We can fix all these anomalies by passing a *comparator function* to `sort`. Sorting is performed based on the return value of the comparator function `comparator( a, b )`:

```
const arr = [12, 122, 21];
const comparatorLargestFirst = (x, y) => y - x;
const comparatorSmallestFirst = (x, y) => x - y;

arr.sort( comparatorLargestFirst );
// returns: [12, 21, 122]

arr.sort( comparatorSmallestFirst ); 
// returns: [12, 21, 122]
```

The above comparator functions solve the problem of numerical sorting. The `localeCompare` string method can be used to order characters of different locales:

```
["o", "u", "ö", "ü"].sort( (s1, s2) => s1.localeCompare( s2 ) )
// returns: ["o", "ö", "u", "ü"]
```

### The `reverse` method

The `reverse` method reverses an array in place:

```
const arr = [12, 122, 21];

arr.reverse() // returns: [21, 122, 12]

console.log( arr )
// prints: [21, 122, 12]
```
