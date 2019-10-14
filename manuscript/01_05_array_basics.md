## Arrays

An array is an ordered list of items. The items may be of any type. You know, in most post offices, there are hundreds or thousands of post boxes. Each post box may or may not contain something. Each post box has a numeric handle. Post box 25 may be your box. You unlock it, grab its handle, and access its contents.

The trick is that in case of arrays, you have to imagine the post boxes with handles called *keys* of 0, 1, 2, and so on. Typically, arrays have continuous keys.

```
let days = [ 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ];
```

If you are looking for post box `3` among the `days` post office, you get `Thursday`, because `Monday` is the 0th element, `Tuesday` is the 1st element, `Wednesday` is the 3rd element, and `Thursday` is the 4th element of the array.

Arrays do not have to contain elements of the same type. We can place strings, `null`, `undefined`, symbols, objects, and other arrays in the array:

```
let storage = [ 1, 'Monday', null ];
```

According to an joke, Bill Gates once visited a lower grade class and asked children to start counting to ten. One of the children stood up and said, one, two, three, four, five, six, seven, eight, nine, ten. Bill Gates thanked for the efforts of the kid and asked someone else. A second kid stood up and started counting: one, two, three, four... Bill Gates already knew the result, so he thanked the second student for his efforts and asked someone else. Then came a third kid forward and started counting: zero, one, two, three... and this is when the kid got hired by Microsoft.

The takeaway of this story is that each element of the array can be accessed using an *index* starting from zero:

```
> days[0]
'Monday'

> days[4]
'Friday'

> days[5]
undefined
```

In the third example, we indexed out of the array.

Arrays have lengths:

```
> days.length
5
```

We often need to access the last element of an array. For instance, the `days` array has a length of `5`. Indexing of an array starts with `0`. Therefore, the last index is `4`. *In general, the index of the last element equals the length of the array minus `1`:*

```
> days.length - 1
4

> days[ days.length - 1]
'Friday'
```

> Remark: In some other languages, such as Python, we can refer to the last element of a list using the index `-1`. In Python, `days[-1]` is the same as `days[len(days) - 1]`. The index of `-1` is interpreted as the first element counting backwards from the end of the list. In JavaScript, we cannot use this way of indexing.

You can add elements to the beginning and to the end of the array.

```
> days.push( 'Saturday' );

> console.log( days ); // add 'Saturday' to the end
["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]

> days.unshift( 'Sunday' ); // add 'Sunday' to the beginning
["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]
```

You can also remove these elements from the array:
- Pop removes the last element from the array and returns it.
- Shift removes the first element from the array and returns it.

```
> let element = days.pop();
> console.log( element, days );
"Saturday" ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]

> let secondElement = days.shift();
> console.log( element, days );
"Sunday" ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
```

Similarly to objects, you can delete any element from the array. The value `undefined` will be placed in place of this element:

```
> delete days[2]
["Monday", "Tuesday", undefined, "Thursday", "Friday"]
```

The values of an array can be set by using their indices, and equating them to a new value. You can overwrite existing values, or add new values to the array. The indices of the added values do not have to be continuous:

```
> days[2] = 'Wednesday';
> days[9] = 'Wednesday';
> console.log( days );
["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", undefined, undefined, undefined, undefined, "Wednesday"]
```

Strings also provide access to their characters as if a string was an array of characters:

```
const str = 'Hello';

console.log( str[1], str[4], str[5] );
// --> e o undefined
```

The element at index 1 is the character `e`. The element at index 4 is the fifth character of the string, `o`. If we tried to access the element at index 5 of the string, we would get the sixth character of the array. This would make us index out from the array though. In JavaScript, indexing out from an array or string is possible: we just get an `undefined` value.

Our last language construct is the `slice` method. Unsurprisingly, this method slices an array, returning a *new array* with a continuous subset of elements.

We can specify the beginning of the slice as follows:

```
let days = [ 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ];

> console.log( days.slice( 1 ) )
[ 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ]

> console.log( days.slice( 4 ) )
[ 'Friday' ]
```

The beginning of the slice is the index of the first element *we want to see in the slice*. This number can also be zero, in which case we make a *shallow copy* of the original array:

```
let daysCopy = days.slice( 0 );
daysCopy[0] = '???';

console.log( days );
// [ 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ]

console.log( daysCopy );
// [ '???', 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ]
```

If you know the difference between a *shallow copy* and *deep copy*, be aware that `slice` creates the former. Otherwise, at this stage, it is enough to understand that slice always returns a new array, copying its elements.

For a useful slicing operation, we also need a way to specify the end of the slice. In JavaScript, the end of the slice is specified as *the index of the first element we do not want to see in the array*.

```
// Monday - Wednesday:
// - we start with the 0th element,
// - the first element we don't want is at index 3
> days.slice( 0, 3 )
[ 'Monday', 'Tuesday', 'Wednesday' ]

// Thursday:
// - we start at index 3
// - the first element we don't want is at index 4
> days.slice( 3, 4 )
[ 'Thursday' ]
```

Specifying the end of the slice is optional. This means, `days.slice( 1 )` is the same as `days( 1, days.length )`.

> Remark: as many developers learn Python, it's worth noting that Python uses the colon in the index for slicing. `days[0:3]` is the same as `days( 0, 3 )`. Whenever we have a zero on any side of the column in Python, that zero is optional: `days[:3]` is the same as `days[0:3]`, `days[2:]` is the same as `days.slice( 2 )` in JavaScript, and `days[:]` is the same as `days.slice( 0 )` in JavaScript. We can see how similar some programming languages are to each other. You are better off learning the thought process, and then the syntax will be easy.

As with most topics, bear in mind that we are just covering the basics to get you started in writing code. There are multiple layers of knowledge on JavaScript arrays. We will uncover these lessons once they become important.


### Exercises: Arrays

**Exercise 25:** Without executing the code, determine what is written to the console:

```
let array = [ 7, 15, 32, 9, '3', '11', 2 ];

// A.
console.log( array[3] );

// B.
console.log( array[7] );

// C.
console.log( array.pop() );

// D.
console.log( array );

// E.
console.log( array.shift() );

// F.
console.log( array );

// G.
console.log( array.push( 6 ) );

// H.
console.log( array );
```

**Exercise 26:** Without executing the code, determine what is written to the console:

```
const days = [
    'Monday',
    'Tuesday',
    'Wednesday',
    'Thursday',
    'Friday'
];

console.log( days[2] );
console.log( days[1][2] );
console.log( days[ days.length - 1][1] );
```
