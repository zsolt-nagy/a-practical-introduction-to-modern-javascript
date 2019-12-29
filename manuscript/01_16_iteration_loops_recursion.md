## Iteration: Loops and Recursion

Now that we know how selection works, let's move on to learn about iteration.

### Recursive function calls

Let's start with an introductory example. First, we'll create a simple array:

```
let numbers = [19, 65, 9, 17];
```

If these numbers look familiar to you, yes, they form the level select cheat code of the Sega classic, Sonic 2.

**Exercise**: Using what you already know, calculate the sum of the elements of the `numbers` array. The `numbers` array can contain arbitrary elements.

**Solution**: We have learned how to write if-else statements, functions, operators. The problem is, we have not learned how to sum more than two numbers. Therefore, we need some inspiration to solve this riddle.

We know that the sum of the elements of an empty list is 0.

We also know that the sum of elements of a list of lenth 1 equals the only element of the list.

Suppose we can somehow sum the first `i` elements of the `numbers` list and store it in the variable `S`. Using the value `S`, we can sum the first `i + 1` elements of the list: `S + numbers[i]`.

Ha valahogy a lista első `i` elemét összegezni tudjuk, és ez az összeg `S`, akkor a lista első `i+1` elemének az összege `S + numbers[i]`.

In tabular form:

```
index  numbers[index]   previous sum  new sum
    0       19          0             0 + 19 =  19
    1       65          19            19 + 65 =  84
    2        9          84            84 +  9 =  93
    3       17          93            93 + 17 = 110
```

We have created our first *loop*. Each *iteration* of the loop is characterised by an index ranging between 0 and `numbers.length - 1`. During each iteration, two things change:

- the index,
- the sum.

All we need to do is note the value of the index and the sum in each iteration. Perform all the iterations by looping through the whole array.

We need to know when to end the iteration. We finish iterating once the value of `index` reaches `numbers.length`.

Let's turn this idea into code. We will use a function to perform an iteration of the loop.

For the sake of simplicity, we will do the exact opposite of what our original idea was. In the original idea, we took the sum of the first `i` elements and added the `i + 1`th element to the sum. Here, we take the first element, and add it to the sum of the rest of the list. This small difference determines if the sum is calculated from left to right or right to left. As a benefit, our function will be more compact.

```
function sum( array ) {
    return array.length === 0 ? 0 :
           array[0] + sum( array.slice( 1 ) );   
}
```

If the list is empty, zero is returned as the sum.

If the list is not empty, we take its first element, and add it to the sum of the remaining elements. Example:

Step 1. `sum( [ 19, 65, 9, 17 ] )`. The first element is `19`.
Step 2. `19 + sum( [ 65, 9, 17 ] )`
Step 3. `19 + 65 + sum( [ 9, 17 ] )`
Step 4. `19 + 65 + 9 + sum( [ 17 ] )`
Step 5. `19 + 65 + 9 + 17 + sum( [] )`
Step 6. `19 + 65 + 9 + 17 + 0`

After the last step, the sum becomes `110`.

We have successfully created *iteration* using functions. Iteration is a piece of code that we run over and over again. Although we are using functions now, at a later stage, we will use loops to implement iteration.

A loop is like a cheap song. This reminds me of Berlin, where every third person claims they are a DJ. Once I had a "DJ" neighbour too. Fortunately, the property management didn't tolerate his activities. I can still recall as he was "working" on the same melody for half a year. Over and over again... until someone called the police. 

Take a short melody, repeat it a hundred times. You get a song. Simple, isn't it? Programming is similar: take a code segment and run it many times.

Although it is possible to use functions to implement iteration, this solution is rarely recommended. In the future, we will learn how to write iteration using loops. This form becomes a lot more compact than the function form, let alone the performance benefits.

A> Iteration using a function calling itself is called *recursion*. 

To introduce an important concept that helps you understand loops, let's reorganize the solution a bit:

```
function sum( array ) {
    return sumHelper( array, 0, 0 ); 
}

function sumHelper( array, index, previousSum ) {
    if ( index >= array.length ) return previousSum;
    var newSum = previousSum + array[index];
    sumHelper( array, index + 1, newSum );
}
```

By using *default function argument values*, we can make this solution even more compact:

```
function sum( array, index = 0, previousSum = 0 ) {
    if ( index >= array.length ) return previousSum;
    return sum( array, index + 1, previousSum + array[index] );
}
```

When the value of `index` or `previousSum` is not given, the default value is used. So `sum( [1, 2] )` is the same as `sum( [1, 2], 0, 0)`.

Let's use arrow functions and the ternary operator to simplify the function even more:

```
const sum = ( array, index = 0, previousSum = 0 ) => 
    index >= array.length ? 
    previousSum :
    sum( array, index + 1, previousSum + array[index] );
```

Although loops are often more performant in JavaScript than recursion, the expressive power of well written recursion if surprisingly good. We can just read the code line by line:

