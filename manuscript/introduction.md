# Introduction

If you have read most of the blog posts of zsoltnagy.eu, you can conclude that most of the articles require at least some basic knowledge about JavaScript. The main exception is the  [JavaScript Basics](http://www.zsoltnagy.eu/category/javascript-basics/) category.

I wrote this book to bridge the gap between my less experienced audience and the knowledge required to understand my more advanced content on JavaScript. This book requires absolutely no JavaScript knowledge.

To gain some leverage on learning JavaScript, it is important to see why it is worth learning the language in 2019 and beyond.

- why today is the best time to get started with JavaScript,
- what your career prospects are,
- and why JavaScript provides you with a close to optimal learning experience in 2019.

## The Mission of this Book

I am on a mission to create the best JavaScript resource for beginners to learn coding in JavaScript.

This mission was inspired by my video course ES6 in Practice, that was initially marketed to a wide audience: beginners, intermediates, and experts. While intermediate and expert developers really liked the resource, beginners got stuck, because pace was too fast for them, and the exercises were too demanding.

The mission of this book is to make JavaScript understandable. I have no intention to replace the documentation, simply because the purpose of the documentation is to be complete. In the courses accompanying this book, my objective is to transform your coding skills.

This mission will take long to accomplish, and you can also be a part of it. If you have any feedback, feel free to send me an email at [info@zsoltnagy.eu](mailto:info@zsoltnagy.eu).

Let's continue with the history of JavaScript.

## JavaScript on the Client

Chances are that you accessed this book via a web browser such as Google Chrome or Firefox. Websites that are displayed in the browser are primarily written in three languages: HTML, CSS, and JavaScript.

HTML (Hyper Text Markup Language) describes the structure and content of a website. CSS (Cascading Style Sheets) works with presentation: it determines which font, colors, background images etc. are used to display the website.

JavaScript is a full-fledged programming language that can not only animate and modify elements on screen, but it can perform many other tasks, such as:

- communication with a server, providing and storing data,
- description of application logic: for instance, the application logic can validate the personal data you entered,
- visualization: for instance, JavaScript can draw a chart displaying the stock price of Google.

> *Animation* in computer science is the act of moving or transforming an object on screen. During the move, the features of the object may change, which means that the animated object may be drawn in different color, different size, or in case of three dimensional animation, we might see the object from a different angle.

Transforming an object means that a feature of the object changes in time. We can change many features of the object, such as its color, its shape, or its orientation.

JavaScript has been clearly the language to go to when it comes to client side development. Let's stop for a moment. What is client side and what is server side?

> *Client-side* development focuses on writing code that runs in the browser of the end user. *Server-side* development focuses on writing code that runs on the server of the service provider.

When a client retrieves the stock price of Google from a server, a server-side program queries data on the Google stock from a database. Then these data are transmitted to the client using a specified format. The client can then read the data and display a graph on the historical stock prices.

Back in the 90s and early 2000s, JavaScript was a little toy language that could *animate* elements on a static website. These animations were called *dynamic behavior*.

> Displaying an object on screen at a given point in time is called *rendering*.

Animation can also be defined by continuously rendering an object on screen, while its features may change.

Twenty years ago, JavaScript was not taken seriously in the software development industry. Many "developers" had no idea what they were doing, and they just copy-pasted code snippets to add some dynamic behavior to their site. Often times, these snippets clashed with each other, because they used the same variables.

JavaScript became more popular, once *AJAX* programming (Asynchronous JavaScript and XML) started spreading. In 2006, the `XMLHttpRequest` object became standardised, meaning that you could submit a request to the server and await for its response. Once the response arrived, you could display the results *without reloading the page*. This worked like magic on websites, because before this technique became wide-spread, every interaction with the server required a full page reload. As a page reload may take seconds, getting rid of the need for reloading pages was a big achievement.

The JavaScript community was growing, but we had another problem at hand: in order to write code that works in all major browsers, we had to write different code for different browsers. Sometimes the situation was hopelessly confusing. Therefore, you had to be a domain expert to write JavaScript code.

Not for long though. In 2006, another important milestone happened. The library `jQuery` got released with the slogan *write less, do more*. Instead of writing tens of lines of code to make sure you covered all browsers, jQuery gave you single line commands to achieve the same result. You didn't have to be a serious software developer to write JavaScript code. You just had to include jQuery, and your problems were solved.

Unfortunately, jQuery created another problem. We could use the slogan of Scarlet Spider, the evil clone of Spider-Man: *all the power, none of the responsibility*. Lowering the entry barriers meant that people who didn't care about software engineering, also started writing code.

At the same time, the idea of *single page applications* and *client-side rich web-applications* became mainstream. Before AJAX and jQuery, almost everything was on server-side. The task of the server was to assemble a web page, and send it to the client. The server created HTML, CSS, and JavaScript code, and the client only loaded that one page. This changed when rendering and some parts of the application logic was moved to the client. This meant the application had to be loaded once, and multiple megabytes of JavaScript code was responsible for rendering the part of the application the client was interested in. This step was made possible by Moore's law, because the performance of the end user's computers doubled every few years.

> *Single-page applications* receive all the HTML, CSS, and JavaScript on page load, and the client can navigate between different views of the application without informing the server. The client communicates with the server with AJAX calls, and receives data without the need to reload the page. This way, single-page applications became faster, and as easy to use as a desktop application.

From the above five traits, scalability of an application means that the application gives a response that can be calculated easily as a function of increased load. Scalability can be defined on resources and development processes. For instance, if a server guarantees an average response time of 1 second per 100 concurrent users, we need to know the server guarantees for 1000, 10000, or 100000 concurrent users. An example for the scalability of a process  can be the average time needed to fix a bug in an application having ten thousand, hundred thousand, or a million lines of code. Another scalability metric of a development process could be the number of mistakes made per thousand lines of code in an application having ten thousand, hundred thousand, or a million lines of code.

The main problem was that people calling themselves software developers, used their hacking skills to create bad quality software. People soon realized that some jQuery knowledge limits the size of the application they can develop. Beyond a certain size, they encounter maintainability issues.

> *Maintainability* is the act of making a software solution easy to develop, modify, scale, test, and debug. If you write ten lines of code, you need a different approach than writing a million lines of code.

The answer to the maintainability issue was the emergence of JavaScript frameworks. Frameworks made it possible to write maintainable code in a structured way, without the need to reinvent the wheel. Frameworks enforced some well known best practices from the field of software-engineering. In order to understand these best practices, the entry barriers got raised again to a healthy level.

> A *framework* structures your code and runs your application. When using a framework, the framework is *in control*. This means, the framework calls your code.

> A *library* is a set of functionalities that you can call to perform a given task. A library is not a framework, because as long as you use a library, you are in control, the library does not call your code.

In the early 2010s, literally everyone wanted to write a framework. A new framework got created literally every week. Creating a framework means that you reinvent the wheel, because you solve a well known problem in your own way. If you want to build a portfolio, don't even think about building a framework, because it does not make sense.

Fortunately, we are past the time when the *churn rate* of JavaScript development was so high that you had to learn a new framework or library every month. Today, it is quite clear that you use React or Angular or Vue. Based on Google search data, React seems to be winning the overall battle, but Angular and Vue also have their niche. There is a big open source community behind the main frameworks, because React is backed by Facebook, and Angular is backed by Google.

> *Open source communities* are formed around the idea that anyone can contribute to the source code maintained by the community. The strength behind popular open source communities is that major errors are reported and fixed fast, and the progress of development is continuous. As a result, we can trust open source communities in ensuring a certain quality standard.

The frameworks were also great, but developers had one more problem. The frameworks and libraries were so much beyond the capabilities of JavaScript that learning the ins and outs of JavaScript appeared to have become unnecessary. The language was already quite old, and we needed an update. This update was ES2015, or using its old name, ES6. Many innovations made it to ES6 from different sources such as jQuery, some frameworks, some functional programming libraries like UnderscoreJs, and some languages like TypeScript.

> ES stands for ECMAScript. *ECMA International* (ECMA = European Computer Manufacturers Association) is a standardizing organization founded in 1961. ECMA International is responsible for the standard describing languages like JavaScript and ActionScript. The standard describing the latest JavaScript language is ECMA-262.

Around the time when ES6 emerged, old browsers like Internet Explorer 8 became so unpopular that there was hardly any demand to provide compatibility with them. This resulted in more compact and more uniform JavaScript code.

Since ES2015, there was no turning back. Every year, some updates made it to JavaScript, and these updates also ended up in my course, [ES6 in Practice](http://www.zsoltnagy.eu/es6-in-practice).

We can conclude based on the history of JavaScript that there has never been a better time to be a JavaScript developer. In many companies, you can make more money than a C++ developer or a PHP developer. Just look at stackoverflow.com jobs or payscale.com data. The challenges you deal with on a daily basis are interesting, and more importantly, you often get immediate feedback on your efforts by seeing the effects of your changes in your browser thanks to the *live reload* feature automatically reloading your updates.

A> Summary:
A>
A> - JavaScript was first a toy language for creating dynamic behavior
A> - AJAX made it possible to update websites without reloading the page of the application
A> - jQuery lowered the entry barriers to programming the web
A> - Frameworks and libraries forced us to use well known design patterns in software engineering
A> - Old browsers such as IE8 lost popularity, and the new browsers helped JavaScript developers by implementing the JavaScript standard more closely
A> - ES2015 and beyond: many patterns became standard part of the language

## JavaScript on the server

If these benefits were not enough for you, let's add some more sauce to the mix.

JavaScript is not just a client-side language anymore. Node.js makes it possible to run JavaScript on the server. Node.js is built on the foundations of the execution engine of Google Chrome, called V8. Recall that even Michael Schumacher won his first world championship using a V8 engine. The V8 engine is fast like a Formula One car. The V8 compiler turns JavaScript to machine code, which means that on the server, we are not dealing with *interpreted* code anymore.

> *Interpreted code* runs on a *virtual machine*, translating the sets of instructions written by a developer to executable commands. Interpreted languages are typically slower than *compiled* languages. Interpreted languages are also *portable*, which means that you can take the source code of a program and execute it on any system that has a virtual machine for that specific code. Languages that compile to *machine code* have the benefit of running code as close to machine code level as possible. This translates to faster execution times. Unfortunately, this machine code cannot be *ported* to different machines running different operating systems or having different hardware architecture.

Node.js solved the speed problem by offering a compiler to machine code. This is not a big deal yet, because most other server-side languages can do the same thing. Why is node.js still a good choice for certain server-side tasks?

The reason lies in some node.js architectural decisions. Node.js comes with an *event loop* that can execute and serve parallel requests on the server without blocking. This is called *non-blocking I/O*. Opposed to many other languages, when you have to read or write a database or a file, node.js is not blocked until the I/O operation is finished. This means that node.js stays busy handling other tasks, possibly important for other clients.

> *Architecture* is the product of an *architect*, describing the principles of how a system works. *Software architecture* describes the structure of how a system works.

> *I/O operations* are Input/Output operations. Input stands for inputting data into a system. Examples: typing, moving a mouse, taking a photo or a screenshot, downloading data, or requesting our bank statement. Output operations are described as data sent by the system. Examples: display or print text, upload files to a server, or respond to a bank statement query in a specified format.

Think about it for a moment. When is this feature beneficial?

> Node.js shines when there are a lot of independent parallel requests requiring a lot of I/O operations, but not many server-side computations.

For instance, a 3D renderer algorithm comes with a lot of operations. Even though the V8 engine produces fast machine code, there are some other languages that are faster. Node.js only gets the edge over these languages once we deal with many inexpensive operations.

In today's world, this use case happens to be very popular. The computers of the end users are strong enough to run a lot of logic on client side, including presentation of data by rendering charts, tables, and other components. The application server provides data through APIs (Application Programming Interface), and mostly interfaces database servers and file servers. The application server receives API requests and formats data for API responses in a way that clients can fetch and understand them using AJAX requests.

> *API (Application Programming Interface)*: describes the way how an application can be used, including a communication protocol. The description is made from the perspective of an external user. The API of a *service* running on an *application server* is described as a set of *endpoints*. Endpoints can be called using *requests*. A *request* typically contains a web address (URL - Uniform Resource Locator) and *payload* data. The *response* of an API contains information presented in a specified format such as JSON (JavaScript Object Notation) or XML (eXtensible Markup Language). The API response and the API request payload typically share the same format, and the primary format for JavaScript APIs is JSON. The user of a server API is typically a client-side JavaScript application or code running on another server.

The role of the server is limited to purposes that do not require a lot of computing power per request. In other words, most API requests are not CPU intensive. These constraints provide an optimal environment of node.js.

A lot of problems have been solved effectively by *microservices*. You can simply query a microservice to perform a CPU-heavy operation, often on another server, using a different technology. If you are interested in microservices, [check out my introduction on this topic](http://www.zsoltnagy.eu/an-introduction-to-microservices/).

As a conclusion, once you learn client side development, you can upgrade your skills to perform server side development as well. Developers who are good at both client side and server side development are called *full stack developers*. Full stack development is a great career path upgrade for you in case you are looking for more responsibility in a smaller company. These companies typically provide fast career progress in exchange for you taking more responsibility to help out the company.

A> Summary:
A>
A> - JavaScript is compiled to fast machine code, using the V8 engine of Google. This code can run on the server.
A> - Node.js comes with non-blocking I/O, making it possible to handle many I/O operations in parallel.
A> - In today's world, many computation heavy tasks are either performed on client side or by using a specialized microservice. Therefore, node.js is an excellent choice for implementing less resource-intensive APIs that require servicing a lot of parallel requests.

## Other JavaScript Use Cases

JavaScript development is fun. Originally, the primary use case of JavaScript was client side development for web-browsers. Then came node.js with the ability to write server-side code. JavaScript has a lot more to give in 2019 though. Let's see some of the more exotic options:

- **JavaScript and VR.** [React 360](https://facebook.github.io/react-360/) makes it possible to deliver VR experiences using JavaScript. [Some other libraries](https://github.com/ku-fpg/vr-ideas/wiki/JavaScript-VR-libraries) help you with VR as well.
- **JavaScript can compile to other languages, and other languages can be compiled to JavaScript.** *WebAssembly* makes it possible to compile many languages to JavaScript so that you can run code in the browser. We can even use code written in these languages in our JavaScript code.
- **Machine Learning, AI in JavaScript.** [TensorFlow](https://js.tensorflow.org/), Google's machine learning library containing neural network implementations, is also available in JavaScript. Many other libraries for machine learning and artificial intelligence are also available.
- **Mobile development.** [React Native](https://facebook.github.io/react-native/) provides a way to perform mobile development using JavaScript. Native mobile apps and JavaScript are an amazing combination, because of the facilitation of code reusability.
- **Blockchain Programming.** At the time of writing this section, there are more than a thousand blockchain-related libraries on npm ([proof](https://www.npmjs.com/search?q=keywords:blockchain)). [Crypto-js](https://www.npmjs.com/package/crypto-js) provides us with easy-to-use encryption and decryption algorithms. Everything is set to implement blockchains in JavaScript.
- **Real Time Communication on the Web**: video and audio streams can be controlled using JavaScript. The [WebRTC](https://webrtc.org/) open source project makes it possible to create applications with real time communication.
- **Microservices**. [Seneca](http://senecajs.org/) is one example for organizing microservices in your application.

If you are an intermediate to advanced JavaScript developer, and you are interested in the latter two use cases, check out my video course on Packt Publishing: [Beginning Modern JavaScript Development with Microservices, WebRTC, and React](https://www.packtpub.com/web-development/beginning-modern-javascript-development-microservices-webrtc-and-react-elearning-video).

JavaScript may or may not be optimal for certain tasks. Obviously, if a task is computation intensive, such as character animation and shading in three dimensions, JavaScript may not be the optimal language to write applications that perform these operations. However, JavaScript execution environments are continuously improving, and new use cases emerge on the horizon, where using JavaScript is an alternative. Remember, if a use case becomes feasible in JavaScript, chances are, a big passionate community will soon be formed around it. Chances for corporate support are high as well.

## JavaScript Domination on the Job Market

According to the [2018 survey of HackerRank](https://research.hackerrank.com/developer-skills/2018/),

- JavaScript is the number 1 language employers are looking for. In total, 47.8% of employers post JavaScript positions
- There is a big gap between employer demand and employee knowledge in JavaScript frameworks. The biggest gap is with React: 33.2% of employers are looking for React developers, while the supply is only 19%. Scarcity translates to more money, less competition, and more opportunities.
- You can be a self-taught developer, because companies place significantly more emphasis on experience (90.6%), your portfolio (72.7%) than on education. If you market it properly, experience can be gathered developing your personal projects, which will end up in your portfolio. This means, in JavaScript development, only your efforts limit you, there are no gatekeepers, universities, internships, or certification industries. In Berlin/Germany for instance, you can become a self-taught programmer on your own, and you can get hired for a higher salary than the average salary for a German citizen. In case of many cities or remote work opportunities, the same principle applies.
- Although JavaScript only ranks fifth in languages developers prefer behind Python, C, C++, and Java, this might be offset by the bad experience coming from older people who had to deal with the immature version of JavaScript. When it comes to developer experience, an important metric is that out of all frameworks of all languages, the top four are JavaScript frameworks: Node.js, React, ExpressJs, and AngularJs. Working with these frameworks makes developers happier than anything else.

The [2018 survey of StackOverflow](https://insights.stackoverflow.com/survey/2018/) paints the same picture:

- JavaScript is the most popular language with a share of 69.8%. On StackOverflow, JavaScript is more popular than Python.
- Three frameworks lead the list of most popular frameworks: Node.js, Angular, React.
- Salaries of JavaScript developers are marked lower in this survey than the salary paid in many other fields. In my opinion, this statistic is misleading, because the salaries of experts are overshadowed by the salaries of entry level developers more than in case of a language requiring a lot of expertise. In an average JavaScript first interview, based on my experience, it is not uncommon to filter out 70% of the applicants. In an average C++ interview on the other hand, people who reach the first interview know a lot better what they are doing. I encourage you to do your own research on payscale.com or glassdoor.com to find specific JavaScript developer salaries of companies that require your skills.

Although the audience matters, in today's world, you cannot really go wrong with JavaScript. You can also expect that JavaScript stays in an uptrend.

A> Summary:
A>
A> - JavaScript and JavaScript frameworks are popular in the industry
A> - Demand for JavaScript developers is higher than the supply

## Why is it easier than ever to become a JavaScript developer?

We have already dealt with the economical aspect of becoming a JavaScript developer. There is no doubt about the high demand for JavaScript developers both on client side and on server side.

There is no money in the world that would compensate you for a bad developer experience though.

Learning JavaScript is easier than ever before. Years ago, a lot of frustrations prevented an average developer from experiencing an optimal learning experience:

- Computer resources were more scarce than now
- The standardization of the language was a lot more immature than now, yielding to `if`-`else` structures containing different code snippets for each browser,
- The ES5 standard provided a lot worse developer experience than ES2015 and beyond
- JavaScript was not regarded as a serious programming language,
- Browser developer tools and debugging capabilities were immature,
- Third party library support was scarce and unreliable,
- Good integrated development environments or text editors did not exist,

Talk to anyone who wrote JavaScript code fifteen years ago, and you can conclude, you are not working with the same language anymore.

If there is a problem, a passionate open source community, as well as tech giants like Google or Facebook, are likely to provide you with a reliable JavaScript solution. Since 2015, standardization also started speeding up. We are living in the greatest time of JavaScript history. And it's just going to be better.

## JavaScript learning experience according to science

The first good news is that you can immediately start writing code. The second good news is that you can see the effect of your efforts within a seconds. You don't need to go through a long compilation process, and the things you build with JavaScript often manifest in visible changes on screen.

While I am not claiming that learning JavaScript is super easy, I do claim that you get more direct and immediate feedback when dealing with JavaScript than with most other languages. Why does this matter?

Because everything is given for you to experience [flow](https://en.wikipedia.org/wiki/Flow_(psychology)). Flow experiences are often referred to as optimal experiences. It feels like you are "in the zone". If you are in flow, time flies. You are deeply immersed in an activity. Your learning experience becomes close to optimal.

According to science, there are a few necessary conditions for flow to happen:

1. The goals of the activity must be clear
2. The task is neither too easy, nor too hard
3. You get direct feedback on the outcome of your actions

Let's see these points one by one.

**The goals of the activity must be clear**

Regarding the goals, just look at the two developer surveys and figure out whether it makes sense for you to become a JavaScript developer in 2019. You can literally work from the beach as a freelancer, or as an employee, being part of an international team. Writing JavaScript code often feels like playing with LEGO. You also happen to make good money with it. Many people are productive as junior developers within half a year. If you can't write code right now, what better experience could you imagine for yourself than utilising your skills as a frontend or full stack developer?

**The task is neither too easy, nor too hard**

Learning JavaScript is not an obvious thing to do. There are some riddles, some pitfalls, some hurdles you need to go through. Don't let this discourage you though! Just think about it. Who would you be if you never faced a challenge? There would be nothing you are proud of in your life right now. These hurdles serve your benefit. These hurdles also make your learning experience hard enough so that you can experience flow learning JavaScript.

My opinion is that learning JavaScript is not too hard to experience flow. Obviously, this opinion is debatable, because if you worked as a bus driver for instance, and you have never seen a programming language before, you will need some fundamentals. I admit, my learning resource, [ES6 in Practice](http://www.zsoltnagy.eu/es6-in-practice) is not an optimal resource for absolute beginners, because it assumes you know at least the basics of how programming languages work, what if statements and loops are, what functions are etc. I am planning an entry level product for JavaScript, and I know, advanced JavaScript may be too hard for some people. I wrote this book based on the feedback of my clients who struggled with ES6 in Practice.

However, once you lay down the foundations, you will be ready for more advanced resources, and nothing will stop you. Therefore, with proper guidance, you will improve, you will get better, without getting frustrated about your experience of learning JavaScript.



**You get direct feedback on the outcome of your actions**

This is where JavaScript shines. As long as you use JavaScript on client side, and you don't complicate your tooling too much, you will get immediate feedback on your actions. Sometimes you just have to refresh your browser. In some cases, you don't even need a browser refresh. Whatever you do, you will immediately see the results of your code.

For this reason, JavaScript is a great candidate for flow experience. Python is the only language I am aware of that may be comparable to JavaScript in terms of reaching flow fast.

## Summary

Regardless of whether you want to learn JavaScript, or you want to choose or change your specialization, it is important to take a moment and appreciate the current state of JavaScript.

Things were not always as bright as in these days. In the first half of the chapter, we went through the dark history of JavaScript on client side, then we transitioned to the somewhat brighter and shorter history of JavaScript on the server.

These events made it possible for JavaScript developers to experience growth way beyond what we imagined ten years ago. An avalanche of use cases await JavaScript developers, such as VR and Blockchain technologies, helping JavaScript conquer new horizons.

As JavaScript continuously gained popularity, software developers who specialize in technologies that include JavaScript have a bright present and future. Two developer surveys concluded that you cannot really go wrong with betting on JavaScript.

If you would like to learn JavaScript, the last part of this chapter concluded that JavaScript is close to optimal in terms of supporting you reach an optimal learning experience. Given that you often experience an immediate feedback to your actions, as long as you stick to reasonable challenges, you can expect to spend more development and learning time in flow than in case of many other languages.
