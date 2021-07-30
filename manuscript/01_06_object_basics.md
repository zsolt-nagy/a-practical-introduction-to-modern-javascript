## The Object type

This section will introduce the Object type. We will only learn the basics here.

An object is a data structure with String or Symbol keys and arbitrary values. Imagine it like a machine that accepts a key, and gives you a value. Some people call this data structure *associative array*, others call it *hashmap*. These names may sound fancy, but essentially we mean the same thing.

*Side note: we will only deal with `String` keys for now. `Symbol` keys are also allowed for strings. `Symbol` keys are also allowed for strings, but at this stage, it is not beneficial to learn about symbols.*

An associative array is like human memory. In order to get access to memory, we need an association, which is a handle or a key. This key unlocks the memory by providing access to it. The address of associative memory is therefore content. In JavaScript, we will use strings to describe this content.

```
let author = {
  name: null,
  website: "zsoltnagy.eu",
  age: 35
}

console.table( author );
```

Run the above code in the console of Google Chrome developer tools. You can see that `console.table` enumerates the keys and values of the `author` object in a tabular format.

Similarly, `console.log( author )` also logs the `author` object, but in this log, we need more clicks to read the keys and values.

The members of the `author` object can be accessed using a dot. For instance, `author.name` gives you read and write access to the `name` property of the `author` object. For instance, we can read the `author.name` value and log it using `console.log( author.name )`. To change the value of the name property, we have to write `author.name = 'Zsolt'`.

```
author.name = "Zsolt";
console.log( author.name, author.website )
// Prints: Zsolt zsoltnagy.eu
```

It is possible to delete members of an object using the `delete` operator:

```
delete author.name
console.log( "Author name: ", author.name )
// Prints: Author name: undefined
```

If a field in an object is deleted or not even declared, the value of this field is `undefined`.

```
let o = {};

> o.name
undefined
```

An object contains *fields*. A *field* in an object can be referenced in the following ways:

- the already introduced dot notation: `object_name.member_name`
- bracket (associative array) notation: `object_name[ string_or_symbol_value ]`

Let's explore how we can select a member of an object if the corresponding key is in a variable:

```
let key = 'website';

// How can we select author.website?
```

The solution is to use the bracket notation and get `author[ key ]`. The value inside the brackets is converted to a key.

```
author[ key ]
// Prints: zsoltnagy.eu
```

We already know that the key of an object is a string. If we supply a key of a different type inside the brackets, then this key is automatically converted to a string:

```
const key = 1;
const street = {};

street[ key ] = 'house';

console.log( street );
```

After executing the above code, the value `{ "1": "house" }` is printed to the console.

A member of an object can be another object:

```
let car = { numberPlate: 'ABC123' };

let garage = {
    size: 1,
    parking: car
}
```

Here we can see that the garage has an integer size and an object property called `parking`.

We typically build objects using braces by enumerating key-value pairs inside an opening brace and a closing brace. Once an object is built, we can add more properties to it:

```
garage.owner = { name: 'Zsolt' };
```

In the above example, we changed the value of `garage.owner` from the default `undefined` to an object.

We saw that we can refer to members of an object in two ways:

1. dot notation: the value of `garage[size]` is `1`,
2. bracket notation: `garage['size']` is `1`.

The two notations are equivalent.

It is important to note that in the bracket notation, you need a value that can be converted to a string and does not throw an error. Therefore, if you try to retrieve `garage[ nonExistingKey ]`, you get an error in case the variable `nonExistingKeys` is not declared.


### Exercises: objects

**Exercise 27:** Create an object that models a lottery poll. A lottery poll is defined by its time. We model this time using a string of format `"2020-11-25 18:20"`. We also store the prize, which is also a string of form `"20.000.000$"`. We also store five numbers that can range between `1` and `90`. These values are stored in an array.

**Exercise 28:** Suppose the following object is given:

```
let ticket = {
    from: {
        airport: 'HAN',
        date: '2020-11-05',
        time: '09:40'
    },
    to: {
        airport: 'AAA',
        date: '2020-11-05',
        time: '11:25'
    },
    name: 'Java Script',
    passport: '123456XY'
}
```

Using this object, write the following values to the console:

- start and arrival time and date,
- name,
- passport id,
- airport code of the destination.

**Exercise 29:** Create an object that contains an infinitely long chain of object references. For instance, if you call your object `tree`, make sure `tree.tree`, `tree.tree.tree`, `tree.tree.tree.tree` etc. are all available.

```
let tree = { leaf: "fruit" };

// Write your solution here such that the below logs
// all write "fruit"

console.log( tree.leaf );            // "fruit"
console.log( tree.tree.leaf );       // "fruit"
console.log( tree.tree.tree.leaf );  // "fruit"
// ...
```

**Exercise 30:** Suppose there is a `safe` object. The safe is opened by a secret key combination `"123456"`. Create a reference that unlocks the safe and provide access to the value belonging to the key `"123456"`.

```
let safe = { "123456": "$10.000" };
```

**Exercise 31:** We learned that the key of an object can either be a string or a symbol. Suppose that there is a variable declared and defined as `let num = 5;`. Consider the following code:

```
let num = 5;
let o = {};

o[ num ] = true;

console.log( o, o[ 5 ], o[ "5" ] );
```

Run the above code in your console and check the output. Explain what happens to the `5` key in `o[ 5 ]` that results in the log you saw.

Now let's create a variable containing the `"5"` string, and run this code:

```
let text = '5';

o[ 'text' ] = false;

console.log( o, o[ 5 ], o[ "5" ] );
```

Run the above code and explain what happens when querying `o[ 5 ]`.

**Exercise 32:** Create a `map` object with keys of the values of array `arr`. The values belonging to the keys are universally `true`. Use the `console.table` function to inspect the `map` object in Chrome developer tools.

```
let arr = [1, 5, 3, 1];

let map = {};

// Write valid JavaScript code in place
// of the  ____ symbols to add key-value pairs to map.
// ____arr[0]____ = true;
// ____arr[1]____ = true;
// ____arr[2]____ = true;
// ____arr[3]____ = true;

console.table( map );
```

**Exercise 33:** Modify the previous exercise such that instead of `true`, the values belonging to keys `arr[0]`, `arr[1]`, `arr[2]`, `arr[3]` are their respective indices `0`, `1`, `2`, `3`. Before running your code, determine the key-value pairs stored in the object `map`.

```
let arr = [1, 5, 3, 1];

let map = {};

// Write valid JavaScript code in place
// of the  ____ symbols to add key-value pairs to map.
// ____arr[0]____ = 0;
// ____arr[1]____ = 1;
// ____arr[2]____ = 2;
// ____arr[3]____ = 3;

console.table( map );
```
