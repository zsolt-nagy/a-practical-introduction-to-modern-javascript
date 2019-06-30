## Variable Scopes and Shadowing

This section will be challenging, therefore, read it multiple times to let the material sink in.

Let's summarize what we learned about scopes:

```
let global = true;  // global variable
{
    let block = true; // block scope
}

(function() {
    var functionScoped = true; // function scope
})();
```

Global variables are visible everywhere.

Block scoped variables are visible within the block they are created in, but they are not visible outside the block.

The last example is an immediately invoked function expression. This is a function that we immediately invoked using the `()` symbols. Variables created using `var` inside this function invocation are visible inside the function, but not outside it.

Let's see what happens if we nest multiple immediately invoked function expressions:

```
var functionScoped = 'Sun';
let x = 1;
(function outer() {
    var functionScoped = 'Moon';
    (function inner() {
        console.log( '----Function----' );
        console.log( 'x: ', x );
        console.log( 'functionScoped: ', functionScoped );
    })();
})();
```

After the execution of the program, the following is written on the console:

```
----Function----
x: 1
functionScoped: Moon
```

It does not matter if the `x` variable is declared using `let`, `var`, or `const`. We could even omit the keyword representing the scope, as either way, `x` is created in the *global scope*, therefore, it will be a *global variable*. Therefore, the value of `x` is visible everywhere in the code, so in the `inner` function, we can console log its value.

Inside the `inner` function, we can access all variables of the `outer` function, regardless of whether they are declared using `var`, `let`, or `const`, or they come from the outside.

Both in the `inner` and `outer` functions, we can access variables that were created *in the same scope where the outer function was created*. In this specific situation, it's the global scope.

The above explanation is not complete though. According to the explanation so far, in both `outer` and `inner`, we would have access to two `functionScoped` variables. One has a value `'Moon'`, while the other has a value `'Sun'`. In reality though, we only have access to one of the variables.

If we move outwards from the `inner` scope, we can only access the *closest* variable with a given name. In case of `functionScoped`, this variable is in the `outer` scope. The `functionScoped` variable in the `outer` scope therefore *shadows* the global `functionScope` variable.

In other words, the `'Moon'` shadows the `'Sun'`, giving you a total eclipse from the perspective of the `inner` and `outer` scopes. This is why we can only see the `'Moon'` in the `console.log` statement in the `inner` scope.

Based on this explanation, you can have an idea of what *lexical scope* is for functions. Lexical scope gives you access to

- all variables within a given function,
- all variables in the function containing the scope we are examining recursively,
- if two variables have the same name in a lexical scope, the variable that is defined closest to the scope we are examining *shadows* all variables with the same name that are outside this scope.

The same explanation holds for block scope:

```
let blockScoped = 'Sun';
let x = 1;
{
    let blockScoped = 'Moon';
    {
        console.log( '----Block----' );
        console.log( 'x: ', x );
        console.log( 'blockScoped: ', blockScoped );        
    }
}
```

### Exercises: variable scopes and shadowing

**Exercise 37:** Without running the program, determine the value written to the console:

```
// Global scope
let x = 1;
{
    // block A
    let x = 2;
    {
        // block B
        let x = 3;
    }
    {
        // block C
        console.log( x );
    }
}
```

**Exercise 38:** Rewrite the code of the previous exercise such that you use `var` instead of `let`, and you use immediately invoked function expressions instead of blocks.
