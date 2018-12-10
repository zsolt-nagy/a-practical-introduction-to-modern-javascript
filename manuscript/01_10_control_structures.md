## Control structures

The time has come, when we can fit the puzzle pieces together. You have learned about different primitive and composite types. You know how to check these types. You know the basic functions and arithmetic (addition, subtraction, multiplication etc.) and logical (true or false) operations in JavaScript. 

There are only two things missing. 

So far, we can write a sequence of instructions that perform a calculation. In software development, there are three types of control structures:

- sequence: writing instructions one after the other
- selection: either execute one set of instructions, or another
- iteration: execute a set of instructions a finite or infinite number of times

As you already know how to sequence instructions one after the other, it is time to learn about selection and iteration. Let's start with selection:

```
if ( condition ) {
    instruction1;
    instruction2;
    //...
}
```

The instructions inside the if-branch are only executed if `condition` is truthy. 

Notice the space between the `if` and the opening parentheses. This space is there to indicate that `if` is a *keyword* and not a function. Although this space is not mandatory, I highly recommend it for readability reasons.

```
function printNumber( x ) {
    if ( typeof x === 'number' ) {
        console.log( x + ' is a number.' ); 
    }
}

> printNumber( 5 )
5 is a number.
undefined
```

The first value is the console log. The second value is the return value of the `printNumber` function. Remember, if the return value of a function is not specified, it returns `undefined`.

If we call the `printNumber` function with a non-numeric value, it does not print the console log, because the instructions inside the `if` branch are only executed, whenever the condition inside the `if` statement is truthy.

```
> printNumber( '' )
undefined
```

It is a bit awkward that we don't print anything in case the input is not a number. You already know everything to write a program that does this. The thought process is the following:

- if `x` is a number, print it
- if `x` is not a number, print the message `"The input has to be a number."`


```
function printNumber( x ) {
    if ( typeof x === 'number' ) {
        console.log( x + ' is a number.' ); 
    }
    if ( typeof x !== 'number' ) {
        console.log( 'The input has to be a number.' ); 
    }
}
```

The second biggest problem with this solution is that we are writing too much for no reason.

The main problem with this solution is called *lack of abstraction*. Imagine that one day somebody comes and realizes that the condition `typeof x === 'number'` has to be modified. If you forget changing the second condition, you create an inconsistency in your code. We prefer thinking less when we don't have to. Therefore, I recommend another solution, where we only have one condition:

```
function printNumber( x ) {
    if ( typeof x === 'number' ) {
        console.log( x + ' is a number.' ); 
    } else {
        console.log( 'The input has to be a number.' ); 
    }
}
```

Notice the `else` keyword. The `else` branch is only executed if the original condition is not true.

We can cascade this approach further, because after the `else`, you can have another condition:

```
function logLampColor( state ) {
    if ( state === 1 ) {
        console.log( 'Red' );
    } else if ( state === 2 ) {
        console.log( 'Yellow' );
    } else if ( state === 3 ) {
        console.log( 'Green' );
    } else {
        console.log( 'Wrong lamp state' );
    }
}
```

The beauty of the above code is that you can read it as if it was plain English. If the state is 1, then log Red. Otherwise if the state is 2, then log Yellow. And so on.

There is an abbreviated version for a long chain of if-else statement: the `switch` operator. Switch is like a telephone operator. It puts you through some code in case the correct value is stored in your variable. There is also a default line, saying "the number you have dialed is invalid".

```
function logLampColor( state ) {
  switch( state ) {
    case 1:
      console.log( 'Red' );
      break;
    case 2:
      console.log( 'Yellow' );
      break;
    case 3:
      console.log( 'Green' );
      break; 
    default:
      console.log( 'Wrong lamp state' ); 
  }
}

logLampColor( 1 );
```

Try this code example out. Play around with it. Check what happens if you remove the `break` commands. Check what happens if you call this function with other arguments.

Now that you got a feel for the switch statement, let me explain it. You have a variable inside the `switch`. This variable may have values. We jump to the `case` label for which `state` is equal to the label value.

