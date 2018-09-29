## Using Strings in JavaScript

In software development, working with strings is a common problem. We often read, process, and write text files, perform logging on the activities of a system, or analyze user input.

Learning how to perform string operations is essential in any programming language.

Let's first recap what you already know about strings from the [JavaScript fundamentals article](http://www.zsoltnagy.eu/javascript-tutorial-for-absolute-beginners/).

### Creating JavaScript strings

Strings contain a sequence of characters. You can either use single quotes (e.g. `'ES6 in Practice'`) or double quotes (e.g. `"ES6 in Practice"`) to create strings.

```
let firstString  = "Hugo's dog",
    secondString = 'Hugo\'s dog';
```

In the console, strings are displayed with double quotes. 

As you can see in the previous example, it is possible to use a single quote inside a double quote, and it is also possible to use a double code inside a single quote. If you want to use a single quote inside a single quote, you have to escape it with a backslash.

The `\` tells the JavaScript interpreter that the next character should be treated as a literal character, not as a meta character. Therefore, `\'` does not signal the start or the end of a string. Side note: if you want to place a backslash in a string, you have to escape it in the form of `\\`.

### Equality of strings

Two strings are equal whenever their values are equal:

```
firstString == secondString
> true

firstString === secondString
> true

firstString === 'Hugo\'s dog'
> true
```

### Sorting strings

Often times in software development, we have to sort strings. There are a few problems with string sorting:

- upper case and lower case letters are sorted differently: `'a' > 'B'`,
- accented characters are completely out of sequence: `'á' > 'b'`.

The [localCompare](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) string method solves both problems:

```
'á'.localeCompare( 'b' )
> -1
'á'.localeCompare( 'a' )
> 1

'a'.localeCompare( 'A' )
> -1
'b'.localeCompare( 'A' )
> 1
'A'.localeCompare( 'b' )
> -1
'B'.localeCompare( 'b' )
> 1
```

Sorting an array of strings in place works as follows:

```
const words = [ 'Practice', 'ES6', 'in', 'á' ];
const sorter = function( a, b ) {
    return a.localeCompare( b );
}

words.sort( sorter );

words 
> ["á", "ES6", "in", "Practice"]
```

The `sort` JavaScript array method sorts its contents in place. This means the order of the elements change inside the array.

## The length of a string

Strings have a `length` property that is equal to the number of characters in the string. The shortest possible string is the *empty string* having a length of `0`:

```
firstString.length
10

''.length
0
```

### Multiline strings

When defining the string, the start and end of the string has to be in the same line. Therefore, we need to insert a *newline character* into the string to make it multiline:

```
'First line.\nSecond line.\nThird line.'
```

Alternatively, you can place a backslash at the end of the line:

```
'First line.\
Second line.\
Third line.'
```

Both solutions are inconvenient. Fortunately, in ES6, template literals were introduced.

### Template literals

Template literals and template tag functions are considered an advanced topic, which is out of scope for us at this stage. Remember, the objective of this article is to highlight practical use cases of strings.

A template literal is defined using backticks:

```
const htmlTemplate = `
    <div>
        This is a node template.
    </div>
`;
```

Notice that newline characters stay inside the template literal. 

It is also possible to evaluate JavaScript expressions inside a template literal:

```
const nodeText = 'This is a node template';
const parametrizedHtmlTemplate = `
    <div>
        ${ nodeText }
    </div>
`;
```

Once created, template literals are immediately evaluated and converted to strings:

```
parametrizedHtmlTemplate
> "↵    <div>↵        This is a node template↵    </div>↵"
```

