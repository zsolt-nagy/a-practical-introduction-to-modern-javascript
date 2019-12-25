## Selection in Depth: if-else and switch

The time has come, when we can fit the puzzle pieces together. You have learned about different primitive and composite types. You know how to check these types. You know the basic functions and arithmetic (addition, subtraction, multiplication etc.) and logical (true or false) operations in JavaScript.

There are only two things missing.

So far, we can write a *sequence of instructions* that perform a calculation. In software development, there are three types of control structures:

- *sequence*: writing instructions one after the other
- *selection*: either execute one set of instructions, or another
- *iteration*: execute a set of instructions a finite or infinite number of times

### if statement

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

We now know everything to write the `printNumber` function:

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
        console.log( 'Amber' );
    } else if ( state === 3 ) {
        console.log( 'Green' );
    } else {
        console.log( 'Wrong lamp state' );
    }
}
```

The beauty of the above code is that you can read it as if it was plain English. If the state is 1, then log Red. Otherwise if the state is 2, then log Yellow. And so on.

The generic form of an `if-else if-else` statement is as follows:

```
if ( condition1 ) {
    statements1;
} else if ( condition2 ) {
    statements2;
} else if ( condition3 ) {
    statements3;
} else {
    statements4;
}
statement_after_if_else;
```

It is possible to have more than two `else if` branches. Also note that `statement_after_if_else;` is executed right after entering any of the branches in the `if-else if-else if-else` construct. Interpret the code as follows:

- If `condition1` is truthy, then `statements1` is executed. Then we exit from the long `if-else` statement, and run `statements_after_if_else`.
- If `condition1` is falsy, but `condition2` is truthy, then we run `statements2`. Afterwards, we exit from the long `if-else` statement, and run `statements_after_if_else`.
- If `condition1` and `condition2` are both falsy, but `condition3` is truthy, then we run `statements3`. Afterwards, we exit from the long `if-else` statement, and run `statements_after_if_else`.
- If you reach this point, `condition1`, `condition2`, and `condition3` are all falsy. This branch describes all other cases and runs `statements4`. Then we exit the `if-else` statements, and run `statements_after_if_else`.

The else branch is never necessary. For instance, the following construct is perfectly valid:

```
if ( condition1 ) {
    statement1;
    statement2;
} else if ( condition2 ) {
    statement3;
    statement4;
}
```

When there is only one statement after an `if` statement, the use of braces is not mandatory. For instance, suppose you are writing a function that displays a message on screen:

```
function displayMessage( message ) {
    if ( typeof message !== 'string' ) return;
    // display the string message
}
```

When we verify the input arguments, often times it is worth creating single line `if` statements to exit from the function in case of invalid input. The typical form of these exit conditions is as follows:

```
if ( condition ) statement;
```

We will soon talk about some common mistakes beginner developers make. The above format is often desirable, because it avoids the beginner mistake number `3`, writing a second statement indented after the `if` statement.

Let's see another example for an exit condition:

```
function countdown( num ) {
    if ( typeof num !== "number" || num <= 0 ) return;
    console.log( num );
    countdown( num - 1 );
}