Then we start executing the code.

If there was no `break` at the end of the code segment belonging to a label, execution would continue on the next code line. It does not matter that it is now under another label. Code just jumps through the labels.

This is why we have a `break` statement at the end of each code segment belonging to a label. The `break` statement jumps out of the closest `switch` statement, and your program continues execution after the switch statement.

We have two reasons not to include a `break` statement after a label:

- we use a `return` statement instead,
- we intentionally fall onto the next label (discouraged).

Example:

```
function getLampColor( state ) {
    switch( state ) {
        case 0:
        case 1:
            return 'Red';
        case 2:
            return 'Yellow';
        case 3:
            return 'Green';
    } 
}

getLampColor( 1 );
```

In this example, both cases `0` and `1` return `'Red'`.

Notice you already know another way to return values without `if-else`:

```
function getLampColor( state ) {
    return state == 1 ? 'Red' : 'Green';
}
```

The ternary operator gives you red if the state is `1`, and green otherwise.

We can place another ternary expression in place of `'Green'` to add more lamp states:

```
function getLampColor( state ) {
    return state == 1 ? 'Red' : 
           state == 2 ? 'Yellow' :
           state == 3 ? 'Green' :
           'Error';
}
```

Some people don't like this way of writing code. You can hit up their rant about how awful this construct is under the name of *ternary operator abuse*. I personally do not share their opinion, but this does not matter. If you believe you should use it, use it.

That's all for selection. Let's see iteration. In order to execute the same expressions multiple times, we create *loops*. A loop is like a cheap song. You know, Berlin is famous for the city of DJs. Sometimes I believe every third man claims he is a DJ. I happened to be a neighbor of one, fortunately, property management terminated his contract. This lunatic guy "worked" on one melody for half a year. And he repeated it over and over and over and over and over and over again. 

Think of a loop like the song "Around the world, around the wo-orld. Around the world, around the wo-orld...". You get the idea. Take a melody, repeat it a hundred times, and you get the song. In programming terms, take some code, repeat it `x` amount of times, and you get code executed a hundred times.

Let's create a function that sums the values of an array:

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];
```

The first four numbers are not by accident. They were the level selector cheat code of Sonic 2. If you have slight aspergers syndrome, you tend to remember some weird numbers.

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    let sum = 0;
    let i = 0;
    while ( i < values.length ) {
        sum += values[i];
        i += 1;
    }
    console.log( 'The loop was executed ' + i + ' times' );
    return sum;
}

sumArray( numbers );
```

The variable `i` keeps track of how many times the loop is executed. 

First the JavaScript interpreter examines the condition in the `while` loop. As `i` is `0` and `numbers.length` is `13`, we conclude the condition is true.

If the condition is true, we execute the body of the while loop. So we add the ith element of the array to the sum, and increase the loop variable by `1`.

Then we compare `1` against the length of the array, `13`. As `1` is smaller than `13`, we execute the loop body again. The `sum` variable now stores `19 + 65 = 84`. The value of `i` becomes `2`.

We continue this until `i` becomes `13`. Then we realize the condition `i < numbers.length` becomes `false`. Once the condition of the `while` loop becomes `false`, we continue with the code after the `while` loop.

This is an important concept, so let's spend a bit more time on the execution. I am using a resource you will find weird: [pythontutor.com](pythontutor.com). I know, we are learning JavaScript. The author of the website has a great JavaScript engine too, so don't worry, we are not learning Python. The code being executed is valid JavaScript code.

Start moving the slider from left to right to see how the value of the variables change.

