## Using JavaScript with HTML and CSS

The goal of this section is not to teach you the basics of CSS or JavaScript button click event handling, but to show you how HTML, CSS, and JavaScript is structured.

### Creating the Markup

When visiting a website, we define its HTML markup, some styling information, and some dynamic functionality.

Markup is written in HTML. HTML stands for Hyper-Text Markup Language. We will not introduce HTML in detail, so in case you don't know how to write simple HTML documents, check out [this](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics) article followed by [this](https://www.w3schools.com/html/html_intro.asp) tutorial.

Let's create a simple example with a form. We will place a textfield in a form, and a button that displays a greeting in the form of an alert box.

```
<!doctype html>
<html lang="en">
  <head>
    <title>Greetings</title>
  </head>
  </body>
    <form>
      <input type="text" 
             class="tf-large  js-name" 
             placeholder="name">
      <button class="btn-large  js-hello">Greet</button> 
    </form>
  </body>
</html>
```

As an editor, you can use [Sublime Text](https://www.sublimetext.com/3), [Atom.io](https://atom.io/), or [Visual Studio Code](https://code.visualstudio.com/). Experiment with the text editor of your choice a bit.

Create a `GreetingProject` folder on your computer and save the above file there. Name it `greeting.html`. Create a `js` and a `styles` folder in your folder. You should have the following folder structure:

```
GreetingProject
  [-] js
  [-] styles
  ----greeting.html
```

If you double click the `greeting.html` file, it opens in a browser. You can see a textfield there, where you can enter your name. Unfortunately, when you press the Greet button, the text you enter in the textfield is gone. This is what we will fix with JavaScript.


### Adding JavaScript code

When you create an HTML form, pressing a button submits the form by default. Submitting a form reloads the page. Once you reload the page, the data entered in the textfield is lost. This is what we will prevent now.

Create a `form.js` file inside the `js` folder, and place the following content there:

```
function helloListener( event ) {
    event.preventDefault();
    console.log( 'button pressed' );
}

const helloButton = document.querySelector( '.js-hello' );
helloButton.addEventListener( 'click', helloListener );
```

First, we created a `helloListener` function. This function prevents the default action of the event, which is the submission of the form. 

The second line in the function creates a console log that appears in the developer tools of your browser. More on this later.

The last line attaches the `helloListener` function to the button. We tend to use `js-` prefixed classes to refer to elements in the Document Object Model, also known as the DOM. The `document.querySelector` function takes a selector string, in this case a class name, and locates the node in the DOM that has this class. Check out the HTML file, you can see the same class in the class list of the button.

Once we located the `.js-hello` button, we can add an event listener function to it. This function takes an event, and can perform any JavaScript action ranging from manipulating the contents you can see on screen to calling a service or an API on the web, saving your data in a persistent storage.

There is only one problem with this code: we don't have access to it in the HTML file. Let's change this by adding an HTML tag at the bottom of the body.

```
<!doctype html>
<html lang="en">
  <head>
    <title>Greetings</title>
  </head>
  </body>
    <form>
      <input type="text" 
             class="tf-large  js-name" 
             placeholder="name">
      <button class="btn-large  js-hello">Greet</button> 
    </form>
    <script src="js/form.js"></script>
  </body>
</html>
```

If you did everything correctly and saved all the files, after opening the `greeting.html` file in your browser, the name does not disappear once you press the Greet button.

> Note that there are other ways to insert JavaScript code into an HTML document. I highly recommend sticking to the above method, but for completeness, feel free to read [this article](https://www.w3schools.com/js/js_whereto.asp).

JavaScript is executed in the browser using the JavaScript interpreter. JavaScript is an interpreted language, which means that it runs JavaScript as it appears in the file without compiling it to an intermediate representation.

### Developer Tools

Each browser has developer tools. For simplicity, I will use Google Chrome in this article, but most browsers have similar functionality.

Right click on your website anywhere inside the browser window, and select `Inspect` from the context menu. You will find yourself inside the developer tools. Find the `Console` tab. Assuming you have clicked on the button, you can find the following there:

```
button pressed
>
```

You can execute any JavaScript expression by writing it after the `>` prompt:

```
button pressed
> 2+2
4
> helloButton
    <button class="btn-large  js-hello">Greet</button>
```

The `helloButton` variable stores a DOM node, fully accessible in JavaScript.


### Greeting the User

Let's use the console to get the name entered in the textfield

```
> document.querySelector( '.js-name' )
    <input type="text" class="large-text  js-name" placeholder="name">
> document.querySelector( '.js-name' ).value
    Zsolt
```

Instead of a console log, we need to get the value of the textfield and display a greeting in an alert box:

```
function helloListener( event ) {
    event.preventDefault();
    const name = document.querySelector( '.js-name' ).value;
    alert( 'Hello, ' + name + '!' );
}

const helloButton = document.querySelector( '.js-hello' );
helloButton.addEventListener( 'click', helloListener );
```

The `+` operator on strings concatenates strings. The `alert` function creates an alert box. 

If you test the code, you can see that everything is in place.



### Styling

We know that 

- the static markup providing information on the structure of the website is in the HTML file,
- the dynamic functionality goes in the JavaScript files.

Many people think that the look and feel of the page is also defined in the HTML file. This approach is wrong. Styling is separated from HTML. 

We describe styles in CSS (Cascading Style Sheets) files.

```
.tf-large {
    font-size: 1.5rem;    
    padding: 1rem;
}

.btn-large {
    font-size: 1.5rem;
    padding: 1rem;
    font-weight: bold;
}
```

Similarly to JavaScript, we need to reference the CSS file from the HTML document. We do it in the head using a `<link>` tag:

```
<!doctype html>
<html lang="en">
  <head>
    <title>Greetings</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  </body>
    <form>
      <input type="text" 
             class="large-text  js-name" 
             placeholder="name">
      <button class="btn-large  js-hello">Greet</button> 
    </form>
    <script src="js/form.js"></script>
  </body>
</html>
```

If you reload the page, you can see the changes on screen. 

There are other ways to insert stylesheets into the HTML documents, but stick to external files so that you separate concerns. HTML should contain markup, CSS should contain styles. If you need more information on the basics of CSS, check out [w3schools.com](https://www.w3schools.com/html/html_css.asp).


### HTML classes: separation of concerns

Recall the button `<button class="btn-large  js-hello">Greet</button>`. You can see two classes in there, `btn-large` and `js-hello`. The first class is used solely for styling, and the second class is used solely for referencing in JavaScript.

No-one forces you to write code this way, but it pays off to separate classes for styling and functionality. When multiple people work on the same codebase, this separation pays off. This way, a person responsible for styling can add, delete, or rename any styling classes without affecting functionality. JavaScript developers can do the same thing with the `js-` prefixed classes.

> `js-` prefixed classes should be used for functionality, while regular classes should be used for styling.

### Why aren't we using HTML IDs?

You may know from your studies or previous work that we can also reference DOM nodes using their ID attributes:

```
<div id="intro">This is an introduction</div>
```

If you have the above node in the DOM, you can reference it using

```
document.getElementById( 'intro' )
```

The problem with ID attributes is that they have to be unique for the whole document. If you violate this rule, you get an HTML error.

In big websites and applications, most developers never know the context in which their markup will appear. Chances are that if you use an ID attribute name, someone else will do the same elsewhere.

> As two DOM nodes cannot have the same ID, using ID attributes is not advised in most cases. 

Once a business owner asked me to try out his affiliate plugin, because it was not working for him. Sure enough, I filled in the form, but once I pressed register, nothing happened. I checked the developer tools of the browser, and it turned out that there were some duplicated ID attributes in the markup. 

I asked him how many times he included the affiliate plugin. He said, once for desktop computers, and once for mobile. He proudly told me that he made the mobile version hidden when someone checks it in a desktop.

Unfortunately, he only managed to hide it using a CSS style (`display: none`). The markup was in his document with the exact same ID attributes as the other version.

```
<div id="affiliate-plugin" class="desktop">
    <!-- Content goes here -->
</div>
<div id="affiliate-plugin" class="mobile  hidden">
    <!-- Content goes here -->
</div>
```

The above markup is erronous due to the duplicated ID attributes. My entrepreneur friend, lacking web development knowledge, lost hours on not knowing the fundamentals. You can now save these hours next time you encounter a similar situation.


### What do we do with multiple JavaScript and CSS files?

In large projects, placing all the JavaScript code in one file is not advised for development. Therefore, we often have hundreds if not thousands of JavaScript and CSS files.

Placing all these files in the HTML markup is not advised either, because enumerating hundreds of files in the markup is neither convenient, nor efficient. You may also encounter JavaScript errors if you include the JavaScript files in the wrong order.

> For large projects, use Webpack and npm (Node Package Manager) to bundle your files into one file that you can include in your markup.

You can learn more on npm modules and Webpack [in my article](https://www.zsoltnagy.eu/using-es6-modules-with-webpack/). The syntax may be a bit too advanced for you at this stage. You will understand everything if you sign up for my ES6 Minitraining at the bottom of this article.

In a large project, I highly recommend that you learn and use SASS. SASS not only enriches your CSS syntax, but it helps you structure it better. Check out my SitePoint article titled [CSS Architecture and the Three Pillars of Maintainable CSS](https://www.sitepoint.com/css-architecture-and-the-three-pillars-of-maintainable-css/) on this topic.
