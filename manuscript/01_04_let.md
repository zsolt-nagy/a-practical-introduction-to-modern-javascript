## The let keyword

First of all, in the below example, you have to know that `console.log` may print any number of arguments separated by commas. In the console, the values appear next to each other separated by a space.

We can create variables with the `let` keyword. Think of a variable like a drawer. Let *declares* a variable, which means to you that a drawer is created with a handle.

```
let myDrawer;
```

You can put a value in your drawer:

```
myDrawer = '$1.000';
```

In order to access the value, you have to grab the *handle* of the box and open it. In this example, you have a drawer called `myDrawer`. It contains a string written `'$1.000'` on it. To access your thousand bucks, you have to open the drawer:

```
drawer
'$1.000'
```

You can assign an initial value to your variable with the `=` sign. This is called *initialization*, and it can occur either in the same statement where you declared the variable (see `x`), or after the declaration (see `y`). You may access a declared variable even if you have not initialized it. Its value becomes `undefined`. 

```
let x = 5;

let y;
y = x ** 2;

let z;

console.log( x, y, z );
```

As the above editor is editable, try out one thing. 

Move `let z` below the `console.log` statement. You should see a `ReferenceError`:

```
ReferenceError: z is not defined
```

The message is somewhat misleading, because it means `z is not declared` using the `let` keyword. Don't mix this message with the `undefined` value. You only get the above reference error if you reference a variable that does not exist.

You did the following: you asked for the contents of your drawer `z` in the console log. But the drawer itself does not exist yet. You only created the drawer afterwards, with `let z;`:

```
console.log( z )  // Reference Error: z is not declared

let z;
```

*Side note: I know, in most tutorials, you see `var` instead of `let`. This is an advantage of reading an ES2018-compliant tutorial. Don't worry about var for now, you will hear about it later. Ok, I understand. If you do worry about it, read [this article](http://www.zsoltnagy.eu/es2015-lesson-2-function-scope-block-scope-constants/).*
