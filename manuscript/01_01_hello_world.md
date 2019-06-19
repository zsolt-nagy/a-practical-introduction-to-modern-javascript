# JavaScript Fundamentals

Practical application is always more important than theory. Therefore, in this course, don't expect long theory or an opinionated rant about how JavaScript code should be written. The objective of this course is that you understand how JavaScript works from a practical point of view so that you can get started with writing code.

## Your First JavaScript Line

When learning programming, we often start with writing and executing a `"Hello World!"` program that writes the `Hello World!` message to the output of our choice. In some languages like Java, it takes a lot to write Hello World to the standard output.  In JavaScript, we get away with one single line:

```
console.log( "Hello World!" );
```

The semicolon marks the end of the statement. Semicolons are optional in JavaScript, because they are inserted automatically by the JavaScript interpreter. However, it is good practice to stick to inserting semicolons, because there are some edge cases, when the JavaScript interpreter inserts semicolons to the wrong place.

You may ask, where can I execute this line? Let me give you a few options.

A> A sandbox is a development environment isolated from its surroundings, where you can experiment with your code without having to deal with tedious setup, dependency import, or other tasks. It's like a sandbox, where kids can get dirty play without consequences in the outside world.  

1. Open [CodePen](https://codepen.io/pen/?editors=0012). CodePen is an online web development sandbox containing boxes for HTML, CSS, and JavaScript code. You need to write your code in the JavaScript box. You can see the result in the console. Whenever you make a change to the JavaScript code, a new line appears in the console.
2. You can also write your code at the bottom of the CodePen console. You can see the same result after pressing enter.
3. Alternatively, you can open a new tab in your browser. Most browsers are the same in this aspect. This item uses the terminology of Google Chrome in English. After opening a Chrome tab, right click inside the tab and select Inspect from the context menu. Alternatively, you can press `Ctrl + Shift + I` in Windows or Linux, and `Cmd + Shift + I` in Mac. Once the Chrome developer tools pops up, you can see a menu bar at the top of the developer tools. This menu bar starts with Elements, Console, Network, and so on. Select Console. You can now see a similar console as the CodePen console. The `>` sign is the prompt. You can enter your JavaScript code after the `>`.

You will find exercises in the book from time to time. Try solving them on your own. If you get stuck, revise the book until you are comfortable with the material. Some exercises have solutions below the exercise, while you are on your own in case of others.

**Exercise 1.** Try out the above three methods to run the `Hello World!` program. Experiment in the Chrome developer tools console what happens if you use `console.info`, `console.warn`, or `console.error` instead of `console.log`.

**Solution:** In the Chrome deverloper tools console, check out the color of the message and the icon in front of the message in case of using `console.log`, `console.info`, `console.warn`, and `console.error`. These colors and icons represent logging levels that are more or less uniform in every programming language. Logging is a way to record what happened in your system. Logging is important for discovering errors in your system in hindsight, and replay what happened exactly.

If you typed the message `console.log( "Hello World!" );`, you can see the following evaluation:

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
);
```

As you can see, you can format JavaScript code in any way you want. The interpreter will not care about the redundant whitespace characters.

If your code spans multiple lines and you are in a console, pressing `Enter` normally executes the line. If you want to add a newline character without executing the code, press `Shift + Enter`.

---

Experiment a bit more with the log. Instead of "Hello World!", write 5 + 2. You should see the following:

```
> console.log( 5 + 2 );
7
undefined
```

`>` symbolizes the input of the console.

By the way, you don't even need `console.log` to write the outcome of the `5 + 2` sum to the standard output:

```
> 5 + 2
7
```

`5 + 2` is an expression. The JavaScript interpreter takes this expression and *evaluates* it. Once this expression is evaluated, its value appears as the output. Notice this is not a log message. In case of a log message, a message is logged, and then the return value of the `console.log` is written to the console. The return value of `console.log` is always `undefined`. As we evaluated the expression directly, we don't have this `undefined` second line on the console.

An alternative online development sandbox is [JsFiddle](jsfiddle.net). Try it out by entering the following code in the JavaScript box of the editor:

```
document.body.innerText = 'Hello World!';
```

After entering this code, the text `Hello World!` appears in the Output. The task of this sandbox is to assemble an HTML page, and this command told the sandbox what to display in the document body.

Congratulations! You managed to write `Hello World!` to the console twice. Let's see what we learned:

- console.log writes a log message to the console
- `"Hello World!"` is a string. One way to formulate a string is using double quotes. Mind you, `'Hello World!'` is also a valid string notation in JavaScript
- there is a semicolon at the end of the statement. The semicolon itself is optional, but I recommend using it

While reading this tutorial, I encourage you to keep [CodePen](https://codepen.io/pen/?editors=0012) open, and play around with the examples.

Later we will learn how to

- execute JavaScript in our browser developer tools,
- embed JavaScript in HTML pages,
- execute JavaScript using node.js.
