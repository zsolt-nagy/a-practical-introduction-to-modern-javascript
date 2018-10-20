## Datatypes in JavaScript


Most programming languages help you create values that symbolize a number, a character in a text, or a longer text. You can also symbolize the concept of true and false values using booleans. You can also create values that symbolize the absence of a value. These values are all called *primitive datatypes*.

The name primitive does not come from a negative place. These datatypes are neither stupid, nor inferior to any other datatypes we use in JavaScript. The name primitive comes from their simplicity. The other datatypes you will learn later are *composite*, and they consist of many primitive datatypes.

In JavaScript, there are six primitive types:

- boolean (`true` or `false`)
- number (including integers like `1`, `-2`, and floating point numbers like `1.1`, `2e-3`)
- string ( `''` or `""`, `'ES6 in Practice'` or `"ES6 in Practice"` )
- null type (denoted by `null`)
- undefined (denoted by `undefined`)
- Symbol (don't worry about them yet)

At the bottom of the console in [CodePen](https://codepen.io/pen/?editors=0012), there is a line with a `>` sign. This is where you can enter *JavaScript expressions*. Let's try some. Enter the expression you see after the `> ` sign. Then press enter. You can see the result appear on the next line.

```
> 5
5

> 5 + 2
7

> 7 % 5
2

> 5 ** 2
25
```

Handling integers is straightforward. You have the four arithmetic operations ( `+`, `-`, `*`, `/`) available for addition, subtraction, multiplication, and division respectively. 

The `%` operator is called modulus. `a % b` returns the remainder of the division `a / b`. In our example, `7 / 5` is `1`, and the remainder is `2`. The value `2` is returned.

The `**` operator is called the exponential operator. `5 ** 2` is five raised to the second power.

```
> 0.1 + 0.2
0.30000000000000004

> 3.1e-3
0.0031
```

Some more info on floating points. Due to the way how numbers are represented, `0.1 + 0.2` is not exactly `0.3`. This is normal and occurs in most programming languages.

`3.1e-3` is the normal form of `0.0031`. Read it like the exact value of `3.1` times ten to the power of minus three. Although the form is similar to `3.1 * (10 ** -3)`, there are subtle differences. `3.1e-3` describes the exact value of `0.0031`. `3.1 * (10 ** -3)` describes a composite expression that needs to be calculated:

```
> 3.1 * (10 ** -3)
0.0031000000000000003
```

Floating point arithmetics does not even make it exact.

The division `0 / 0` or using mismatching types creates a special number called *not a number* or `NaN`.

```
> 0 / 0
NaN

> 'ES6 in Practice' * 2
NaN
```

The latter is interesting to Python users, because in Python, the result would have been `'ES6 in PracticeES6 in Practice'`. JavaScript does not work like that.

There is another interesting type: infinity.

```
> 1 / 0
Infinity

> Infinity * Infinity
Infinity

> -1 / 0
-Infinity

> 1e308
1e+308

> 1e309
Infinity
```

JavaScript registers very large numbers as infinity. For instance, ten to the power of 309 is represented as infinity. Division by zero also yields infinity. 

Let's see some strings.

```
> 'ES6 in ' + 'Practice'
"ES6 in Practice"
```

The plus operator concatenates strings. Concatenation means that you write the contents of two strings after each other.

Strings are *immutable* which means that their value cannot be changed. When concatenating two strings, the result is saved in a third string. 

If any of the operands of plus is an integer, the result becomes a string. JavaScript automatically converts the operands of an operator to the same type. This is called *automatic type casting*:

```
> 1 + '2'
"12"

> '1' + 2
"12"
```

Rules may become confusing, so don't abuse automatic type casting. Just know that you may have to explicitly cast a string to an integer to be able to add it to another integer:

```
> 1 + +"2" // +"2" gives a sign to "2", converting it to a number
3

> 1 + Number("2")
3

> 1 + Number.parseInt( "2", 10 )
3

> 1 + Number.parseInt( "2" )
3
```

All conversions work. The first relies on giving a sign to a numeric string which converts it to a number. Then `1+2` becomes `3`. The second type cast is more explicit: you use `Number` to wrap a string and convert it to a number. 

I recommend using the third option: `Number.parseInt` with a radix. `parseInt` converts a string into a number. The second argument of `parseInt` is optional: it describes the base in which we represent the number.

```
> Number.parseInt("ES6 in Practice")
NaN

> Number.parseInt( "10", 2 )
2

> Number.parseInt( "a" )
NaN

> Number.parseInt( "a", 16 )
10
```

Arbitrary strings are often `NaN`. "2" in base 2 is 10. You can see how easy it is to convert a binary or a hexadecimal (base 16) string into a decimal number. Base 16 digits are `0123456789abcdef`. The last 6 digits may also be upper case.

`Number.parseInt` recognizes the starting characters of a string as integer numbers, and throws away the rest:

```
Number.parseInt( "1234.567 89" )
1234
```

The dot is not a character present in integer numbers, so everything after `1234` is thrown away by `Number.parseInt`.

You can also use `Number.parseFloat` to parse floating point. It parses the floating point number until the terminating space:

```
Number.parseFloat( "1234.567 89" )
1234.567
```

Let's see some booleans values. Booleans are either true or false.

```
> 5 <= 5
true

> 5 < 5
false

> !(5 < 5)   // ! stands for negation. !true = false, !false = true.
true

> !!""
false

> !!"a"
true

> !!0
false

> !!1
true

> !!NaN
false

> !!Infinity
true

> !!null
false

> !!undefined
false
```

We can compare two numbers with `>`, `>=`, `==`, `===`, `<=`, `<`. We will discuss the difference between `==` and `===` soon. For the rest of the operators, the result of the comparison is a boolean.

The `!` operator negates its operand. True becomes false, and false becomes true. 

> A **truthy** value is a value `v` for which `!!v` is `true`. Example truthy values are: nonzero integers, strings containing at least one character. 
> A **falsy** value is a value `w` for which `!!w` is `false`. Example falsy values are: empty string, `0`, `null`, `undefined`.

We can convert a value to a boolean by negating it twice: `!!`:

- assuming `v` is truthy, `!v` becomes `false`. `!!v` becomes `!false`, which becomes `true`.
- assuming `w` is falsy, `!w` becomes `true`, and `!!w` becomes false.

For values `a` and `b`, `a == b` is true if and only if both `a` and `b` can be converted to the same value via type casting rules. This includes:

- `null == undefined` is true
- If an operand is a string and the other operand is a number, the string is converted to a number
- If an operand is a number and the other operand is a boolean, the boolean is converted to a number as follows: `true` becomes `1`, and `false` becomes `0`.

Don't worry about the exact definition, you will get used to it. 

For values `a` and `b`, `a === b` is true if and only if `a == b` *and* both `a` and `b` have the same types.

```
> 5 == '5'   // '5' is converted to 5
true

> 5 === '5'  // types have to be the same
false

> 0 == ''    // '' is converted to 0
true

> 0 === ''   // types have to be the same
false

> NaN == NaN // I know... just accept this as something odd and funny
false
```

The negation of `==` is `!=`. Read it as *is not equal to*. 

The negation of `===` is `!==`.

```
> 5 != '5'
false

> 5 !== '5'
true
```

Let me introduce the ternary operator to drive home a strong point about truthiness.

The value of `a ? b : c` is:

- `b` if `a` is truthy
- `c` if `a` is falsy

It is important to note the difference between `2 == true` and `!!2`.

```
> 2 == true    // true is converted to 1
false 

> !!2          // 2 is a truthy value
true

> 2 == true ? 'the condition is true' : 'the condition is false'
"the condition is false"

> !!2 ? 'the condition is true' : 'the condition is false'
"the condition is true"
```

I have seen the nastiest bug in my life in a code, where a condition was in a format `num == true`. As I never felt like learning boring definitions, my lack of knowledge shot me in the foot, because I assumed the opposite conversion in `2 == true`. I can save you some headache by highlighting this common misconception. In `2 == true`, `true` is converted to `1`, and not the other way around.

Null, undefined, and Symbols are primitive types. 

Null represents an *intentional* absence of a primitive or composite value of a *defined* variable.

Undefined represents that a value is *not defined*.

A `Symbol()` is a unique value without an associated literal value. They are useful as unique keys, because `Symbol() == Symbol()` is false. At this stage, just accept that symbols exist. You don't have to use them for anything yet. 

```
> null
null

> undefined
undefined

> void 0
undefined

> Symbol('ES6 in Practice')
[object Symbol] {}
```