The below content may or may not work for you. If you cannot see the example below, please click [this link](http://pythontutor.com/javascript.html#code=let%20numbers%20%3D%20%5B19,%2065,%209,%2017,%204,%201,%202,%206,%201,%209,%209,%202,%201%5D%3B%0A%0Afunction%20sumArray%28%20values%20%29%20%7B%0A%20%20%20%20let%20sum%20%3D%200%3B%0A%20%20%20%20let%20i%20%3D%200%3B%0A%20%20%20%20while%20%28%20i%20%3C%20values.length%20%29%20%7B%0A%20%20%20%20%20%20%20%20sum%20%2B%3D%20values%5Bi%5D%3B%0A%20%20%20%20%20%20%20%20i%20%2B%3D%201%3B%0A%20%20%20%20%7D%0A%20%20%20%20console.log%28%20'The%20loop%20was%20executed%20'%20%2B%20i%20%2B%20'%20times'%20%29%3B%0A%20%20%20%20return%20sum%3B%0A%7D%0A%0AsumArray%28%20numbers%20%29%3B&curInstr=0&mode=display&origin=opt-frontend.js&py=js&rawInputLstJSON=%5B%5D) instead.

We have a few more loops to go. The `do-while` loop executes the loop body at least once, and checks the condition before the end.

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    if (  values.length == 0 ) return 0;
    let sum = 0;
    let i = 0;
    do {
        sum += values[i];
        i += 1;
    } while ( i < values.length );
    console.log( 'The loop was executed ' + i + ' times' );
    return sum;
}

sumArray( numbers );
```

Notice the first line in the function. We have to exit the `sumArray` function before reaching the `do-while` loop in case the array is empty. Otherwise, the code works in the exact same way as the while loop, except that the condition for running the loop again is at the bottom.

We mainly use do-while loops for input validation. The user inputs a value, then we check its validity. 

Let's use the `prompt` function to get a value. 

`prompt( 'message' )` opens a dialog displaying message. A textfield appears in the dialog, where you can enter a value. Once you press the OK button, the `prompt` function returns a string.

Example:

```
let name = '';
do {
    name = prompt( 'Enter a name!' );
} while ( name.length == 0 );
```

This is where the do-while loop makes sense, because we can be sure we need to enter data at least once. In the example summing array members, using the do-while loop is technically possible, but it does not make sense, because the simple while loop is easier.

You will now learn another loop that is perfect for iteration: the *for* loop. This loop combines several lines of code into one. The execution of the for loop is identical to the while loop:

```
initialization_of_loop_variable;
while ( condition ) {
    statements;
    increment_loop_variable;
}

for ( initialization_of_loop_variable; condition; increment_loop_variable ) {
    statements;
}
```

The for loop has everything you need in one line. You don't have to mix your loop body with the increment of the loop variable. The execution of the for loop is as follows:

1. `initialization_of_loop_variable`
2. check `condition`. If `condition` is falsy, exit the for loop
3. `statements` in the loop body
4. `increment_loop_variable`, then go back to step 2

Rewrite the `sumArray` function using a for loop. Here is the example with the `while` loop:

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    let sum = 0;
    let i = 0;
    while ( i < values.length ) {
        sum += values[i];
        i += 1;
    }
    return sum;
}

sumArray( numbers );
```

Don't continue reading before you solve this exercise. Please change the while loop into a `for` loop.

Welcome back!

I hope you liked the exercise. To verify your solution, check this code:

```
for ( let i = 0; i < values.length; i += 1 ) {
    sum += values[i];
}
```

This code should go in place of 

```
    let i = 0;
    while ( i < values.length ) {
        sum += values[i];
        i += 1;
    }
```

Notice you can declare variables in the initializer part of the for loop. The rest of the code works exactly like the `while` loop.

Let's simplify the for loop a bit further: you can write `i++` or `++i` in place of `i += 1`:

```
for ( let i = 0; i < values.length; ++i ) {
    sum += values[i];
}
```

In some programming competitions, people tend to count downwards instead of upwards. The reason is that computing `values.length` costs some nanoseconds more than checking if the value of `i` is positive:

```
for ( let i = values.length - 1; i >= 0; --i ) {
    sum += values[i];
}
```

These wannabe geniuses don't stop there by the way. They go even further:

```
for ( let i = values.length; i; sum += values[--i] );
```

Weird, isn't it? Instead of iterating from `12` to `0`, we iterate from `13` to `1`. The condition `i` is `true` as long as its value stays non-zero. This is the easiest check a computer can make with an integer.

