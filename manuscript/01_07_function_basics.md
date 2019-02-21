## Functions

Think of a function like a mathematical function giving you a relationship between input and output variables. If you don't like maths, think of a function like a vending machine. You give it some coins and a number, and it gives you a bottle of cold beverage. 

```
function add( a, b ) {
    return a + b;
}
```

This function definition describes the relationship between its input variables `a` and `b`, and the return value of the function.

The return statement returns the value of the function. When calling the `add` function with *arguments* `a` and `b`, it computes the value `a+b` and returns it. Example:

```
function add( a, b ) {
    return a + b;
}

> add( 5, 2 )
7
```

Try to modify the input variables. The return value also changes. Try to call the add function with one variable, e.g. `add( 5 )`, and see what happens. 

Functions are useful to create reusable chunks of code that you can call with different arguments. We will write more useful functions once you learn the basics of control structures.

You can also define functions without placing the name between the `function` keyword and the argument list. This structure is great if you want create a reference to it using a variable. Remember, the variable `subtract` is a handle to a drawer. This time, your drawer contains a function.

```
let subtract = function( a, b ) {
    return a - b;
}
```

There is another popular notation first introduced in ES6: the fat arrow notation. 

```
let multiply = ( a, b ) => a * b;
```

The fat arrow describes the relationship between the argument list and the return value. If there is only one input argument, you may omit the parentheses around it:

```
let square = a => a * a;
```

All functions can be called using their references:

```
> add( 2, 3 )
5
> subtract( 2, 3 )
-1
> multiply( 2, 3 )
6
> square( 2 )
4
```

When a function does not return anything, its return value becomes `undefined`:

```
> let empty = function() {}

> empty()
undefined
```

The JavaScript interpreter always inserts a `return undefined;` statement at the end of each function. This is the default return value of every function. This default value can be overridden by the developer by specifying a return statement.

Variables inside the function are not the same as variables outside the function:

```
let a = 5;
function addOne( a ) {
    a = a + 1;
    return a;
}

> addOne( a ) 
6
> a
5
```

The `a` variable inside the function is valid inside the *scope* of the function. It *shadows* the variable `a` outside the function. Therefore, adding one to the internal `a` variable does not have any effect on the external value.
