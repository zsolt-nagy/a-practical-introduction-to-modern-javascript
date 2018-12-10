## Some more operators

We will soon write conditions and loops. In these two control structures, a few operators come handy:

- `+=`, `-=`, `*=`, `/=`, `%=` etc. are abbreviations for adding a value to a variable. `a += 1` is the same as writing `a = a + 1`.
- `++x` increases the value of `x` by `1`, then returns the increased value
- `x++` returns the original value of `x`, then increases its value by `1`
- `--x` decreases the value of `x` by `1`, then returns the decreased value
- `x--` returns the original value of `x`, then decreases its value by `1`

I know, the difference between `++x` and `x++` may not make sense to you right now. I argue that in most cases, it should not even make a difference as long as you want to write readable code.

Both `x++` and `++x` have a *main effect* and a *side effect*. As a main effect, they return a value. Either `x`, or `x + 1`, depending on whether you write the `++` after the `x` or before. 

```
let a = 1;

a *= 2;  // a = a * 2;
console.log( '2++: ', a++ ); 
console.log( '--3: ', --a );
```

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

The value `NaN` was mentioned.

When formulating a condition that checks if a value is `NaN`, we have the problem that `NaN == NaN` is false. The value `NaN` does not equal to itself. How can we then check if a value is `NaN`? The answer is, use `Number.isNaN()`.

```
> Number.isNaN( NaN )
true
```

## The Spread Operator and Rest Parameters

The Spread operator and Rest parameters are two related features. Let's introduce them with an example.

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

It is not too comfortable to write this much just for a simple merge.

Let's introduce the spread operator that helps you solve the same problem faster. 

A> The spread operator *spreads* the arguments of an array as comma separated values. 

For values `v1`, `v2`, `v3`, the spread operator works as follows: `...[v1, v2, v3]` becomes `v1, v2, v3`.

At first glance, you may have some uncertainties surrounding this construct, and I fully understand why. After all, writing `...[1,2,3]` in the console gives you a syntax error:

```
> ...[1, 2, 3]
Uncaught SyntaxError: Unexpected number
```

This means, you cannot write comma separated values everywhere in your code. Let's see some basic use cases, where comma separated values can occur:

- array elements: `[1, 2, 3]`,
- function or method invocations: `Math.max(1, 2)`

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



