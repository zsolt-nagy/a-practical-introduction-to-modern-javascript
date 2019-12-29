## The Spread Operator, Destructuring, and Rest Parameters

The Spread operator, Destructuring, and Rest parameters are three related features. Let's introduce them with an example. Let's first introduce the Spread operator with an example:

### Spread Operator

We will introduce the spread operator via examples. The difference between examples and exercises is that you haven't read everything you need to solve these examples in the easiest possible way. While you can try solving these examples, please always read the reference solutions.

**Example 1**: Suppose that you have two baskets containing fruits:

```
const Basket1 = [ 'Apple', 'Pear', 'Strawberry' ];
const Basket2 = [ 'Banana', 'Peach' ];
```

Create a new array that contains all fruits that are in `Basket1` or `Basket2`.

**Solution**: First we have to create a new array.

```
const MergedBasket = [];
```

Then, we have to place the contents of `Basket1` and `Basket2` in the new array:

```
for ( let fruit of Basket1 ) {
    MergedBasket.push( fruit );
}
for ( let fruit of Basket2 ) {
    MergedBasket.push( fruit );
}
```

We can check that the result is correct:

```
> console.log( MergedBasket )
(5) ["Apple", "Pear", "Strawberry", "Banana", "Peach"]
```

It is not too comfortable to write this much just for a simple merge. Let's introduce the spread operator that helps you solve the same problem faster. 

A> The spread operator *spreads* the arguments of an array as comma separated values. 

For values `v1`, `v2`, `v3`, the spread operator works as follows: `...[v1, v2, v3]` becomes `v1, v2, v3`.

At first glance, you may have some uncertainties surrounding this construct, and I fully understand why. After all, writing `...[1,2,3]` in the console gives you a syntax error:

```
> ...[1, 2, 3]
Uncaught SyntaxError: Unexpected number
```

This means, you cannot write comma separated values everywhere in your code. Let's see some basic use cases, where comma separated values can occur:

- array elements: `[1, 2, 3]`,
- argument list of a function or method: `Math.max(1, 2)`

Regarding array elements, let's see what happens if we place the `...[1, 2, 3]` expression in an array:

```
> [...[1, 2, 3]]
[1, 2, 3]
```

We got back a flat array with the same elements. If we examine these lines a bit more deeply, you can see that this operation came with some side-effects:

```
const numbers = [1, 2, 3];
const spreadNumbers = [...numbers];

spreadNumbers[0] = 5;

console.log( spreadNumbers );  // Printed value: [5, 2, 3] 
```

What is the value of `numbers[0]`? 

```
> numbers 
(3) [1, 2, 3]
```

As you can see, `numbers[0]` is `1`, because `spreadNumbers` is not the same array as `numbers`. After the elements of `numbers` were copied to `spreadNumbers`, their elements were the same. However, The two arrays were different. We managed to make a **shallow copy** of the original array using the Spread operator. 

Making a shallow copy is a type of cloning. Cloning is a complex operation in computer science, and it is outside the scope of this introductory topic. In a later chapter, we will revisit this construct. 

A> The Spread operator can be used to make a **shallow copy** of an array. In `B = [...A]`, `B` is the shallow copy of `A`.

**Second solution of Example 1**: Now that we know how the spread operator and shallow copying works, let's recall that our task can be translated tou copying the contents of two baskets into a third basket. To solve this exercise, we need to place the shallow copy of `Basket1` and `Basket2` in the same array:

```
const Basket1 = [ 'Apple', 'Pear', 'Strawberry' ];
const Basket2 = [ 'Banana', 'Peach' ];

const MergedBasket = [ ...Basket1, ...Basket2 ];
```

No `for...of` loops are needed. The spread operator solves everything.

#### Exercises: Spread operator

**Exercise 57.** Fill in the blanks such that the result of executing this code becomes `1 7 3`. Do not use any numeric digits in your solution.

```
let A = [1, 2, 3];
let B = _____;
B[0] += 1;
console.log(
    A[0],
    B[0] + B[1] + B[2],
    B.length  
);
```

### Destructuring Arrays