The in-depth description of template literals is in my book [ES6 in Practice](https://leanpub.com/es6-in-practice), and you can also read the theory [in this article on template literals](http://www.zsoltnagy.eu/strings-and-template-literals-in-es6/).

### Accessing characters inside a string

The bracket notation, also used with arrays, can provide access to an arbitrary character in a string:

```
let digits = '0123456789';
digits[4]
> "4"
```

Opposed to arrays, setting a character inside the string to a new value doesn't work. Indexing a string is strictly *read-only*:

```
digits[4] = 'X';
digits
> "0123456789"
```

Setting `digits[4]` to `'X'` failed silently. 

In general, strings are said to be *immutable*. This means that we cannot change their content. When adding a character to the end of the string, a new string is created.

To iterate on a string, all JavaScript control structures can be used: `for`, `while`, `do...while`, `for...in`, `for...of`:

```
let sum1 = 0;
for ( let i = 0; i < digits.length; ++i ) {
    sum1 += digits[i];
}

let sum2 = 0;
for ( let i in digits ) {
    sum2 += digits[i];
}

let sum3 = 0;
for ( let digit of digits ) {
    sum3 += digit;
}
```

### Finding the index of a substring inside a string

The `indexOf` and the `lastIndexOf` string methods return the first and last index of a substring inside a string.


```
let sequence = '1,2,3,4,5';

sequence.indexOf( ',' )
> 1

sequence.lastIndexOf( ',' )
> 7

sequence.indexOf( ',3' )
> 3

sequence[3]
> ","
```

When the argument of `indexOf` is a string of length higher than `1`, the return value is the position of the first character.

At this point, we assume that you don't use *long unicode characters*. As soon as you know you will use these characters, check out my article [Strings and Template Literals in ES6](http://www.zsoltnagy.eu/strings-and-template-literals-in-es6/) to know how to deal with them.

When string `s` does not contain a specific substring `s0`, then `s.indexOf( s0 )` returns `-1`:

```
sequence.indexOf( 'abc' )
> -1
``` 

Assuming you want to enumerate the indices of all matches, you can specify a second argument, indicating the first index of the string from where we start searching:

```
sequence.indexOf( ',' )
> 1

sequence.indexOf( ',', 1 + 1 )
> 3

sequence.indexOf( ',', 3 + 1 )
> 5

sequence.indexOf( ',', 5 + 1 )
> 5

sequence.indexOf( ',', 7 + 1 )
> -1
```

The question "Does string `s` include the substring `s0`?" is commonly asked during programming problems. We could use `indexOf` to implement the answer:

```
s.indexOf( s0 ) >= 0
```

As this line of code is not too intuitive to read, in ES6, we can use the `includes` method for the same purpose:

```
s.includes( s0 )
```

For more details on the ES6 construct, check out my book ES6 in Practice or [this article](http://www.zsoltnagy.eu/strings-and-template-literals-in-es6/).

### Splitting, slicing, joining, and concatenating strings

Strings have properties. One example is the `length` property. There are also some operations defined on strings. These operations are called methods.

We learned in the previous section that `digits[4] = 'X'` does not set a character inside the `digits` string.

By the end of this section, we will know everything needed to change a character inside strings.


### Splitting a string into an array of substrings

The `split` method splits a string into an array of substrings. Split expects one argument describing how the split should be made.

For instance, in the programming world, we often process CSV files. CSV stands for Comma Separated Values. Let's create an array from a CSV line:

```
const line = '19,65,9,17,4,1,2,6';

line.split( ',' );
> ["19", "65", "9", "17", "4", "1", "2", "6"]
```

If we want to create an array containing each character in the string, we can pass an empty string to the split method:

```
lines.split( '' );
> ["1", "9", ",", "6", "5", ",", "9", ",", "1", "7", ",", "4", ",", "1", ",", "2", ",", "6"]
```

As the contents of arrays can be changed, we can easily change the digit `4` inside the `digits` sequence:

```
let digitsArray = '0123456789'.split( '' );
digitsArray[4] = 'X';
digitsArray
["0", "1", "2", "3", "X", "5", "6", "7", "8", "9"]
```

Split also works with a regular expression argument. In this case, the regex describes the pattern used for splitting strings. For instance, `/\D/` matches every character that is not a digit. Splitting based on this regular expression works as follows:

```
'0,1,2,3,4,5,6,7,8,9'.split( /\D/ );
(10) ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
```

If you want to learn more about regular expressions, check out my [JavaScript Regex Udemy video course](https://www.udemy.com/the-javascript-regular-expression-launchpad/?couponCode=JSREGEX). Use the coupon `JSREGEX` to get it at minimum price.

### Joining strings

We can join strings in two ways:

- using the `+` operator,
- using the `join` string method.

You already saw how the `+` operator works on strings in the [introductory article](http://www.zsoltnagy.eu/javascript-tutorial-for-absolute-beginners/):

```
'first part' + ' second part'
"first part second part"
```

The 'join' method is a bit more interesting. It takes an array of strings and joins them into one string. When `join` is used without any arguments, it joins the strings by inserting commas in-between them. This is because the most common string writing functionality is logging and creating CSV files.

```
["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"].join()
> "0,1,2,3,4,5,6,7,8,9"
```

If you want to join strings without anything in-between them, specify an empty string as the argument of `join`:

```
["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"].join( '' )
"0123456789"
```

You can also specify any other characters:

```
["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"].join( '👍👍' )
"0👍👍1👍👍2👍👍3👍👍4👍👍5👍👍6👍👍7👍👍8👍👍9"
```

### Slicing a string

The `slice` method is commonly used in simple functions and coding challenges. It returns a substring of the string specified by its argument list.

The easiest way to remember the parameter list of `slice` is:

```
str.slice( firstIndexInString )

// or 

str.slice( firstIndexInString, firstIndexAfterString )
```

The first argument of `slice` specifies the position of the first character of the substring. The second argument is optional. When it is missing, slicing happens until the end of the string. When it is specified, it points at the first character after the sliced substring.


```
let hexadecimalDigits = '0123456789ABCDEF';

hexadecimalDigits.slice( 1, 6 )
> "12345"

hexadecimalDigits.slice( 10 )
> "ABCDEF"

hexadecimalDigits.slice( 0, 10 )
> "0123456789"
```

Similarly to Python arrays, the arguments of `slice` can be negative. Negative values count from the end of the array:

```
hexadecimalDigits.slice( -6 )
> "ABCDEF"

hexadecimalDigits.slice( -6, -3 )
> "ABC"

hexadecimalDigits.slice( -6, 13 )
> "ABC"
```

You could learn the `substr` and `substring` methods that perform slicing using a different syntax. However, you will end up using `slice` most of the time anyway, therefore, in this summary, we will omit these two methods. Substr works like slice, but it allows the first argument to be greater than the second one, and still return the substring between the indices. The `substring` method specifies the index of the first character and the length of the substring.

The reason why I advise only using `slice` is that you will use the same method with arrays too. Its parametrization is intuitive, and you can also understand  Python array slicing better.

### Upper and lower case letters

The `toUpperCase` and `toLowerCase` string methods return an upper case and a lower case version of their string respectively:

```
'aBCd'.toLowerCase()
> "abcd"

'aBCd'.toUpperCase()
> "ABCD"
```