> countdown( 3 )
3
2
1
```

In the first line of the function body, we exit from the function whenever `num` is not a positive number. If `num` is a positive number, we print its value, and we call the same `countdown` function, with a value one less than the current value of `num`. We will talk about this technique later. At this stage, let's concentrate on the exit condition on the first line. We used just one line for the same exit condition that could have required three lines with braces:

```
function countdown( num ) {
    if ( typeof num !== "number" || num <= 0 ) {
        return;
    }
    console.log( num );
    countdown( num - 1 );
}
```

In both cases, it is mandatory to have an exit condition in the `countdown` function, not only because of verifying the input, but also because this is the only way to terminate an infinitely long iteration. If we don't give ourselves a way to exit, we run around the same loop forever. At least in theory. In practice, a *stack overflow* error terminates the program after a given number of iterations.  

Generally, the usage of braces is highly recommended due to readability reasons.

Some common beginners errors about if statements:

#### 1. six lines instead of one for a simple assignment

Let's introduce this mistake with an example. Suppose we ask the user to enter a number. As text user input is always in string format, we convert this string to a number. Then we call a function that prints if this value is greater than 100.

```
let input = prompt( 'Enter a number:' );
let num = Number.parseInt( input, 10 );
console.log( isGreaterThanHundred( num ) );
```

**Remark:** if `input` is not a number, then `Number.parseInt` returns `NaN`. The `NaN` value is not greater than `100`.

Let's write the `isGreaterThanHundred` function. Its return value is `true` whenever `num` is greater than `100`. Otherwise, the return value is `false`.

```
function isGreaterThanHundred( num ) {
    if ( num > 100 ) {
        return true;
    } else {
        return false;
    }
}
```

For the sake of this explanation, let's create a `returnValue` variable, and place this value after the `if-else` statement:

```
function isGreaterThanHundred( num ) {
    let returnValue;

    if ( num > 100 ) {
        returnValue = true;
    } else {
        returnValue = false;
    }

    return returnValue;
}
```

Let's examine the value of `returnValue`:

- `returnValue` is `true`, whenever `num > 100` is `true`
- `returnValue` is `false`, whenever `num > 100` is `false`

In other words, `returnValue` is nothing else but the value of the boolean expression `num > 100`:

```
function isGreaterThanHundred( num ) {
    let returnValue;

    returnValue = num > 100;

    return returnValue;
}
```

The two versions are equivalent. Obviously, we can continue simplifying the three statements in the function body and writing a one liner `return num > 100;`. However, the point of this section is not to simplify the function further. The point is that we can simplify if-else statements of the following form:


```
let value;
if ( condition ) {
    value = true;
} else {
    value = false;
}
```

If `condition` is a boolean value, the above code can be substituted by just one assignment:

```
let value = condition;
```

If `condition` is not a boolean value, you can use `Boolean` or double negation to convert it to a boolean. Using `Boolean` is more descriptive, especially for beginners.

Using `Boolean`:

```
let value = Boolean( condition );
```

**Examples:**

```
> Boolean( 0 )
false

> Boolean( 1 )
true

> Boolean( 2 )
true

> Boolean( "" )
false

> Boolean( " " )  // non-empty string
true

> Boolean( undefined )
false

> Boolean( {} )
true
```

Double negation can also be used instead of the `Boolean` constructor:

```
let value = !!condition;
```

**Examples:**

```
> !!0
false

> !!1
true

> !!2
true

> !!""
false

> !!" "  // non-empty string
true

> !!undefined
false

> !!{}
true
```

To make your code more readable, I suggest avoiding double negation and explicitly using the `Boolean` constructor.

#### 2. Unnecessary nesting of if statements

**Example**: Suppose a variable `num` is given. If this variable contains a number, perform the following operation: write the text `"even"` if `num` is even.

Our first solution translates the text to code word by word, line by line:

```
if ( typeof num === "number" ) {
    if ( num % 2 === 0 ) {
        console.log( "páros" );
    }
}
```

Note that the nested `if` statements are not necessary. We can also write them in one statement:

```
if ( typeof num === "number" && num % 2 === 0 ) {
    console.log( "páros" );
}
```

**Remark:** here we took advantage of the *shortcut* property of Boolean expressions. If `A` is false in an `A && B` expression, then the whole expression becomes false, *without evaluating the value of `B`*. In other words, if `num` is not a number, then we don't even evaluate the `num % 2 === 0` expression.

**Summary:**

```
if ( condition1 ) {
    if ( condition2 ) {
        statement;
    }
}
```

While the above code is syntactically correct, notice we can just join the two statements with the and operator:

```
if ( condition1 && condition2 ) {
    statement;
}
```

#### 3. Wrong formatting by avoiding braces

The below code is dangerously misleading, especially for those familiar with Python:

```
if ( condition )
    statement1;
    statement2;