* Line 1: You take an array, an index starting with zero, and the previous sum starting with zero. 
* Line 2: Once you reach the end of the array...
* Line 3: ...you return the accumulated sum. 
* Line 4: Otherwise, you add one to the index, accumulate the current value of the array in the sum, and continue the iteration. 

An intermediate state of the iteration is described by the `index` and `previousSum` variables. These variables are called accumulator variables.

A> The state of the iteration can be described described using *accumulator variables* in the argument list of the function.

#### Exercises: Recursion

**Exercise 49.** Adott egy egész számokat tartalmazó tömb. Írd ki `console.log` segítségével egymás alá külön sorba a tömb elemeit. Használj rekurziót.

**Exercise 50.** Írj egy függvényt, amely kiszámol egy sorozatot. Ennek a sorozatnak az első két eleme 1 és 1. A harmadik elemtől a sorozat következő eleme az előző két elem összege. Hívjuk ezt a sorozatot *fibonacci* sorozatnak:

```
fib( 1 ) = 1
fib( 2 ) = 1
fib( 3 ) = fib( 1 ) + fib( 2 ) = 2
fib( 4 ) = fib( 2 ) + fib( 3 ) = 3
fib( 5 ) = fib( 3 ) + fib( 4 ) = 5
...
```

### While loop

It is generally harder to write iteration using functions than using built-in loops. Therefore, we will introduce the while loop:

```
while ( condition ) {
    statements;
}
```

As long as `condition` is `true`, statements are executed. These statements change the internal state of the application such that sooner or later the `condition` becomes `false`. This is when we can exit the loop.

Let's create a function that sums the values of an array:

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

#### Exercises: While loop

**Exercise 51.** Let's recall the `map` structure from a previous exercise:

```
let arr = [1, 5, 3, 1];

let map = {};

map[ arr[0] ] = true;
map[ arr[1] ] = true;
map[ arr[2] ] = true;
map[ arr[3] ] = true;

console.table( map );
```

Write a function that builds a similar map structure from an arbitrary array. Use a while loop!

**Exercise 52.** Recall the base 16 to base 10 / base 2 converter:

```
/**
 *  Prints hexadecimalValue in base 2 and base 10.
 *  
 *  @param  string    hexadecimal number in correct format
 *  @return undefined
 */
function convert( hexadecimalValue ) {
    let baseTenValue = Number.parseInt( hexadecimalValue, 16 );
    console.log(
        hexadecimalValue + ' in base 10:',
        baseTenValue,
        '\n' + hexadecimalValue + ' in base  2:',
        baseTenValue.toString( 2 )
    );
}

convert( 'ACE' )
// --> ACE in base 10: 2766
//     ACE in base  2: 101011001110
```

Rewrite the numeric base converter function such that you can enter an arbitrary base as a second argument of the convert function. Make sure the program only accepts integers greater than or equal to 2. Example:

```
convertAll( 'ACE', [12, 10, 8, 4, 3, 2] )
// --> ACE in base 12: 1726
       ACE in base 10: 2766
       ACE in base 8: 5316
       ACE in base 4: 223032
       ACE in base 3: 10210110
       ACE in base 2: 101011001110
```



### The do-while loop

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

#### Exercises: the do-while loop

**Exercise 53.** You can create a random number between 1 and 50 using the following code:

`Math.trunc( Math.random() * 50 ) + 1`

Create a function that generates a random number, and then asks the user for input between `1` and `50`. Repeat asking the user for input until the user doesn't guess a previously generated random number correctly. 

(a) Use a do-while loop
(b) Use recursion

### The for loop

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

#### Exercises: for loop 

**Exercises 54 and 55.** Recall the two exercises in the `while` loop secion. Rewrite your solutions using the for loop.

### The for..in and for..of loops

Our next simplification is the `for..in` loop. Why bother iterating an `i` variable if a loop can take care of it for us?

```
let values = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];
let sum = 0;

for ( let i in values ) {
    sum += values[i];
}

console.log( sum );
```

The `for..in` loop enumerates all the available indices of the `values` array from `0` to `12` in ascending order.

I have another simplification for you. What if I said, "why bother using a variable for iteration at all, if we could enumerate the values of the array?". In ES6, there is a loop called the `for...of` loop, which does exactly that.

```
let values = [19, 65, 9, 17, 4, 1, 2, 6, 1, 9, 9, 2, 1];
let sum = 0;

for ( let value of values ) {
    sum += value;
}

console.log( sum );
```

That's all. Go back to the editor and substitute the `for..in` and the `for..of` constructs in place of your for loop. It works exactly the same way.

We are almost done. Just two small constructs.

We can use `break` or `continue` inside the loops:

- `break` exits the closest loop it is in, and continues with the next command,
- `continue` skips out from the loop body, and jumps back to the condition of the loop.

**Example**: sum every second element of the `numbers` array:

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

#### Exercises: for..in and for..of

**Exercise 56:** Create a function that expects an array of numbers and returns the largest number in the array. Example:

```
max([19, 65, 9, 17, -99])
// --> 65

max([])
// --> null
```
