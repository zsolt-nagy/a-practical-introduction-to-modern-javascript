## Data types in JavaScript


Most programming languages help you create values that symbolize a number, a character in a text, or a longer text. You can also symbolize the concept of true and false values using booleans. You can also create values that symbolize the absence of a value. These values are all called *primitive data types*.

The name primitive does not come from a negative place. These data types are neither stupid, nor inferior to any other data types we use in JavaScript. The name primitive comes from their simplicity. The other data types you will learn later are *composite*, and they consist of many primitive data types.

Why are data types important for us?

For instance, whenever you check your emails, go on Facebook, or check your bank account, you always see data: your name, your messages, the current date and time, and in the settings, you can also see other features of your account.

Data have types. We tend to use an integer (whole number, without a fractional part) than text. A checkbox can have two possible values: true or false. These data types are also unique. For each data type, different operations apply, and their possible values are also different.

In JavaScript, there are six primitive types:

- boolean (`true` or `false`)
- number (including integers like `1`, `-2`, and floating point numbers like `1.1`, `2e-3`)
- string ( `''` or `""`, `'ES6 in Practice'` or `"ES6 in Practice"` )
- null type (denoted by `null`)
- undefined (denoted by `undefined`)
- Symbol (don't worry about them yet)

A> Floating point numbers typically contain a **decimal separator** character, most often a dot. The **precision** of floating point numbers is limited, because there are a limited number of bits available.

We will soon learn more about anomalies arising from restrictions on floating point precision.

A> **Operations** can be performed on data of given types. Operations are denoted by an **operator** symbolizing the operation. Examples: `+`, `-`, `*`, `/`. Operators perform operations on data that are called the *operands* of the operation.

For instance, in the `2 * 3` operation, `*` is the operator symbolizing multiplication. Multiplication has two operands: `2` and `3`.

Some important operators are:

- `+` stands for **addition**. Example: `2 + 3` is `5`.
- `-` stands for **subtraction**. Example: `2 - 3` is `-1`.
- If there is no operand on the left of `+` or `-`, then `+` or `-` becomes a **sign**. Examples: `+3` or `-2`.
- `*` stands for **multiplication**. Example: `3 * 2` is `6`.
- `/` stands for **division**. Example: `3 / 2` is `1.5`.
- `%` stands for the **modulus** operation, which is the remainder of a number divided by another number using the rules of integer division. Example: `5 % 2` is `1`, because `5` divided by `2` is `2`, and the remainder is `1`. In other words, the *mod 2 remainder of 5 is 1*.
- `**` is the **power operator**. Example: `2 ** 3` (two to the power of three) is `2 * 2 * 2`, which is `8`.

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

Operations can be grouped together using parentheses. Parentheses override the priority of executing operations. For instance, in mathematics, multiplication has higher priority than addition. This means, `1 + 2 * 3` is the same as `1 + (2 * 3)`.

Let's see an example for using parentheses:

```
>  5 * ( 1 + 2 * ( 3 + 4 ) )
// 5 * ( 1 + 2 * 7 )
// 5 * ( 1 + 14 )
// 5 * 15
75
```

Opposed to mathematics, we do not use brackets or braces to group operations. Parentheses can be used within parentheses. It is also important to construct valid expressions with parentheses, which means that each closing parenthesis should belong to a preceding opening parenthesis.

Similarly to mathematics, different operators have different priority (also referred to as precedence). When an operation has to be performed before another operation, we say that this operator:

- has higher priority,
- binds stronger.

Most operators have either one or two operands. This means the operator transforms either one or two values to a new value. Examples:

- The operands of `5 + 2` are `5` and `2`. The `+` operator transforms these operands to `7`.
- The operand of `-(2)` is `(2)`. I put parentheses around the `2` to emphasize that `-` is an operator and not a symbol to describe an integer.

Operators **bind** their operands. We have already seen that some operators bind stronger than others. For instance, multiplication binds stronger than addition:

```
5 * 2 + 3 ----> 10 + 3 ----> 13
```

We have also seen that the priority of operators can be overridden using parentheses:

```
5 * (2 + 3) ----> 5 * 5 ----> 25
```

The basic arithmetic operations (`+`, `-`, `*`, `/`, `**`) and the two signs (`+`, `-`) have the following priority:

1. Signs: `+` or `-` can stand in front of a number. This sign is evaluated first.
2. Power: `**` binds the strongest out of the operators with two operands.
3. Multiplication and division: `*` and `/`
4. Finally, addition and subtraction: `+` and `-`

A> If you use more complex operations in JavaScript and you are not sure about their priority, use parentheses. Relying too much on the evaluation priority of operations reduces the readability of your code, which means others may have a hard time cooperating with you if you tend to give them riddles.

The modulus operation was not placed in the above priority order, because most of the time, you won't need it in a complex expression. In the unlikely case you used it together with other operators, use parentheses. The `%` operator binds just as strongly as multiplication and division does. However, when using `%` in a complex expression, parentheses increase the readability of your code.

---

**Exercise 5:** Determine the type of the following expressions.

a. `7 % 2`
b. `""`
c. `"false"`
d. true
e. `2.5`

**Exercise 6:** Calculate the value of the following expressions:

a. `5 - -1`
b. `2 - 2 * 2`
c. `2 + 2 * 3 ** 2`

**Exercise 7:** Suppose you invest a hundred thousand dollars. Use JavaScript to determine how much money you will have after 1, 2, 5, and 20 years, provided that the annual interest rate is 2%. Help: an annual interest rate of 2% means that you will get 102% of your current money in one year. The ratio between 102% and the current amount (100%) is `1.02`.

**Exercise 8:** Determine which expressions are valid.

a. `2 ** 2 ** 2 ** 2`
b. `( 1 ) + (2 * ( 3 ) )`
c. `( 1 + 2 ) * ( 3 * 4 ) ) * ( ( ( 5 - 2 ) * 3 )`
d. `- ( 2 + 2)`



## The number type

Handling numbers is mostly straightforward. You have the four arithmetic operations ( `+`, `-`, `*`, `/`) available for addition, subtraction, multiplication, and division respectively.

The `%` operator is called modulus. `a % b` returns the remainder of the division `a / b`. In our example, `7 / 5` is `1`, and the remainder is `2`. The value `2` is returned.

The `**` operator is called the exponential operator. `5 ** 2` is five raised to the second power.

---

**Exercise 9.** Match the following expressions with the possible values below.

Expressions:

A. `5 ** 2 + 1`
B. `11 * 11 - (-4)`
C. `1e2 - 11 * 8 - 2 * 2 / 4`

Values: `26`, `711`, `11`, `165`, `125`.

---

Let's see some more surprising floating point operations.

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

Floating point arithmetics does not even make this expression exact.

If you need precise values, you have two options: one is rounding or truncating the result, and the other is to convert the floating point operands to integer numbers. For instance, instead of `0.25` dollars, you can write `25` cents. This works when you always expect the same number of precision after the decimal point.

Let's see an example for rounding:

```
> 0.1 + 0.2
0.30000000000000004

> Number( 0.1 + 0.2 ).toFixed( 1 );
0.3
```

In the above example, the precision of the result is fixed to one decimal point.

The division `0 / 0` or using mismatching types creates a special number called *not a number* or `NaN`. Ironically, we will soon see that the type of the `NaN` value is `number`.

```
> 0 / 0
NaN

> 'ES6 in Practice' * 2
NaN
```

The latter is interesting to Python users, because in Python, the result would have been `'ES6 in PracticeES6 in Practice'`. JavaScript does not work like that.

There is another interesting numeric value: `Infinity`.

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

**Exercise 10.** Determine the type and value of the following numbers:

a. `(1 - 1) / 0`
b. `(1 - 1) / 1 * 0`
c. `5e0`
d. `5 ** 0 / 0`
e. `5 ** (0 / 0)`


## Strings and escape sequences

Moving on to string data:

```
> 'ES6 in ' + 'Practice'
"ES6 in Practice"
```


The plus operator concatenates strings. Concatenation means that you write the contents of two strings after each other. Concatenation means that you join the values on the left and on the right of the concatenation operator (`+`).

A frequent question is, how to write quotes inside a string if quotes represent the boundaries of a string. In JavaScript, there are multiple solutions:

```
// Solution 1:
console.log( '--- "This is a quote" ---' );

// Solution 2:
console.log( "--- 'This is a quote' ---" );

// Solution 3:
console.log( "--- \"This is a quote\" ---" );
```

You can use any number of double quotes inside single quotes, and any number of single quotes inside double quotes. However, using a single quote inside a string defined using single quote would mean that we terminate the string. The same holds for using a double quote inside a string defined using double quotes.

As both single quotes and double quotes are used frequently, the need arises to use both the single quote and the double quote characters inside a string at any time. We can do this by *escaping* the quote using the `\` (backslash) character.

A> The backslash (`\`) character means that a special character (or characters) is coming. The backslash and the special character(s) together are called an *escape sequence*. Escape sequences symbolize special characters.

Examples for escape sequences:

- `\'` and `\"`: single or double quote characters. In JavaScript, escaped quotes do not start or terminate a string.
- `\n`: newline character. We can put a line break in the string, making the character after `\n` appear on the next line.
- `\\`: as the backslash character creates an escape sequence, it is a special character itself and has to be escaped. The first backslash tells the JavaScript interpreter that a special character is coming. The second backslash says that this character is the backslash. This escape sequence is important to keep in mind when describing Windows file paths in JavaScript or node.js:

```
> console.log( `c:\\js\\hello.js` )
"c:\js\hello.js"
```

Multiline strings can be created using *template literals*. This comes handy when saving HTML markup in a string:

```
> console.log( `
  <p>
    paragraph
  </p>
  <ul>
    <li>first list item</li>
    <li>second list item</li>
  </ul>
` );
```

The above expression prints the text in-between backticks, including the newline characters. The usage of template literals is an advanced topic, we will not deal with them in this chapter.

---

**Exercise 11.** Write the following JavaScript strings in the console of your developer tools:

- "JavaScript is easy", at least until it's not.
- Save everything to the `C:\Documents` folder.
- Write the following countdown using one `console.log` statement:

```
3
2
1
START!
```

---

Strings are *immutable* which means that their value cannot be changed. The word immutable comes from the fact that strings cannot be mutated. If strings were mutable, we would be able to change the `b` character in the `'abc'` string without creating a new string. In reality, in order to make an `'aXc'` string from an `'abc'` string, we need to create a new string from scratch.

Similarly, the result of `"a" + "b"` is a brand new string: `"ab"`. Even after the result is created, `"a"` and `"b"` stay in memory. This is why strings are *immutable* in JavaScript.

If any of the operands of plus is an integer, while the other operand is a string, then the result becomes a string. JavaScript automatically converts the operands of an operator to the same type. This is called *automatic type casting*:

```
> 1 + '2'
"12"

> '1' + 2
"12"
```

Rules may become confusing, so don't abuse automatic type casting. Most software developers do not know these rules by heart, as it generally pays off more to write code that is obvious and understandable for everyone.

A> **Implicit type conversion** happens when the JavaScript interpreter automatically converts a datum of one type to a datum of another type. **Explicit type conversion** occurs when the type conversion is specified in the code.

Examples:

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

I recommend using the third option: `Number.parseInt` with a radix. `parseInt` converts a string into a number. The second argument of `parseInt` is optional: it describes the base in which we represent the number. Most of the time, we use base 10 values.

Let's see some more `Number.parseInt` values:

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

Strings that do not start with a number are often `NaN`. `"10"` in base 2 is `2`. The character `"a"` is not interpreted in base 10, its value is `NaN`. The same `"a"` character in base 16 is `10`.

A> **Hexadecimal numbers** are base 16 numbers. Hexa means 6, and decimal means 10. Ten plus six equals sixteen, hence the hexadecimal name. The digits of hexadecimal numbers are `0123456789abcdef`. The last six digits can also be in upper case yielding `ABCDEF`.

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

---

**Exercise 12.** Select the values out of the following list that have the type `number`.

a. `+"1"`
b. `Number.parseInt("")`
c. `Number("1")`
d. `1 + "1"`
e. `"1" + 1`
f. `1 + +"1"`

**Exercise 13.** Determine the value of the following expressions:

a. `Number.parseInt( "1.25" )`
b. `Number.parseInt( "1 2" )`
c. `Number.parseInt( "5", 2 )`
d. `Number.parseInt( "15", 2 )`
e. `Number.parseInt( "f", 16 )`
f. `Number.parseInt( "ES6" )`
g. `Number.parseInt( "ES6", 16 )`


---

### The boolean type

Let's see some booleans values. Booleans are either `true` or `false`.

The `!` operator symbolizes negation. `!true` becomes `false`, while `!false` becomes `true`.

```
> !true
false

> !false
true
```

An arbitrary value can be converted to boolean using the `Boolean` function:

```
> Boolean(0)
false

> Boolean(1)
true

> Boolean(2)
true

> Boolean(null)
false
```

The `!`operator not only negates a value, but also converts it to a boolean. For instance, the negation of a string can be described as follows:

- the empty string (`""`) is evaluated as `false` by default in a boolean expression. Negating this value yields `true`.
- An arbitrary at least one character long string is evaluated as `true` in a boolean expression. Negating this value yields `false`.

```
> !""
true

> !" "
false
```

In JavaScript, we differentiate between **truthy** and **falsy** values. These values are not necessarily booleans. Their value only becomes `true` or `false` after a *type conversion*.

> A **truthy** value is a value `v` for which `Boolean(v)` is `true`. Example truthy values are: nonzero integers, strings containing at least one character.
> A **falsy** value is a value `w` for which `Boolean(w)` is `false`. Example falsy values are: empty string, `0`, `null`, `undefined`.

Question: Why do we need type conversion using the `Boolean` function?

Answer: Because otherwise automatic type conversion would produce unintended results. For instance, in the expression `2 == true`, both sides of the comparison are converted to numbers. As the value of `Number(true)` is `1`, the `2 == 1` expression is evaluated to `false`:

```
2 == true ---> 2 == Number(true) ---> 2 == 1 ---> false

2 == false ---> 2 == Number(false) ---> 2 == 0 ---> false
```

Furthermore, `null` and `undefined` are neither `true`, nor `false`:

```
> null == true
false

> null == false
false

> undefined == true
false

> undefined == false
false
```

However,

- `Boolean( null )` and `Boolean( undefined )` are both `false`
- `!null` and `!undefined` are both `true`
- `!!null` and `!!undefined` are both `false`

Similarly to the `Boolean` function, double negation also converts an arbitrary value into boolean:

- if `v` is truthy, then `!v` is `false`, and `!!v` is `true`
- if `w` is falsy, then `!w` is `true`, and `!!w` is `false`

Examples:

```
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

A> Once you start writing complex software, use the `Boolean` function instead of double negation to convert values to booleans. This way, your code becomes more readable.

We can compare two numbers with `>`, `>=`, `==`, `===`, `<=`, `<`. We will discuss the difference between `==` and `===` soon. For the rest of the operators, the result of the comparison is a boolean.

```
> 5 <= 5
true

> 5 < 5
false

> !(5 < 5)   // ! stands for negation. !true = false, !false = true.
true
```

The `=` symbol is not used for comparison. It is used for assigning a value to a variable (see later).

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

The negation of `==` is `!=`. Read it as *is not equal to*. For instance, `!(a == b)` becomes `a != b`. It is time mentioning that you are free to use parentheses to group your values and override the default priority of the operators.

The negation of `===` is `!==`.

```
> 5 != '5'
false

> 5 !== '5'
true
```

**Exercise 14:** Choose the values that (1) are `true`, (2) are truthy.

a. `1`
b. `""`
c. `"false"`
d. `!!"false"`
e. `0 == ''`
f. `0 === ''`
g. `0 != !1`
h. `0 !== !1`
i. `1 != !1`
j. `1 !== !1`
k. `null`
l. `undefined`
m. `null == undefined`  
n. `null === undefined`



So far, all operators have been unary or binary meaning that they *bind* one or two values:

- the expression `5 + 2` has the operands `5` and `2`
- the expression `+'2'` has the operand `'2'`

Recall that operators bind their operands. Some operators are said to bind stronger than others. For instance, multiplication binds stronger than addition:

```
5 * 2 + 2 ----> 10 + 2 ----> 12
```

Also recall that is possible to override the precedence of the operators with parentheses:

```
5 * (2 + 2) ----> 5 * 4 ----> 20
```

There is one ternary operator in JavaScript.

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






### null, undefined, symbol types

Null, undefined, and Symbols are primitive types.

Null represents an *intentional* absence of a primitive or composite value of a *defined* variable.

Undefined represents that a value is *not defined*. We will deal with the difference between `null` and `undefined` later.

A `Symbol()` is a unique value without an associated literal value. They are useful as unique keys, because `Symbol() == Symbol()` is false. Imagine a symbol as a unique key that opens one specific lock, in a world, where each created key is different from all other keys previously created. At this stage, just accept that symbols exist. You don't have to use them for anything yet.

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

The value undefined can also be created using the `void` prefix operator.

Symbols can have a string description. This string description does not have an influence on the value of the symbol:

```
> Symbol('a') == Symbol('a')
false
```

### Exercises

**Exercise 15:** Without running the code, determine the values written to the standard output:

```
// A. Arithmetics
console.log( 2*2+4 );

// B. Ternary operator
console.log( 3 % 2 ? 'one' : 'zero' );

// C. Not a Number
console.log( (0/0) == NaN );
```

Once you are done, verify your answers by running the code.

**Exercise 16:** Convert the following hexadecimal (base 16) values into base 10 and base 2: `0`, `F`, `ff`, `FFFFFF`, `99`, `10`.

Hint: you can convert a value from decimal (base 10) into binary (base 2) in the following way:

```
Number( 2 ).toString( 2 );
// --> "10"

Number( 3 ).toString( 2 );
// --> "11"
```

**Exercise 17:** Without evaluating the expression, estimate the difference of the base 10 value `2 ** 24` and the hexadecimal value `FFFFFF`. Create a JavaScript expression that calculates this difference.

**Exercise 18:** Which datatype would you use to model the following data? In case you chose a `number` type, choose whether you would use an integer or a floating point.

A. your name
B. your bank account number (assuming it only contains digits)
C. your age
D. whether you are over 18 or not
E. the price of a book is 9 dollars 95 cents 