```

In reality, the above code is translated to this:

```
if ( condition ) {
    statement1;
}
statement2;
```

If you are learning Python, this code may surprise you, because in Python, indentation can form blocks of code just like how braces form blocks in JavaScript. Bear in mind that in JavaScript, whitespace characters bear little role in structuring your code.

**Example:** suppose an inexperienced developer wrote the following code:

```
function logInput( value ) {
    if ( typeof value !== "string" )
        console.warn( "Wrong input", value );
        return;
    console.log( "The input was: ", value );  
}
```

The developer meant that for non-string values, we print a warning message and exit from the function. For string inputs, we log the value.

In reality, the code is translated as follows:

```
function logInput( value ) {
    if ( typeof value !== "string" ) {
        console.warn( "Wrong input", value );
    }
    return;
    // unreachable code
    console.log( "The input was: ", value );  
}
```

This means, the last `console.log` line becomes unreachable, and the input is never logged.

This is why it is not a good idea to avoid braces in an if statement. The only exception is the previously mentioned exit condition:

```
if ( condition ) statement;
```

Here, it is intentionally hard to write another statement indented in such a way that software developers may think the new statement belongs to the body of the if statement.

#### 4. Erroneous negation

Suppose we have a red and a yellow lamp. We model their state using Boolean values: if the value of the lamp is `true`, it is turned on. If the value of the lamp is `false`, it is turned off.

**Task:** write Boolean expressions to model the following states:

1. The red and the yellow lamps are both on.
2. The red or the yellow lamp is on.
3. The red and the yellow lamps are not on simultaneously.
4. Either the red lamp is off, or the yellow lamp is off.
5. It is not true that the red or the yellow lamp is on.
6. Neither the red, nor the yellow lamps are on.

We will refer to the red and yellow lamps with the variables `red` and `yellow` respectively.

**Solution**:

**Part (1)** is easy, because the text can be directly translated to the value of `red && yellow`. If we used this expression in an `if` statement, we would write the following:

```
if ( red && yellow ) {
    // ...
}
```

**Part (2)** describes the `red || green` condition. *Note that the or-expression contains the case when both the red and the yellow lamps are on*.

To avoid ambiguity, think of the or-expression as a relation between the inputs and the output such that the output is true whenever at least one of the inputs are true.

The expression can be written in the following way in an `if` statement:

```
if ( red || yellow ) {
    // ...
}
```

The last four points are more difficult. As long as you cannot write conditions as if they were your reflexes, your friend is a tool called the *truth table*. A truth table gives you the result belonging to each possible input combinations.

For instance, let's see the truth table of `red && yellow`. We will need it later. In order for `red && yellow` to be `true`, we need both inputs to be true. Based on this information, fill out the outputs of the following truth table:

```
    Inputs      |     Output
red     yellow  | red && yellow
----------------|----------------
false   false   | _____
false    true   | _____
 true   false   | _____
 true    true   | _____
```

You will soon read the correct solution. Before that, let's construct the truth table of the `OR` operator (`||` in JavaScript). The value of `red || yellow` is true whenever at least one of the two inputs, `red` or `yellow`, are true. Based on this information, fill out the outputs of the following truth table:

```
    Inputs      |     Output
red     yellow  | red || yellow
----------------|----------------
false   false   | _____
false    true   | _____
 true   false   | _____
 true    true   | _____
```

Let's now see the solutions. The truth table of the `and` relationship only contains one row with a `true` output: the output is only `true` if both inputs are true:

```
    Inputs      |     Output
red     yellow  | red && yellow
----------------|----------------
false   false   | false
false    true   | false
 true   false   | false
 true    true   |  true
```

The truth table of the `or` relationship contains three `true` rows, as our condition is that at least one of the inputs should be true:

```
    Inputs      |     Output
red     yellow  | red || yellow
----------------|----------------
false   false   | false
false    true   |  true
 true   false   |  true
 true    true   |  true
```

Let's recall the following sentence: *Note that the or-expression contains the case when both the red and the yellow lamps are on*. In English, the word *or* is often used in an *exclusive* sense. For instance, "we can either eat chocolate or mango ice cream." Chances are, if a human hears this statement, they may think they have to choose between the two and they don't even consider that they can get both ice cream flavors. In computer science, the `||` (or) expression also covers the possibility of a `true` value for both inputs.

In order to fully understand boolean logic, we need one more truth table: negation.

```
Input  | Output
 red   | !red
-----------------
false  | true
 true  | false
```

Negation is easy. If the input is `true`, the output is `false`. If the input is `false`, the output is `true`.

**Part (3)** states that "the red and the yellow lamps are not on simultaneously". As this statement looks harder to model than the previous ones, let's start with the truth table. The expression belonging to part **(3)** is `true` whenever at least one of the inputs is `false`:

```
    Inputs      | Output
