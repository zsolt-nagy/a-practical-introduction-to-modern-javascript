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

There is another popular notation first introduced in ES6: the *fat arrow* notation.

```
let multiply = ( a, b ) => a * b;
```
The fat arrow describes the relationship between the argument list and the return value. In other words, it expects two values, `a` and `b`, and transforms these values to `a * b`.

Arrow functions are typically used when the input can be transformed to an output that can be calculated using the input variables:

```
function functionName( a, b, ... ) {
    return value;
}

// conversion:
var functionName = ( a, b, ... ) => value;
```

If there is only one input argument, you may omit the parentheses around it:

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
let coins = 5;
function addOne( coins ) {
    coins = coins + 1;
    return coins;
}

> addOne( coins )
6
> coins
5
```

The `coins` variable inside the function is valid inside the *scope* of the function. It *shadows* the variable `coins` outside the function. Therefore, adding one to the internal `coins` variable does not have any effect on the external value. To see the execution of this code in action, follow [this URL](http://pythontutor.com/javascript.html#code=let%20coins%20%3D%205%3B%0Afunction%20addOne%28%20coins%20%29%20%7B%0A%20%20%20%20coins%20%3D%20coins%20%2B%201%3B%0A%20%20%20%20return%20coins%3B%0A%7D%0A%0Alet%20result%20%3D%20addOne%28%20coins%20%29%3B%0Aconsole.log%28%20result%20%29%3B%0Aconsole.log%28%20coins%20%29%3B&curInstr=7&mode=display&origin=opt-frontend.js&py=js&rawInputLstJSON=%5B%5D).

We learned earlier that variables declared using `var` are function scoped. Function arguments are also function scoped:

```
let coins = 5; // this is a global variable even if var was used
function addOne( coins ) {
    // the inner coins variable shadows the global coins
    // only the inner coins variable is accessible
    coins = coins + 1;
    return coins;
}
```

When there is a variable both inside and outside a function, the inner variable is said to *shadow* the outer variable whenever we execute  code inside the function. This is what happened to the `coins` variable. Operations modifying the value of the inner `coins` variable do not affect the value of the outer `coins` variable.

Without changing execution of the code, we can safely rename the inner variable to illustrate that the two variables are different and only the inner variable is modified inside the function:

```
let coins = 5;
function addOne( innerCoins ) {
    innerCoins = innerCoins + 1;
    return innerCoins;
}
```

### Exercises: functions

**Exercise 34:** Let's recall a possible solution of the number conversion exercise:

```
let hexadecimalValue = 'FF';
let baseTenValue = Number.parseInt( hexadecimalValue, 16 );
console.log(
    hexadecimalValue + ' in base 10:',
    baseTenValue,
    '\n' + hexadecimalValue + ' in base  2:',
    baseTenValue.toString( 2 )
);
```

Write a function that expects a string containing a correctly formatted hexadecimal number, converts this hexadecimal value to base `10` and base `2`, and console logs the result:

```
> convert( 'ACE' )
ACE in base 10: 2766
ACE in base  2: 101011001110
```

**Exercise 35:** Write a head comment to the function you created in the previous exercise. Head comments describe the parameters, the return value, and a one sentence summary of what the function does. Head comments typically have the following format:

```
/**
 *  One sentence summary of the function
 *  
 *  @param  string    description of the parameter
 *  @return undefined
 */
```
