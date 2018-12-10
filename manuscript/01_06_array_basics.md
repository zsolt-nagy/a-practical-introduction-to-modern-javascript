## Arrays

An array is an ordered list of items. The items may be of any type. You know, in most post offices, there are hundreds or thousands of post boxes. Each post box may or may not contain something. Each post box has a numeric handle. Post box 25 may be your box. You unlock it, grab its handle, and access its contents. 

The trick is that in case of arrays, you have to imagine the post boxes with keys 0, 1, 2, and so on. Typically, arrays have continuous keys.

```
let days = [ 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ];
```

Arrays do not have to contain elements of the same type:

```
let storage = [ 1, 'Monday', null ];
```

Each element of the array can be accessed using an index starting from zero:

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

As with most topics, bear in mind that we are just covering the basics to get you started in writing code. There are multiple layers of knowledge on JavaScript arrays. We will uncover these lessons once they become important.
