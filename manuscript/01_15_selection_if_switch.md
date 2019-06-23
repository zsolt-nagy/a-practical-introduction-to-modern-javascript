## Selection in Depth: if-else and switch 

The time has come, when we can fit the puzzle pieces together. You have learned about different primitive and composite types. You know how to check these types. You know the basic functions and arithmetic (addition, subtraction, multiplication etc.) and logical (true or false) operations in JavaScript.

There are only two things missing.

So far, we can write a sequence of instructions that perform a calculation. In software development, there are three types of control structures:

- sequence: writing instructions one after the other
- selection: either execute one set of instructions, or another
- iteration: execute a set of instructions a finite or infinite number of times

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

It is possible to have more than two `else if` branches. Also note that `statement_after_if_else;` is executed right after entering any of the branches in the `if-else if-else if-else` construct.

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

When there is only one statement after an `if` statement, the use of braces is not mandatory:

```
if ( condition ) statement;
```

Generally, the usage of braces is highly recommended due to readability reasons.

Some common beginners errors about if statements:

**1. six lines instead of one for a simple assignment**

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

Some developers who think of themselves as more advance, prefer double negation:

```
let value = !!condition;
```

**2. Unnecessary nesting of if statements**

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

**3. Wrong formatting by avoiding braces**

The below code is dangerously misleading:

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

This is why it is not a good idea to avoid braces in an if statement.

**4. Erroneous negation**

- `!(red && green)`: *not red and green*, a.k.a. *not (red and green)
- `!red && !green`: *not red and not green*

Some beginner developers tend not to notice the difference between the two forms. In reality, the difference is big:

```
red    green   !(red && green)  !red || !green
false  false   true             true
false  true    true             false
true   false   true             false
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

For instance, if you say, the lamp state is "not (red and yellow)", the statement is equivalent to: "the lamp state is not red or not yellow". Most people, especially non-developers say "the lamp state is not red and not yellow", which is an incorrect translation of the original statement.

This small, but significant difference can be a source of huge errors.

### switch statement

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

That's all for selection. In the next subsection, let's see one way to perform iteration.