Now that you know how array members can be spread, let's learn another role of the `...` operator.

Suppose array `A` is given as `[1, 2, 3, 4, 5]`. How can we retrieve the first, second, and third elements of this array one by one?

You already know the bracket notation that helps you retrieve these values:

```
const first = A[0],
      second = A[1],
      third = A[2];
```

This is a lot of writing. Fortunately, ES6 introduces a shorter way of defining these variables: a *destructuring assignment*.

```
const [first, second, third] = A;
```

The two notations are equivalent. In both cases, `first`, `second`, and `third` get the first, second, and third value from `A` respectively. The three assignments are executed in parallel as follows:

```
const [first, second, third] = A;

const [first, second, third] = [1, 2, 3, 4, 5];

const first = 1, second = 2, third = 3; // 4 and 5 are thrown away.
```

Destructuring is called destructuring, because it takes a structure on the right hand side, and destructures it such that it can assign values to the structure on the left hand side. 

**Question 1**: What happens if we are only interested in the third and the fifth elements of the array?

**Answer 1**: we can use commas to indicate that a value needs to be dropped. By placing two commas in front of the `third` variable on the left hand side describes a destructuring assignment, where the first two values are thrown away. Similarly, we can place two commas between the third and the fifth elements to make sure that the fourth value is dropped.

```
const [,,third,,fifth] = [1, 2, 3, 4, 5]

> third
3
> fifth
5
```

**Question 2**: What happens if we omit the `const` keyword in front of the above destructuring assignment?

**Answer 2**: The destructuring assignment stays valid in case `third` and `fifth` had not been defined before. The only drawback of this form is that `third` and `fifth` become *global variables*, which are discouraged in general.

```
[,,third,,fifth] = [1, 2, 3, 4, 5]  // third and fifth become globals
```

Assuming that `third` and `fifth` are declared in a block or function scope not equal to the global scope, these variables do not become globals.

```
const third, fifth;
[,,third,,fifth] = [1, 2, 3, 4, 5]
```

If only one of the variables are declared, using `const` throws a JavaScript error. 

```
let third;

> let [,,third,,fifth] = [1, 2, 3, 4, 5]
Uncaught SyntaxError: Identifier 'third' has already been declared
```

If `third` was assigned a value before, its value is reassigned by the destructuring assignment:

```
let third = -1, fifth = -1;

[,,third,,fifth] = [1, 2, 3, 4, 5]

> third
3
```

Obviously, if `third` is assigned a value as a constant, the destructuring assignment throws an error:

```
const third = 1, fifth = 2;

[,,third,,fifth] = [1, 2, 3, 4, 5]
```

**Question 3**: What happens if I place constants on the left of a destructuring assignment?

**Answer 3**: A JavaScript error is thrown. A destructuring *assignment* cannot be used for filtering. JavaScript is not Prolog, where the left hand side and the right hand side are unified. In destructuring, all we do is destructure the right hand side so that the values on the left hand side are assigned a value.

```
> const [1,,third,,fifth] = [1, 2, 3, 4, 5]
Uncaught SyntaxError: Invalid destructuring assignment target
```


**Question 4**: Can I retrieve the sixth element of an array of length `5`?

**Answer 4**: Yes. The process is similar to retrieving `A[5]`. The corresponding value becomes `undefined`.

```
const [,,,,,sixth] = [1, 2, 3, 4, 5]

> sixth
undefined
```

**Question 5**: Can I use the spread operator on the right hand side of destructuring assignments?

**Answer 5**: As the right hand side of an array destructuring assignment is an array, any operators that help build the array can be used without constraints:

```
const B = [1, 2, 3];
const [first, second,,,fifth] = [...B, 4, 5]
```

### Rest Parameter of Destructuring Assignments

Before the sixth question, let's define the *head* and the *tail* of a list. 

A> In computer science, the *head* of a list is the first element of the list. The tail of the list is a list containing all but the first element of the list in the same order as in the original list. 

In JavaScript, we represent lists as arrays.  The head of `A` is `1`. The tail of `A` is `[2, 3, 4, 5]`. 