red     yellow  | (3)
----------------|----------------
false   false   |  true
false    true   |  true
 true   false   |  true
 true    true   | false
```

Let's compare the truth table of **(3)** and **(1)**:

```
    Inputs      | (1)           | (3)
red     yellow  | red && yellow |
----------------|----------------------
false   false   | false         |  true
false    true   | false         |  true
 true   false   | false         |  true
 true    true   |  true         | false
```

We can conclude that (3) is the negation of (1):

- (3) is `true` whenever (1) is `false`
- (3) is `false` whenever (1) is `true`

**Remark:** let's recall the truth table of negation. The output is the inverse of the input. Here (1) can be regarded as the input, while (3) is the output.

If we wrote some JavaScript code:

```
let firstStatement = red && yellow;

let thirdStatement = !firstStatement;
```

Let's substitute the value of `firstStatement` in the expression `!firstStatement`. The result is:

```
let thirdStatement = !( red && yellow );
```

If we used this statement in a condition of an `if` statement, we would get the following:

```
if ( !( red && yellow ) ) {
    // ...
}
```

**Part (4)**: "Either the red lamp is off, or the yellow lamp is off." Let's construct the boolean expression first this time:

- `!red`: the red lamp is off
- `!yellow`: the yellow lamp is off
- `!red || !yellow`: either the red lamp is off or the yellow lamp is off (or both are off)

In a JavaScript `if` statement:

```
if ( !red || !yellow ) {
    // ...
}
```

Let's see the truth table of expression **(4)**:

```
    Inputs      |   Output (4)
red     yellow  | !red || !yellow
----------------|----------------
false   false   |  true
false    true   |  true
 true   false   |  true
 true    true   | false
```

Is this truth table familiar? That's it. This is the truth table of expression **(3)**.

What does this imply?

This implies that expressions **(3)** and **(4)** are equivalent:

- `!( red && yellow )`
- `!red || !yellow`

One way to describe this equivalence is the following:

- If we look at the last line of the truth table, we get the statement: "it is not true that both red AND yellow are on".
- If we look at the first three lines of the truth table, we get the statement: "either red is off or yellow is off (or both are off)".

**Part (5)**: "It is not true that the red or the yellow lamp is on." Note that by saying "it is not true that", we negate whatever we write after it. In this case, we are negating that "the red or the yellow lamp is on".

Therefore, we need to negate `red || yellow`:

```
if ( !( red || yellow ) ) {
    // ...
}
```

This is what the corresponding truth tables look like:

```
 red    yellow  red || yellow  !( red || yellow )
-------------------------------------------------
false   false | false         |  true
false   true  |  true         | false
 true   false |  true         | false
 true   true  |  true         | false
```

This condition succeeds whenever none of the lamps are on. This is what condition (6) describes:

**Part (6):** "Neither the red, nor the yellow lamps are on". Using a JavaScript expression: `!red && !yellow`.

```
if ( !red && !yellow ) {
    // ...
}
```

As expressions **(5)** and **(6)** are equivalent, we can conclude that:

- `!( red || yellow)`
- `!red && !yellow`

are the same.

---

We can conclude that the exact wording is very important. Some beginner software developer, most business people, and many product managers cannot tell the subtle difference between some of the above statements. Often times the words "and" and "or" are interchanged. Therefore, being a software developer is a responsibility: often times the software developer points out these inconsistencies in the specification of a request.

Let's recall these expressions:

- `!(red && green)`: *not red and green*, a.k.a. *not (red and green)*
- `!red && !green`: *not red and not green*

Some beginner developers tend not to notice the difference between the two forms. In reality, the difference is big:

```
red    green   !(red && green)  !red && !green
               !red || !green   !(red || green)