Suppose `i` is `13`. `values[--i]` is interpreted as `values[12]`, because first we decrease the value of `i`, then we equate the expression `--i` to the new value of `i`. This is a unique case when writing `i--` would have been incorrect, because our array does not even have an element at index `13`.

Don't worry if you don't feel like understanding this optimization technique. Once you read this article for the tenth time, you will most likely get it. It's normal. Oh, and by the way, I discourage using such optimizations. Readability always trumps these slight edges. Sometimes you can save seconds in your code, so don't bother with the nanoseconds. It's like being penny-wise and pound-fool.

Another reason to avoid looking smart and optimizing your code is that JavaScript interpreters actually optimize code for you. This is a very easy and straightforward optimization. You don't have to bother doing it yourself. Just stick to this version of the for loop:

```
for ( let i = 0; i < values.length; ++i ) {
    sum += values[i];
}
```

Our next simplification is the `for..in` loop. Why bother iterating an `i` variable if a loop can take care of it for us?

```
for ( let i in values ) {
    sum += values[i];
}
```

The `for..in` loop enumerates all the available indices of the `values` array from `0` to `12` in ascending order.

I have another simplification for you. What if I said, "why bother using a variable for iteration at all, if we could enumerate the values of the array?". In ES6, there is a loop called the `for...of` loop, which does exactly that.

```
for ( let value of values ) {
    sum += value;
}
```

That's all. Go back to the editor and substitute the `for..in` and the `for..of` constructs in place of your for loop. It works exactly the same way.

We are almost done. Just two small constructs. 

We can use `break` or `continue` inside the loops:

- `break` exits the closest loop it is in, and continues with the next command,
- `continue` skips out from the loop body, and jumps back to the condition of the loop.

Example: sum every second element of the `numbers` array:

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    let sum = 0;
    for ( let i in values ) {
        if ( i % 2 == 0 ) continue;
        sum += values[i];
    }
    return sum;
}

sumArray( numbers );
```

This example is artificial, because we could have written `i += 2` in a simple for loop to jump to every second value. So we are testing `continue` just for the sake of the example. Whenever `i` is even, `continue` moves execution back to the next iteration of `i in values`. 

Notice that we don't have to use braces around just one statement in the code if it is followed by an `if` statement or a loop:

```
if ( i % 2 == 0 ) continue;
```

is the same as

```
if ( i % 2 == 0 ) {
    continue;
}
```

We still prefer braces, because wrong code formatting may lead to many sources of error. For example, some people might think that `statement1` and `statement2` belongs to the loop body.

```
while ( condition )
    statement1;
    statement2;
```

Wrong!

If we added the braces, we would get the following code:

```
while ( condition ) {
    statement1;
}
statement2;
```

This must be very confusing for people familiar with Python. `statement2` is outside the loop. 

You already know what a `break` statement looks like, because we learned it when dealing with the `switch` statement. It is doing the same thing in loops. Suppose we want to break out from the loop whenever the sum exceeds 100:

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    let sum = 0;
    for ( let i in values ) {
        sum += values[i];
        if ( sum >= 100 ) {
            break;
        }
    }
    return sum;
}

sumArray( numbers );
```

I placed the `break` in braces on purpose to show you that `break` breaks out of `switch` statements and loops, not from `if` statements. When break is executed, control is handed over to the statement after the loop: `return sum`.

In this specific example, we don't even need a `break`, because instead of breaking out of the loop, we can return the sum:

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    let sum = 0;
    for ( let i in values ) {
        sum += values[i];
        if ( sum >= 100 ) return sum;
    }
    return sum;
}

sumArray( numbers );
```

Technically, this is an example, where I would suggest a more flexible for loop:

```
let numbers = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];

function sumArray( values ) {
    let sum = 0;
    for ( let i = 0; i < values.length && sum <= 100; ++i ) {
        sum += values[i];
    } 
    return sum;
}

sumArray( numbers );
```