**Question 6**: Can I use the spread operator on the left hand side of destructuring assignments?

**Answer 6**: No. On the left hand side, the `...` operator may only be used to define a *rest parameter*. Consequently, the name of the `...` operator in this position is *rest operator*, as the role of this operator is not spreading values, but collecting them. The rest parameter collects all the remaining values of the array on the right hand side of the destructuring assignment. No arguments may follow a rest parameter:

```
const [head, ...tail] = [1, 2, 3, 4, 5]

> head
1
> tail
[2, 3, 4, 5]
```

The following assignment is invalid:

```
> [...rest,] = [1, 2, 3, 4, 5]
Uncaught SyntaxError: Rest element must be last element
```

If all the elements of an array are consumed before reaching a rest parameter, the value of the rest parameter becomes `[]`:

```
[,,,,,,,,,,,,,...rest] = [1, 2, 3, 4, 5]

> rest
[]
```

#### Exercises: Destructuring

**Exercise 58.** Swap the following two variables using one assignment:

```
let swap = 'swap';
let me = 'me';
```

**Exercise 59.** Create one destructuring assignment inside the for loop that helps you calculate the nth Fibonacci number. Reminder:

- `fib( 1 ) = 1`
- `fib( 2 ) = 1`
- `fib( n ) = fib( n-1 ) + fib( n-2 )`;

```
function fib( n ) {
    let fibCurrent = 1;
    let fibLast = 1;  

    if ( n <= 2 ) return n;

    for ( let fibIndex = 1; fibIndex < n; ++fibIndex ) {
        // Ide illessz be egy destrukturáló kifejezést
    }

    return fibCurrent;
}
```

**Exercise 60.** What variable values does the following expression create?

```
let node = { left : { left: 3, right: 4 }, right: 5 };

let { loft, right : val } = node;
```

### Function Rest Parameter and Array Destructuring

In the upcoming example, we use the `...` operator as *rest parameters*. Rest parameters behave in a slightly more constrained way than the spread operator spreading the values of an array into comma separated values. This difference can be illustrated by the following two functions:

- `const invalidFunction = function( ...args, lastArgument ) { /* ... */ }`
- `const validFunction = function( firstArgument, ...args ) { /* ... */ }`

In theory, both functions accept a variable number of arguments. Suppose we call them with the argument list `1, 2, 3`. 

In case of `invalidFunction`, determining the argument values is not possible.

```
> let [ ...args, lastArgument ] = [1, 2, 3]  
Uncaught SyntaxError: Rest element must be last element

> const invalidFunction = function( ...args, lastArgument ) {}
Uncaught SyntaxError: Rest parameter must be last formal parameter
```

Both in the destructuring exercise and in the function definition, `...` symbolizes a *rest parameter*. Rest parameters may only occur at the end of an array. Consequently, in a function argument list, the `...` rest parameter may only occur at the end of the argument list of the function. When violating this rule, a `SyntaxError` is thrown.

In case of `validFunction`, we have an easy task to determine the argument values:

```
let [ firstArgument, ...args ] = [ 1, 2, 3 ]

> firstArgument
1
> args
[2, 3]
```

Notice that calling a function is a *destructuring* assignment. The left hand side of the destructuring assignment is the argument list of the function definition. The right hand side is consists of the argument list the function is called with. On the left hand side of a destructuring assignment, the `...` operator is used to describe a *rest parameter*. 

**Example**: Write a function that accepts a variable number of arguments. Each argument should be a number. The return value of the function is the difference of the largest and smallest argument value. 

**Solution**: We will use rest parameters to describe this function.

```
const maxMinDifference = function( ...args ) {
    let min = args[0], max = args[0];
    for ( let value of args ) {
        if ( value < min ) min = value;
        if ( value > max ) max = value;
    }
    return max - min;
}

> maxMinDifference( 19, 65, 9, 17 );
56
```

### Exercises: Function Rest Parameter and Array Destructuring

**Exercise 61.**: Create a function that prints all its arguments one by one such that each argument is printed on a different line. Whenever the argument list is empty, the value `undefined` is printed. Use recursion and rest parameters!