false  false    true             true
false  true     true            false
true   false    true            false
true   true    false            false
```

Compare the above expressions with their negations:

```
red    green   red && green   red || green
false  false   false          false
false  true    false          true
true   false   false          true
true   true    true           true
```

We can conclude that

- `!(red && green)` is the negation of `red && green`
- `!red || !green` is the negation of `red || green`

In general, you can always refer to the *de Morgan* equalities for negation:

- `not( A and B ) = not( A ) or not( B )`,
- `not( A or B ) = not( A ) and not( B )`.

Remember, when you move negation inside or outside in an expression, *and* changes to *or*, and *or* changes to *and*.

For instance, if you say, the lamp state is "not (red and yellow)", the statement is equivalent to: "the lamp state is not red or not yellow". Most people, especially non-developers say "the lamp state is not red and not yellow", which is an incorrect translation of the original statement. If you can't see the difference yet, not a problem. Review the above truth tables, and you will sooner or later understand the details.

This small, but significant difference can be a source of huge errors.

---

**Example:** Let's model another statement: "The red lamp is on or the yellow lamp is off".

**Solution:**

- "Red lamp is on" is true if `red` is `true`
- "Yellow lamp is off" is true if `yellow` is `false`, i.e. `!yellow` is `true`
- There is an *or* between the two statements, so the end result is `red || !yellow`.

As we have not modeled a statement like this, it is worth filling out a truth table. First, fill out the output values:

```
    Inputs      |   Output
red     yellow  | red || !yellow
----------------|----------------
false   false   | _____
false    true   | _____
 true   false   | _____
 true    true   | _____
```

- Wherever `red` is `true`, the output is also `true`. Therefore, the third and the fourth lines of the truth table contain a `true` output.
- Wherever `yellow` is `false`, the output is `true`. Therefore, the first and the third lines of the truth table have a `true` output.

```
    Inputs      |   Output
red     yellow  | red || !yellow
----------------|----------------
false   false   |  true
false    true   | false
 true   false   |  true
 true    true   |  true
```

Observing the second line, we know that it is not true that `red` is `false` and `yellow` is `true`:

```
!( !red && yellow )
```

Using the *de Morgan* rule:

- `!( A && B )` becomes `!A || !B`
- `A` is `!red`
- `B` is `yellow`

Substituting the values of `A` and `B`:

```
!( !red && yellow ) ---> !!red || !yellow
```
Substituting `!!red` with `red`:

```
red || !yellow
```

We can also derive the same result from the three `true` statements:

- Both `red` and `yellow` are `true`
- `red` is `true` and `yellow` is `false`
- `red` is `false` and `yellow` is `false`

There is an OR relationship between the above three statements:

```
(red && yellow) || (red && !yellow) || (!red && !yellow)
```

Notice that the first two terms can be simplified:

```
(red && yellow) || (red && !yellow)
```

becomes

```
red && (yellow || !yellow)
```

As `(yellow || !yellow)` is universally `true`, the expression becomes `red`.

Subsituting `red` in place of the first two terms, we get:

```
red || (!red && !yellow)
```

Here, think a bit more:

- if `red` is `true`, the whole expression is `true` without evaluating the right hand side
- if `red` is false, the right hand side is evaluated: `!red && !yellow` becomes `!false && !yellow`, which in turn becomes `!yellow`

So after the simplifications, we are left off with the same expression as before: `red && !yellow`.

You may ask, what does all this have to do with programming? Why do I have to read this stuff?

The answer is simple: when you write an `if` statement, which format would you prefer?

```
if ( red && !yellow ) {
    // ...
}
```

or

```
if ( (red && yellow) ||
     (red && !yellow) ||
     (!red && !yellow) ) {
    // ...
}
```

If you prefer simplicity, it might be useful to double down on simplifying logical expressions.

---

In some cases, logical expressions containing multiple terms cannot be simplified further.

 **Example:** Let's examine the statement "When looking at the red and the yellow lamps, exactly one lamp is on." Formulate a boolean condition.

Although this statement contains an and, this statement has nothing to do with the logical and. Let's write the truth table of this expression:

```
    Inputs      |   Output
red     yellow  | exactly one is on
----------------|------------------
false   false   | false
false    true   |  true
 true   false   |  true
 true    true   | false
