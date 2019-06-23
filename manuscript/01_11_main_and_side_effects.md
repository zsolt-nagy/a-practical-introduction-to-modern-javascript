## Main Effect and Side Effect

When writing programs, we typically rely on two effects: main effect and side effect.

A> The *main effect* of executing an operation or a function is the return value of the executed operation or function.

A> The *side effect* of an operation or function is an observable effect that goes beyond the act of returning the value of the executed operation or function. This observable effect can be e.g. a changed variable value in the *lexical scope*, writing text to the console, or changing the HTML content of a website.

For instance, suppose you cash out a hundred dollars using your credit card. The main effect of the transaction is the cash you get. Although many people don't care about the side effects, in real life, this transaction can have multiple side effects:

- our account balance is decreased by 100 dollars,
- if our balance becomes negative, we owe money to the bank,
- some banks deduct transaction costs from your account,
- while using your account, the bank may store data on your individual preferences and habits.

Let's model some of these side effects with code:

```
let transactionCost = 2;
let balance = 500;

function withdraw( sum ) {
    balance = balance - sum - transactionCost;
    console.log( sum + ' has been withdrawn.' );
    console.log( transactionCost + ' has been paid as transaction cost.' );

    return 'Bank notes worth $' + sum;
}
```

In the first line of the function body, as a *side effect*, we subtract the cashed out sum and the transaction cost from our account balance.

In the second and third lines of the function body, as a *side effect*, we log two messages.

In the last line of the function body, we return the bank notes as the *main effect* of the function. For the sake of simplicity, we return a string here.

We have seen that `console.log` statements rely on their side effect to log messages. Indeed, the main effect of running a `console.log` statement is that it returns the value `undefined`. The side effect is the console message.

One of the main use cases of JavaScript is the dynamic modification of web content. If you open a browser window and the developer tools console, you can modify the HTML content of the displayed website using the `document` global object:

```
document.body.innerHTML = <h1>JavaScript</h1>;
```

The main effect of running the program is the assignment itself. The side effect of running the code is that the content of the website changes. An `<h1>` heading is rendered on screen with the content `JavaScript`. We can even retrieve this content using the `document` object in the following way:

```
// Out of all <h1> tags on your page, return the first one
document.getElementsByTagName( 'h1' )[0]
```

### Exercises: Main and Side Effects

**Exercise 40:** Determine the main effect and side effects of the following function:

```
let numberOfInsertions = 0;

function appendParagraph( text ) {
    document.body.innerHTML =
        document.body.innerHTML + "<p>" + text + "</p>";
    numberOfInsertions = numberOfInsertions + 1;
    console.log( "Inserted paragraph: " + text );
    return true;
}

appendParagraph( "zsoltnagy.eu" );
```
