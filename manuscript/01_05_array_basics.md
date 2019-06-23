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