```

Using the method used in the previous example, we can either

1. enumerate the `true` rows and join their corresponding boolean expressions with an `||`,
2. enumerate the `false` rows, join their corresponding boolean expressions with an `||`, and then negate the end result

We will do the former approach. As an exercise,  do the second approach yourself, and conclude that the two forms are equivalent.

The second and the third rows are `true`:

- Second row: `!red && yellow`
- Third row: `!yellow && red`

Joining the two expressions:

```
if ( (!red && yellow) || (!yellow && red) ) {
    // ...
}
```

**Remark:** this expression is the exclusive or operation. In JavaScript, the exclusive or (XOR) logical operation does not have a symbol.

Using just logical expressions, `&&`, `||`, and negation, it is not possible to simplify this value further in JavaScript.

This does not mean though, that you should use the above complex statement in logical expressions. A simple implementation is counting the on states:

```
let count = 0;
if ( red ) {
    count += 1;
}
if ( yellow ) {
    count += 1;
}
if ( count === 1 ) {
    // ...
}
```

This is a bit too verbose, so we can simplify using the ternary operator:

```
let count = ( red ? 1 : 0 ) + ( yellow ? 1 : 0 );
if ( count === 1 ) {
    // ...
}
```

There are still gains to be made. Look at the truth table of this expression. Clearly analyze the `true` rows and the `false` rows. What can you see?

```
    Inputs      |   Output
red     yellow  | red XOR yellow
----------------|------------------
false   false   | false
false    true   |  true
 true   false   |  true
 true    true   | false
```

- When the output is `true`, the inputs are `______`.
- When the output is `true`, the inputs are `______`.

Fill in the blanks. I will soon reveal the answer so that you can verify if you are on the right track. But first, if you have found an answer, try to fill in the blanks and formulate a simple condition that's true whenever the output of the above truth table is true:

```
if ( _____ ) {
    // ...
}
```

**Fill in the blanks solution**: notice that the inputs are different in the second and in the third row. Therefore, when the output is `true`, the inputs are different. So different is the value of the first blank. The second blank should contain a phrase that indicates that the output is false whenever the inputs are the same.

Regarding the third blank, the condition should describe that the inputs are different. A simple condition that describes this is `red != yellow`.

### Exercises: if-else

**Exercise 44.** Write a function that returns the maximum of two numbers.

```
max2( 1, 2 )
// --> 2
max2( 2, 1 )
// --> 2
```

**Exercise 45.** Create a random number between `1` and `50` using the following expression:

```
Math.trunc( Math.random() * 50 ) + 1
```

Write a function that requests the user to enter a number between `1` and `50`. Depending on the value entered by the user, the program prints one of the following messages:

- "Your guess is too low. Try again!"
- "Your guess is too high. Try again!"
- "The correct result is 36." (assumint 36 is the correct answer)
- "Your guess should be between 1 and 50. Try again!"
- "Invalid format. Try again!"

Help: The `prompt( "question: " )` command writes its argument, and asks the user to enter a value in a textfield. The return value of `prompt` is the string typed by the user.


### switch statement

There is an abbreviated version for a long chain of if-else statement: the `switch` operator. Switch is like a telephone operator. It puts you through some code in case the correct value is stored in your variable. There is also a default line, saying "the number you have dialed is invalid".

```
function logLampColor( state ) {
  switch( state ) {
    case 1:
      console.log( 'Red' );
      break;
    case 2:
      console.log( 'Amber' );
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
            return 'Amber';
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
           state == 2 ? 'Amber' :
           state == 3 ? 'Green' :
           'Error';
}
```

Some people don't like this way of writing code. You can hit up their rant about how awful this construct is under the name of *ternary operator abuse*. I personally do not share their opinion, but this does not matter. If you believe you should use it, use it.

### Exercises: switch

**Exercise 46.** Rewrite the following code using a `switch` statement and cases:

```
if ( a == 1 ) {
    console.log( 'One' );
} else if ( a == 2 ) {
    console.log( 'Two' );
} else if ( a == 3 ) {
    console.log( 'Three' );
}
```

**Exercise 47.** Rewrite the following code using a `switch` statement and cases:

```
if ( a > 0 ) {
    console.log( 'Positive' );
} else if ( a < 0 ) {
    console.log( 'Negative' );
} else {
    console.log( 'Zero' );
}
```

**Exercise 48.** Convert the following code to an equivalent version without using `switch`. Hint: you can use `if-else` statements, the ternary operator, or even function calls.

```
let state = 2;

switch( state ) {
    case 1:
        console.log( 'One' );
        break;
    case 2:
    case 3:
        console.log( 'Two or Three' );
    case true:
        console.log( 'True' );
        break;
    default:
        console.log( 'Default' );
}
console.log( 'Done' );
```
