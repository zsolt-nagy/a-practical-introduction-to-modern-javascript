## Requesting Input from the User

When I started programming back in the days, I mainly studied from books, because back in the 90s, I didn't have access to Internet. I can recall a thick programming book I had. As I worked my way through the examples of the book, I had one question in mind all the way through making progress in the book: how can I get an input from the user?

After a while, I searched for a function that lets me enter an input, and I didn't find this function at all. I asked myself, if it is so hard to get an input, then why am I learning programming?

Eventually, I had to go to an Internet café to find the answer. In hindsight, I found out that user input was not even considered in the thick book I wrote.

As I recalled these memories, I concluded that I don't want to create a book, where I leave you wondering about how to enter input. Therefore, in this section, you will learn about two methods to get input from the user. These are:

1. Prompt window,
2. HTML5 forms.

There are many other ways to get user input, such as an API connection or a direct database connection in case of node.js. A node.js program also helps you process files. However, in this section, we will stick to introducing the capabilities of Prompt windows and HTML5 forms.

### Prompt window

You can use the `prompt` statement to create a window with a textfield and get data from the user:

```
let value = prompt( 'Enter a number' );
```

Once this expression is executed, a popup appears on screen with the `'Enter a number'` message, an input field, and two buttons: OK and Cancel. If you press the Cancel button, the `prompt` function returns `null` in the code. If you press the OK button, the `prompt` function returns the text that the user entered in the input field. If the input field is left empty, the return value after pressing OK becomes the empty string (`""`).

Suppose that the user entered the value `25`. As the `prompt` function returns a string, this value is available as a string:

```
> console.log( value, typeof value);
"25" string
```

### HTML5 Forms

This section only serves as an introduction to how data can be extracted from an HTML page using JavaScript. Our goal here is not deep understanding, but rather illustration of possibilities, so that you know what to expect from JavaScript.

Open a new tab in your Google Chrome browser, and open the developer tools console. Run the following code:

```
document.body.innerHTML = `
  Age: <input type="text" name="age" class="js-age">
  <input type="checkbox" class="js-accept-toc" id="accept-toc">
  <label for="accept-toc">Accept the terms and conditions</label>
`;
```

After running this code, the contents of the website you were viewing got replaced by a textfield and a checkbox. Don't worry, the change is only effective in your browser, no-one else can see these changes from other computers.

You can modify the value of the textfield and checkbox from the browser. Let's learn how we can access these values using JavaScript.

We can extract the contents of the `Age` field in the following way:

```
let age = document.querySelector( '.js-age' ).value
```

The expression on the right hand side of the equation returns the string content of the textfield that has the class `js-age`. This return value is stored in the `age` variable.

The `'.js-age'` string is a selector, where the dot means that we are selecting an HTML element that has a class equal to the value after the dot. As the input field containing the age has an attribute `class="js-age"`, the selector retrieves the correct input field.

The same field could have been selected with many other selectors such as:

- `'[type=text]'`,
- `'[name=age]'`.

A checkbox can either be checked or unchecked. Similarly to the textfield example, we can use a class selector to retrieve the DOM node we are looking for. However, this time, instead of the `value` property, we need to retrieve the `checked` property:

```
let isChecked = document.querySelector( '.js-accept-toc' ).checked
```  

The `isChecked` variable describes a boolean expression that can either be `true` or `false`, depending on whether the checkbox is checked or not. 
