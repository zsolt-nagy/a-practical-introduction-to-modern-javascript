## Your First JavaScript Line

In software development, we often brag about executing a `"Hello World!"` program. In some languages like Java, it takes a lot to write Hello World to the standard output.  In JavaScript, we get away with one single line:

```
console.log( "Hello World!" );
```

You may ask, where can I execute this line? 

If you are lazy, you can simply execute it below. Try it out:

<div class="klipse">
/*---Type here:--->*/
</div>

If you typed the message `console.log( "Hello World!" )`, you can see the following evaluation:

```
"Hello World!"
undefined
```

The first value is a *console log*, which is a value written to the console by the `console.log` function.

The second value is `undefined`, symbolizing that the `console.log` function does not have a defined returned value. You don't have to understand what this means yet until the section on Functions. Until then, just accept that the `undefined` value will appear after your console log.

Notice your statement can span multiple lines. Press enter inside the expression to separate content into two lines. Reformat your code in the above code editor as follows:

```
console
   .log(
        "Hello world!"
)
```

As you can see, you can format JavaScript code in any way you want. The interpreter will not care about the redundant whitespace characters.

Experiment a bit more with the log. Instead of "Hello World!", write 5 + 2. You should see the following:

```
> console.log( 5 + 2 )
7
undefined
```

`>` symbolizes the input of the console. 

As it is inconvenient to load my blog each time you want to write JavaScript, I will recommend a service you can use to execute JavaScript code: [CodePen](https://codepen.io/pen/?editors=0012). In the above link, I prepared everything you need: a JavaScript editor and a console.

In the editor, type

```
console.log( "Hello World!" );
```

Watch it appear in the console.

Congratulations! You managed to write `Hello World!` to the console twice. Let's see what we learned:

- console.log writes a log message to the console
- `"Hello World!"` is a string. One way to formulate a string is using double quotes. Mind you, `'Hello World!'` is also a valid string notation in JavaScript
- there is a semicolon at the end of the statement. The semicolon itself is optional, but I recommend using it

While reading this tutorial, I encourage you to keep [CodePen](https://codepen.io/pen/?editors=0012) open, and play around with the examples.

Later we will learn how to 

- execute JavaScript in our browser developer tools,
- embed JavaScript in HTML pages,
- execute JavaScript using node.js.
