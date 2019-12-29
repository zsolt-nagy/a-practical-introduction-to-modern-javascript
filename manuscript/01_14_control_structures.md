## An Introduction to Control Structures

It is time to learn what a JavaScript program looks like. In this section, we will learn the three main elements of describing the control flow of a program. These are: *sequence*, *selection*, and *iteration*.

A> When writing programs, we use three control structures: *sequencing* instructions, *selection* between different branches containing instructions, and *iteration* on instructions executing them multiple times.

First of all, every program has an entry point and an exit:

![`Flowchart start and end states`](images/Flowchart.png)

This diagram is called a *flowchart* describing the control flow of a program.

Let's explore what happens between these two endpoints.

So far we have learned the fundamentals of coding so that we can create the individual building blocks of a program. These building blocks include:

- declaring and defining variables,
- computing values,
- creating data of simple or complex types,
- invoking functions,
- formulating conditions,
- requesting input from the user.

We can already write these instructions after each other in *sequence*.

### Sequence

Executing instructions one after the other is called *sequencing*. A sequence of instructions is executed one after the other. Example:

```
Ask for prompt user input;
Convert the user input to a number;
Get the last digit of the converted input;
Write the result to the console.
```

The flowchart of this sequence of instructions is as follows:

![`Sequence of instructions`](images/sequence1_en.png)

In a flowchart describing a sequence of instructions, we distinguish between four types of nodes:

- *Start* node: entry point
- *End* node: exit point
- *Trapezium*: input or output operation such as requesting user input or writing a value to the console
- *Rectangle*: operations performed on data

A flowchart is read from top to bottom, moving from the start node towards the end node. The description of a flowchart can be vague or mathematically accurate. For instance, we could use variable names to make the contents of the flowchart more relatable to writing code:

![`Sequence of instructions using variables`](images/sequence2_en.png)

Using JavaScript functions is not necessary. It is enough if we can describe what a node in our flowchart should do. The objective of a flowchart is not to document how your program works. The aim of using flowcharts is for you to learn the fundamentals of programming.

During sequential execution, we execute instructions in sequence. Given that you have learned many JavaScript instructions, you can write many different programs.

Sequencing is not enough though to write sophisticated programs. For instance, you already know how to write conditions in JavaScript. However, I haven't told you yet how these conditions can be used in your code. You will soon learn that conditions are used to perform both selection between branches of code, and iteration on a code segment.

Another example is the creation of arrays. We already know how to create an array of arbitrary length. However, we cannot yet traverse this array based on the content you have read so far. This is where iteration will help you.

Let's explore these two control structures one by one.

### Selection

When performing **selection**, we branch off based on a condition. If the condition is true, we visit one branch. If the condition is false, we visit another branch. We select our branch based on whether our condition. Let's see an example:

```
Ask for prompt user input;
If this value is empty:
    Write "invalid value"
Else:
    Write "valid value"
```

When writing a selection operation, the program branches off. Based on the values in the condition, we choose one branch out of the two:

![`Flowchart of selection`](images/Selection1_en.png)

We denote selections by a diamond with one input and two outputs. Based on the condition written inside the diamond, we choose one output or the other.

You might recall an operator before that implements selection: the ternary operator. The above program can be written using the ternary operator in the following way:

```
let input = prompt();
console.log( input.length == 0 ? "invalid value" : "valid value" );
```

The ternary operator is great when we have to choose between values. Its use is limited though, when we have to execute complex operations, especially if they have side-effects. This is why we will learn the `if` - `else` statement and `switch` to perform selection.

Although we will learn about `if` and `switch` statements later, as an introduction, let's explore how selection is written in JavaScript:

```
let input = prompt();
if ( input.length == 0 ) {
    console.log( 'invalid value' );
} else {
    console.log( 'valid value' );
}
```

This structure is self-explanatory. If the condition inside the `if` is true, we execute the block right after it. Otherwise, we execute the second block. You can write a sequence of instructions inside each block, and even create block scoped variables there.

### Iteration

When performing iteration, we repeat an instruction or a set of instructions as long as a condition stays true.

Iteration is useful for multiple reasons. The most evident benefit of using iteration is that you don't have to manually copy-paste code that you repeat multiple times. For instance, when logging the elements of an array of length `10000`, you might want to avoid writing ten thousand console log statements in your code:

```
console.log( arr[0] );
console.log( arr[1] );
console.log( arr[2] );
...
console.log( arr[9999] );
```

Writing ten thousand console log statements is only possible, because you know how long your array is. In programming, the length of an array can often change. For instance, if you have a website, where the user presses a button, you can build an array of todo items by taking some input field values and saving them in the array as todo items. When printing the contents of your todo list, you cannot rely on knowing in advance how many items there would be in your todo array at the time of running your code. Therefore, writing this code is not possible:

```
console.log( arr[0] );
console.log( arr[1] );
console.log( arr[2] );
...
console.log( arr[arr.length - 1] );
```

What you need, is a control structure performing *iteration*. This control structure would iterate from `0` to `arr.length - 1`, take each value, and log each element of the array one by one:

```
for each *i* between 0 and arr.length - 1:
    LOG( arr[*i*] );
```

The flowchart of this iteration looks as follows:

![`Flowchart of iteration`](images/Iteration1_en.png)

Iteration has the same symbol as selection, with the exception that its input comes from two sources. One source is when we enter the iteration for the first time. Another source is coming from the below, where we finished executing the statements inside the iteration.

We will learn many language constructs to perform iteration. These include:

- loops such as `while`, `do-while`, `for`, `for..in`, `for..of`
- recursion, which is a name for a function calling itself directly or indirectly. Direct recursion means that we execute function `f`, and one of our statements inside the function is calling `f`. Indirect recursion occurs during the execution of function `f`, if we call another function `g`, which may call `f`. Example for direct recursion:

```
function printArray( arr ) {
    if ( arr.length > 0 ) {
        console.log( arr[0] );
        printArray( arr.slice( 1 ) );
    }
}
```

Once you run `printArray( [1, 3, 5, 1] )`, you can see that the result is `1`, `3`, `5`, `1` printed on screen, one value in each line.

If you remember how an `if` statement works from above, you have learned everything else to understand the `printArray` function. We first print the element with index `0`, then we create a slice from the array. This slice keeps all elements from the array except the one printed to the console. We repeat this process until we run out of elements in the array.

Unfortunately, this solution is not only inconvenient, but it is also resource intensive. Somewhere between ten and a hundred thousand elements, the program throws a *stack overflow* error, because it can't handle that many recursive function calls at once. Therefore, we will learn loops to simplify iteration from the above function to a simple and understandable form such as the following:

```
for ( let value of arr ) {
    console.log( value );
}
```

Without jumping ahead too much, you can interpret this code such that you take each value of `arr`, and print it.

I hope this simplification is exciting enough for you to continue with the next sections on selection and iteration.
