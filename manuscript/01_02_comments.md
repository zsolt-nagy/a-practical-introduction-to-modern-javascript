## Comments

We often place comments in our code so that we know what it is doing.

JavaScript is similar to C++ and Java in its commenting style:

- Everything between `/*` and `*/` is ignored by the interpreter
- Everything after `//` on the same line is ignored by the interpreter.

```
let a = 5 + 2; // This is a single line comment lasting until the end of the line.

/*
     A comment that can span multiple lines.
     Everything inside the comment will be ignored by the JavaScript interpreter.
     let b = 2;
*/
```

The above two comments are interpreted as:

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
