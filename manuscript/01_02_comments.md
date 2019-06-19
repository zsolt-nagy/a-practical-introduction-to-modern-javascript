## Comments

When writing code, it is important that others can read it too. This is why it is beneficial to comment our code. JavaScript comments are similar to the C++ and Java commenting format. When the JavaScript interpreter reads comments, it completely ignores their content:

- Everything between `/*` and `*/` is ignored by the interpreter
- Everything after `//` on the same line is ignored by the interpreter.

Examples:

```
let a = 5 + 2; // This is a single line comment lasting until the end of the line.

/*
     A comment that can span multiple lines.
     Everything inside the comment will be ignored by the JavaScript interpreter.
     let b = 2;
*/
```

The above code is interpreted as:

```
let a = 5 + 2;
```

Everything else is ignored.

Why do we use comments? To avoid ending up in similar situations:

```
//
// Dear maintainer:
//
// Once you are done trying to 'optimize' this routine,
// and have realized what a terrible mistake that was,
// please increment the following counter as a warning
// to the next guy:
//
// total_hours_wasted_here = 42
//
```

My other favorite is:

```
// I dedicate all this code, all my work, to my wife, Darlene, who will
// have to support me and our three children and the dog once it gets
// released into the public.
```

Source: [StackOverflow](https://stackoverflow.com/questions/184618/what-is-the-best-comment-in-source-code-you-have-ever-encountered)

Summary: write readable code with good comments!

### Exercises

**Exercise 2**: Without running the code, determine what is written to the standard output:

```
console.log( 1 + 2 + 3 + 4 );
2 + 4;
console.log( 'End' );
```

**Exercise 3**: Run the code of **Exercise 2** both in CodePen and in your browser.

**Exercise 4**: Add comment symbols to the code of Exercise 2 such that the program only prints the `End` message.
