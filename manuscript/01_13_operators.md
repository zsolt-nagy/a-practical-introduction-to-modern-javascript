## Some more operators

We will soon write conditions and loops. In these two control structures, a few operators come handy:

- `+=`, `-=`, `*=`, `/=`, `%=` etc. are abbreviations for adding a value to a variable. `a += 1` is the same as writing `a = a + 1`.
- `++x` increases the value of `x` by `1`, then returns the increased value
- `x++` returns the original value of `x`, then increases its value by `1`
- `--x` decreases the value of `x` by `1`, then returns the decreased value
- `x--` returns the original value of `x`, then decreases its value by `1`

Examples:

```
let a = 1;

a *= 2;            // a = a * 2;
console.log( a );  // 2

a += 1;            // a = a + 1;
console.log( a );  // 3

a %= 2;            // a = a % 2;
console.log( a );  // 1

++a;               // If ++a is not on the right hand side of an asignment,
                   // its effect is the same as writing a = a + 1;
console.log( a );  // 2

a++;               // If a++ is not on the right hand side of an assignment,
                   // its effect is the same as writing a = a + 1;
console.log( a );  // 3

--a;               // If --a is not on the right hand side of an asignment,
                   // its effect is the same as writing a = a - 1;
console.log( a );  // 2

a--;               // If a-- is not on the right hand side of an asignment,
                   // its effect is the same as writing a = a - 1;
console.log( a );  // 1
```

I know, the difference between `++x` and `x++` may not make sense to you right now. I argue that in most cases, it should not even make a difference as long as you want to write readable code.

Both `x++` and `++x` have a *main effect* and a *side effect*. As a main effect, they return a value. Either `x`, or `x + 1`, depending on whether you write the `++` after the `x` or before.

```
let a, aplusplus, plusplusa;

a = 1;
aplusplus = a++;
console.log( "a: ", a, "aplusplus: ", aplusplus );
// a:  2 aplusplus:  1

a = 1;
plusplusa = ++a;
console.log( "a: ", a, "plusplusa: ", plusplusa );
// a:  2 plusplusa:  2
```

The `a++` expression first returns the original value of `a`. This original value is stored in the `aplusplus` variable. Then, as a side effect, the expression increases the value of `a` by `1`.

The `++a` expression first executes its side effect by increasing the value of `a` by `1`. Then the main effect of `++a` is executed, which is the returning of the increased value. This increased value is stored in the `++a` variable.

The same code can be written without relying on any side effects:

```
let a, aplusplus, plusplusa;

a = 1;
aplusplus = a;
a = a + 1;      // or: a += 1;
console.log( "a: ", a, "aplusplus: ", aplusplus );
// a:  2 aplusplus:  1

a = 1;
a = a + 1;      // or: a += 1;
plusplusa = a;
console.log( "a: ", a, "plusplusa: ", plusplusa );
// a:  2 plusplusa:  2
```
The below code illustrates the sequence in which the main effect and the side effect of these operations are executed:

```
y = x++;  // First (main effect):  y = x;
          // Second (side effect): x = x + 1;

y = ++x;  // First (side effect):  x = x + 1;
          // Second (main effect): y = x;

y = x--;  // First (main effect):  y = x;
          // Second (side effect): x = x - 1;

y = --x;  // First (side effect):  x = x - 1;
          // Second (main effect): y = x;
```

Let's see another example:

```
let a = 1;

a *= 2;  // a = a * 2;
console.log( '2++: ', a++ );
console.log( '--3: ', --a );
```

The side effect of `a++` and `++a` is that they increase the value of `x` after returning a value, or before returning a value respectively. Notice that in the above example, the first console log prints the value of `2++`, which is `2`. After this line is terminated, and before the next line is started, the value of `a` becomes `3` due to the side effect. Then we print the value `--3`, which is `2`. The side effect of `--a` is that the value of `a` got decreased by `1` before the returned value got printed.

There are two more operators that come handy when formulating boolean conditions.

Suppose you are checking whether a variable is an array **and** it has a positive length. The and conjuncion is denoted by the `&&` operator:

```
function isNonEmptyArray( x ) {
    return Array.isArray( x ) && x.length > 0;
}

> isNonEmptyArray( 5 )
false
> isNonEmptyArray( [] )
false
> isNonEmptyArray( [1] )
true
```

The value `5` is not an array, so `Array.isArray( 5 )` becomes `false`. A `false` value in conjunction with anything is false:

```
> false && false
false
> false && true
false
```

Therefore, the second operand of the `&&` operator is not even executed. This is good, because `5.length` would have *thrown an error*. We can rely on the `&&` operator not executing the right hand side expression in case the left side is evaluated as `false`. This simplification is called a *shortcut*.

If the left hand side is true, the right hand side is executed. In this case, the value of the `and` expression becomes the value of the right hand side expression:

```
> true && false
false
> true && true
true
> true && 'value'
'value'
```

We can also define an **or** relationship between operands. For instance, suppose we have a function that returns true for numbers and strings:

```
function numberOrString( x ) {
    return typeof x === 'number' || typeof x === 'string'
}

> numberOrString( NaN )
true
> numberOfString( '' )
true
> numberOrString( null )
false
```

The or operator works as follows: in case of `a || b`, if `a` is `true`, then `b` is not even evaluated. This is the *or shortcut*. Once we know that a variable is a number, we don't have to check if the same variable is a string too. We already know that the function should return `true`.

Example for shortcut: if we know that a variable contains a number, then it is useless to check if the type of the value stored in the same variable is a string. Once we know it is a number, the `numberOrString` function can safely return the result.

The value of `a || b` is true, whenever:

- `a` is truthy. In this case, `b` is not even evaluated.
- `a` is falsy and `b` is truthy.

Why is evaluation important? Because `a` and `b` can be expressions with side effects. These side effects are only executed if we evaluate the expressions they are in.

The value `NaN` was mentioned previously.

When formulating a condition that checks if a value is `NaN`, we have the problem that `NaN == NaN` is false. The value `NaN` does not equal to itself. How can we then check if a value is `NaN`? The answer is, use `Number.isNaN()`.

```
let notNumber = NaN;

> notNumber == NaN
false

> Number.isNaN( notNumber )
true
```

### Exercises: Operators

**Exercise 41:** Without running the code, determine what is written to the console:

```
// A. ternary operator
let a = 3;
console.log( a%2 ? 'one' : 'zero' );

// B. side effects
++a;
a *= 3;
a %= 5;

// C. shortcut
a > 2 && console.log( 'Is this line written to the console?' );
a > 2 || console.log( 'What about this one?' );
```

**Exercise 42:** Write the following conditions as JavaScript boolean expressions.

A. The value of the `age` variable should be at least `18`
B. The value of the `age` variable should be between `20` and `30`, including the values `20` and `30`
C. The value of the `age` variable cannot be between `20` and `30`. It cannot be `20` and cannot be `30`.
D. The value of the `age` variable cannot be even.
E. The value of the `age` variable has two digits, and the first digit is smaller than the second digit. Hint: the `Math.floor` function accepts a floating point number and returns the truncated value of this number, where we get rid of the fractional part of the number. For instance, `Math.floor( 1.8 )` is `1`.

**Exercise 43:** Determine the main effect and side effects of the expressions in front of the comments `A` and `B`:

```
let condition = true;

condition && console.log( 'A' ); // A
condition || console.log( 'B' ); // B
```
