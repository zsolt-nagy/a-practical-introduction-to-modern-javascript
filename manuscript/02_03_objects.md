## Using Objects in JavaScript

We learned in the introductory chapter that objects are collections of data and operations that are related. Objects help you group any number of values using one reference.

Data fields stored inside an object are called *properties*. 

Operations that can be executed on an object are called *methods*.

Let's see an example:

```
let account = {
    owner: 'Zsolt',
    amount: 1000,
    deposit: function( depositAmount ) {
        this.amount += depositAmount;
    }
}
```

Notice that we can have access to properties of the objects inside methods by using the `this` keyword.


There are two notations to retrieve the field values of an object:

- dot notation: `account.amount`,
- bracket notation: `account['amount']`.

```
> account.owner
'Zsolt'

> account.deposit( 1000 )
undefined

> account.amount
2000
```

Both notations can be used to get and set values of objects, and delete properties of an object:

```
account.owner = null;

account['x'] = true;
delete account['x'];
```

For instance, the above expression sets `account['owner']` to `null`. Note that the type of the new value does not have to match the type of the original value.

To remove a field from an object, use the `delete` operator:

```
> account
{owner: null, amount: 2000, deposit: ƒ}

> delete account.owner
true

> account
{amount: 2000, deposit: ƒ}
```

The expression `delete account.owner` removes the `owner: null` key-value pair from the object. The expression is then evaluated to `true`, because the deletion succeeded.

We have seen one way to create objects: the object literal notation. An empty object can be created using `{}`. After creation, properties and operations can be added to it:

```
const objectLiteral = {};
objectLiteral.property = 1;
objectLiteral.operation = () => 1;
```

Including the `{}` notation, there are three ways of creating an empty object:

-  `{}`,
- `new Object()`,
- `Object.create( Object.prototype )`.

The third option looks a bit alien to many JavaScript developers, but we will still use it, because it gives us an easy way to set the *prototype* of an object during creation.

We will now cover more advanced Object concepts:

- enumerating object property names and values,
- the global object,
- own properties and inherited properties,
- object properties and their settings,
- freezing and sealing objects,
- getters and setters,
- property shorthand notation,
- computed object keys,
- equality,
- mixins and shallow copies with `Object.assign`,
- destructuring objects,
- spreading objects,
- symbol keys.

In this section, we will not deal with the prototype chain, setting the prototype of an object, or getting the prototype of an object. 

### Enumerating object property names and values

We can retrieve an array of object keys, values, and entries, using the `Object.keys`, `Object.values`, `Object.entries` methods respectively. `>` indicates the prompt of the console.

```
let account = {
    owner: 'Zsolt',
    amount: 1000
}

> Object.keys( account )
["owner", "amount"]

> Object.values( account )
["Zsolt", 1000]

> Object.entries( account )
[["owner","Zsolt"],["amount",1000]]
```

The `for...in` loop may also enumerate properties:

```
> for ( let property in account ) {
      console.log( property );
  }
owner
amount
```

### The global object

We have not covered inheritance yet. However, it is worth noting that it is possible to enumerate properties of objects that do not come from the object itself.

Inheritance of object properties is defined via the *prototype chain*. Some object properties are inherited from the prototype of our object, or the prototype of the prototype of our object, and so on.

The global `Object` sits at the top of the prototype chain. This object has many properties that are made accessible in any object we create.

```
let account = {
    owner: 'Zsolt',
    amount: 1000
}

> account.toString()
"[object Object]"

> account.constructor
ƒ Object() { [native code] }

> account.__proto__
{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, 
hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
```

All these properties come from the global object.

```
> Object.toString
ƒ toString() { [native code] }

> Object.constructor
ƒ Function() { [native code] }

> Object.__proto__
ƒ () { [native code] }
```

Many of these properties are *not enumerable*, this is why they do not make it to the results of `for...in` loops, `Object.keys`, and `Object.entries`. 

> Enumerability is a configuration option for JavaScript object. We will cover it soon.

At this stage, do not worry about the prototype chain of JavaScript objects. All you need to know is that it exists, and each object you create inherits properties from the global object. Later, we will learn how to set the prototype of objects.

### Own properties and inherited properties

We learned that some properties of the global object are not enumerable.

This is not necessarily the case for all properties. For instance, we can define an enumerable property for the ancestor of our object in the prototype chain. This property makes it to the enumerations of any object we create:

```
const account = {
    owner: 'Zsolt',
    amount: 1000
};

Object.prototype.objectProperty = true;  

for ( let property in account ) {
    console.log( property );
}
owner
amount
objectProperty

```

This holds even if we create a new empty object:

```
for ( let property in {} ) {
    console.log( property );
}
objectProperty
```

Let's examine this property a bit further. When console logging a new object, initially, we cannot see anything:

```
> console.log( {} )
 ►{}
```

However, when clicking the printed empty object, we can discover that it has a `__proto__` member:

```
> console.log( {} )
 ▼{}
  ►__proto__: Object
```

When expanding `__proto__` further, we can see a lot of methods as well as the `objectProperty` that was previously defined.

```
> console.log( {} )
 ▼{}
  ▼__proto__: Object
    objectProperty: true
   ►constructor: ƒ Object()
   ►hasOwnProperty: ƒ hasOwnProperty()
   ...
```

All these properties come from `Object.prototype`.

Interestingly enough, in the enumeration, the second inherited method is `hasOwnProperty`. This is a perfect segway towards one way to filter out inherited properties:

```
for ( let property in account ) {
    console.log( property );
}
owner
amount
objectProperty

for ( let property in account ) {
    if ( account.hasOwnProperty( property ) ) {
        console.log( property );
    }
}
owner
amount
```

`Object.keys` and `Object.entries` automatically performs the `hasOwnProperty` check, and only displays own properties:

```
> Object.keys( account )
["owner", "amount"]

> Object.entries( account )
[["owner","Zsolt"],["amount",1000]]
```

`Object.getOwnPropertyNames` gives you access to the names of the own properties of an object as well:

```
> Object.getOwnPropertyNames( account )
["owner", "amount"]
```

The difference between `Object.keys` and `Object.getOwnPropertyNames` is that the former only returns enumerable own property names, while the latter returns all own property names:

```
Object.keys( Object.prototype )
["objectProperty"]

Object.getOwnPropertyNames( Object.prototype )
(13) ["constructor", "__defineGetter__", "__defineSetter__", 
"hasOwnProperty", "__lookupGetter__", "__lookupSetter__", 
"isPrototypeOf", "propertyIsEnumerable", "toString", "valueOf", 
"__proto__", "toLocaleString", "objectProperty"]
```

It is also possible to access the configuration settings of an object using `Object.getOwnPropertyDescriptors`. This leads us to the next section.

### Object property settings

All object properties have settings:

- `configurable`: determines if the property behavior can be redefined. This means, we can make an object non-configurable, non-writable, or non-enumerable only if `configurable` is set to `true`. Only configurable properties can be removed with the `delete` operator.
- `enumerable`: determines if the property will show up in an enumeration (such as `for...in` loops and `Object.keys`)
- `value`: returns the value of the property
- `writable`: determines if the value of a property can be changed by assigning it a new value

We can access these configuration settings using `Object.getOwnPropertyDescriptors`.

```
> Object.getOwnPropertyDescriptors( {a: 1} );
{ 
    a: {
        value:1,
        writable:true,
        enumerable:true,
        configurable:true
    }
}
```

It is also possible to access the property descriptor belonging to a single property:

```
> Object.getOwnPropertyDescriptor( {a: 1 }, 'a' )
{value: 1, writable: true, enumerable: true, configurable: true}

> Object.getOwnPropertyDescriptor( {a: 1 }, 'b' )
undefined
```

Let's create an empty object using the object literal.

```
const objectLiteral = {};
objectLiteral.property = 1;
```

Instead of `objectLiteral.property`, we can also define properties using the `Object.defineProperty` method. `Object.defineProperty` takes three arguments:

- an object reference,
- the property name,
- a configuration object including `value`, `configurable`, `enumerable`, and `writable`. If any of the options `configurable`, `enumerable`, or `writable` are missing, their default value is `false`.

```
Object.defineProperty(
    objectLiteral,
    'definedProperty',
    {
        value: 'propertyValue',
        configurable: true,
        enumerable: true,
        writable: true
    }
);
```

Let's experiment with different property configurations. `>` indicates the prompt of the console.

```
Object.defineProperty(
    objectLiteral,
    'nonConfigurable',
    {
        value: 'v',
        configurable: false,
        enumerable: true,
        writable: true
    }
);

> delete objectLiteral.nonConfigurable
false

> objectLiteral.nonConfigurable
"v"

> Object.defineProperty(
      objectLiteral,
      'nonConfigurable',
      {
          value: 'w',
          configurable: true,
          enumerable: true,
          writable: true
      }
  );
Uncaught TypeError: Cannot redefine property: nonConfigurable
    at Function.defineProperty (<anonymous>)
    at <anonymous>:1:8  
```

Non-configurable properties:

- cannot be deleted,
- cannot be reconfigured.

Let's experiment with non-enumerable properties.

```
Object.defineProperty(
    objectLiteral,
    'nonEnumerable',
    {
        value: 'ne',
        configurable: true,
        enumerable: false,
        writable: true
    }
);

> for ( let p in objectLiteral ) console.log( p );
property
definedProperty
nonConfigurable

> Object.keys( objectLiteral )
["property", "definedProperty", "nonConfigurable"]
```

The non-enumerable property does not show up neither in `for...in` loops, nor in the `Object.keys` enumeration.

Finally, non-writable properties don't make it possible to change the value of a property. Assignments on the property silently fail, the user does not encounter an error, unless the code is run in strict mode declaring the string `"use strict"`.

```
Object.defineProperty(
    objectLiteral,
    'nonWritable',
    {
        value: 'w',
        configurable: true,
        enumerable: true,
        writable: false
    }
);

> objectLiteral.nonWritable = 'X';
"X"

> objectLiteral.nonWritable;
"w"
```

This behavior is not convenient, because the assignment appears to have taken place until we query the value of the previously assigned property. Strict mode can be enabled in function scope, using an *immediately invoked function expression*:

```
(() => { 
    "use strict"; 
    objectLiteral.nonWritable = 'X'; 
})()
Uncaught TypeError: Cannot assign to read only property 'nonWritable' of object '#<Object>'
    at <anonymous>:3:31
    at <anonymous>:4:3
```

It is generally useful to use strict mode, because you tend to get more errors that can be corrected before your application is deployed on production.

### Freezing and sealing objects

Based on my experience as a tech interviewer, some developers think that the `const` keyword can create objects with a content that cannot be modified. This statement is false. The `const` keyword only ensures that the variable references an object, and this reference cannot be changed. The contents of the object can be modified at any time.

```
const account = {
    owner: 'Zsolt',
    amount: 1000
}

> account.amount = 500
500

> account
{owner: "Zsolt", amount: 500}
```

To create a real immutable constant, the object has to be *frozen*:

```
const account = {
    owner: 'Zsolt',
    amount: 1000
}

Object.freeze( account );

> account.amount = 500
500

> account.newProperty = true
true

> delete account.owner
false

> account
{owner: "Zsolt", amount: 1000}

> Object.defineProperty(
      account,
      'newProperty2',
      {
          value: 'w',
          configurable: true,
          enumerable: true,
          writable: false
      }
  );
Uncaught TypeError: Cannot define property newProperty2, object is not extensible
at Function.defineProperty (<anonymous>)
at <anonymous>:1:8
```

Summary: frozen objects are immutable. This means:

- the values of their properties cannot be changed,
- new properties cannot be added to it,
- existing properties cannot be deleted,
- the configuration of properties cannot be redefined.

Strict mode offers more errors, indicating errors when non-strict execution fails:

```
> (() => { 
      "use strict"; 
      account.amount = 500;
  })()
Uncaught TypeError: Cannot assign to read only property 'amount' of object '#<Object>'
    at <anonymous>:3:20
    at <anonymous>:4:3

> (() => { 
      "use strict"; 
      account.newProperty = true;
  })()
Uncaught TypeError: Cannot add property newProperty, object is not extensible
    at <anonymous>:3:27
    at <anonymous>:4:5

> (() => { 
      "use strict"; 
      delete account.owner;
  })()
Uncaught TypeError: Cannot delete property 'owner' of #<Object>
    at <anonymous>:3:7
    at <anonymous>:4:5
```

There are some use cases in JavaScript development, where we need to be able to change existing properties, without being able to add new properties to it, or remove existing properties. This is when `Object.seal` becomes useful.

```
const rootAccount = {
    owner: 'root',
    amount: Infinity
}

Object.seal( rootAccount );

> rootAccount.amount = 1000
1000

> rootAccount
{owner: "root", amount: 1000}

> Object.defineProperty( rootAccount, 'amount', {value: 500} )
{owner: "root", amount: 500}

> rootAccount
{owner: "root", amount: 500}

> (() => { 
      "use strict"; 
      delete rootAccount.owner;
  })()
Uncaught TypeError: Cannot delete property 'owner' of #<Object>
    at <anonymous>:3:7
    at <anonymous>:4:5

> (() => { 
      "use strict"; 
      rootAccount.newProperty = true;
  })()   
Uncaught TypeError: Cannot add property newProperty, object is not extensible
    at <anonymous>:3:31
    at <anonymous>:4:5 
```

Summary: sealed objects have properties that

- can be reassigned and reconfigured,
- cannot be deleted.

New properties cannot be added to a sealed objects.


### Getters and setters

`Object.defineProperty` can also be used to define getters and setters for a property. Let's define an area property such that it returns the square of the `sideLength` property value. When setting the area, the `sideLength` is automatically calculated as the square root of the area.

```
const square = {
    sideLength: 5
};

Object.defineProperty(
    square,
    'area',
    {
        get: function() { 
            return this.sideLength ** 2
        },
        set: function( value ) {
            this.sideLength = value ** 0.5;
        }
    }
);

> square.area
25

> square.area = 2
2

> square.sideLength
1.4142135623730951
```

There is an abbreviated format for defining getters and setters:

```
const rectangle = {
    a: 1,
    b: 1,
    get area() {
        return this.a * this.b;
    }, 
    set area( value ) {
        this.a = this.b = value ** 0.5;
    }
}

rectangle.area
1
rectangle.area = 2 
2
rectangle.area 
2.0000000000000004
rectangle.a 
1.4142135623730951
rectangle.b
1.4142135623730951
```

Let's investigate what happened here:
- when querying `rectangle.area`, we compute the product of `rectangle.a` and `rectangle.b`.
- when setting `rectangle.area` to `2`, the line `this.a = this.b = value ** 0.5;` computes the values of the sides, setting them to an approximate value of the square root of 2.
- when querying the new value of `rectangle.area`, we get the computed value of `1.4142135623730951 * 1.4142135623730951`, as the side values are both `1.4142135623730951`.

### Property Shorthand Notation

Let's declare a `logArea` method in our `shape` object:

```
let shapeName = 'Rectangle', a = 5, b = 3;

let shape = { 
    shapeName, 
    a, 
    b, 
    logArea() { console.log( 'Area: ' + (a*b) ); },
    id: 0 
};
```

Notice that in ES5, we would have to write `: function` between `logArea` and `()` to make the same declaration work. This syntax is called the *concise method syntax*. We first used the concise method syntax in [Chapter 4 - Classes](#ClassesConcise).

Concise methods have not made it to the specification just to shave off 10 to 11 characters from the code. Concise methods also make it possible to access prototypes more easily. This leads us to the next section.

### Computed Object Keys

In JavaScript, objects are associative arrays (hashmaps) with String keys. We will refine this statement later with ES6 Symbols, but so far, our knowledge is limited to string keys. 

It is now possible to create an object property inside the object literal using the bracket notation:

```
let arr = [1,2,3,4,5];

let experimentObject = {
    arr,
    [ arr ]: 1,
    [ arr.length ]: 2,
    [ {} ]: 3
}
```

The object will be evaluated as follows:

```
{
    "1,2,3,4,5": 1,
    "5": 2,
    "[object Object]": 3,
    "arr": [1,2,3,4,5]
}
```

We can use any of the above keys to retrieve the above values from `experimentObject`:

```
experimentObject.arr                  // [1,2,3,4,5]
experimentObject[ 'arr' ]             // [1,2,3,4,5]
experimentObject[ arr ]               // 1
experimentObject[ arr.length ]        // 2
experimentObject[ '[object Object]' ] // 3
experimentObject[ experimentObject ]  // 3
```

Conclusions:

- arrays and objects are converted to their `toString` values
- `arr.toString()` equals the concatenation of the `toString` value of each of its elements, joined by commas
- the `toString` value of an object is `[object Object]` regardless of its contents
- when creating or accessing a property of an object, the respective `toString` values are compared

### Equality

We will start with a nitpicky subject: comparisons. Most developers prefer `===` to `==`, as the first one considers the type of its operands.

In ES6, `Object.is( a, b )` provides *same value equality*, which is almost the same as `===` except the following differences:

- `Object.is( +0, -0 )` is `false`, while `-0 === +0` is `true`
- `Object.is( NaN, NaN )` is `true`, while `NaN === NaN` is false

I will continue using `===` for now, and pay attention to `NaN` values, as they should normally be caught and handled prior to a comparison using the more semantic `isNaN` built-in function. For more details on `Object.is`, visit [this thorough article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness).

### Mixins and Shallow Copies with Object.assign

Heated debates of composition over inheritance made mixins appear as the winner construction for composing objects. Therefore, libraries such as UnderscoreJs and LoDash created support for this construct with their methods `_.extend` or `_.mixin`. 

In ES6, `Object.assign` does the exact same thing as `_.extend` or `_.mixin`.

Why are mixins important? Because the alternative of establishing a class hierarchy using inheritance is inefficient and rigid. 

Suppose you have a view object, which can be defined with or without the following extensions:

- validation
- tooltips
- abstractions for two-way data binding
- toolbar
- preloader animation

Assuming the order of the extensions does not matter, 32 different view types can be defined using the above five enhancements. In order to fight the combinatoric explosion, we just take these extensions as mixins, and extend our object prototypes with the extensions that we need.

For instance, a validating view with a preloader animation can be defined in the following way:

```
let View = { ... };
let ValidationMixin = { ... };
let PreloaderAnimationMixin = { ... };

let ValidatingMixinWithPreloader = Object.assign( 
    {}, 
    View, 
    ValidationMixin, 
    PreloaderAnimationMixin
);
```

> Why do we extend the empty object? Because `Object.assign` works in a way that it extends its first argument with the remaining list of arguments. This implies that the first argument of `Object.assign` may get new keys, or its values will be overwritten by a value originating from a mixed in object.

The syntax of calling `Object.assign` is as follows:

> `Object.assign( targetObject, ...sourceObjects )`

The return value of `Object.assign` is `targetObject`. The side-effect of calling `Object.assign` is that `targetObject` is mutated.

> `Object.assign` makes a *shallow copy* of the properties and operations of `...sourceObjects` into `targetObject`.

For more information on *shallow copies* or cloning, check my article on [Cloning Objects in JavaScript](http://www.zsoltnagy.eu/cloning-objects-in-javascript/).

```
let horse = { 
        horseName: 'QuickBucks', 
        toString: function() { 
            return this.horseName; 
        } 
};

let rider = { 
        riderName: 'Frank', 
        toString: function() { 
            return this.riderName; 
        } 
};

let horseRiderStringUtility = { 
    toString: function() { 
        return this.riderName + ' on ' + this.horseName; 
    } 
}

let racer = Object.assign( 
        {}, 
        horse, 
        rider, 
        horseRiderStringUtility 
    );

console.log( racer.toString() );
> "Frank on QuickBucks"
```

Had we omitted the `{}` from the assembly of the `racer` object, seemingly, nothing would have changed, as `racer.toString()` would still have been `"Frank on QuickBucks"`. However, notice that `horse` would have been `===` equivalent to `racer`, meaning, that the side-effect of executing `Object.assign` would have been the mutation of the `horse` object.


### Destructuring objects

In the scope where an object is created, it is possible to use other variables for initialization.

```
let shapeName = 'Rectangle', a = 5, b = 3;

let shape = { shapeName, a, b, id: 0 };

console.log( shape );
// { a: 5, b: 3, id: 0, shapeName: "Rectangle" }
```

It is possible to use this shorthand in destructuring assignments for the purpose of creating new fields:

```
let { x, y } = { x: 3, y: 4, z: 2 };

console.log( y, typeof y );
// 4 "number"
```

### Spreading objects

The spread operator and rest parameters have been a popular addition in ES2015. You could spread arrays to comma separated values, and you could also add a rest parameter at the end of function argument lists to deal with a variable number of arguments.

Let’s see the same concept applied for objects:


```
let book = {
    author: 'Zsolt Nagy',
    title: 'The Developer\'s Edge',
    website: 'devcareermastery.com',
    chapters: 8
}
```
 
We can now create an destructuring expression, where we match a couple of properties, and we gather the rest of the properties in the bookData object reference.


```
let { chapters, website, ...bookData } = book 
```
 
Once we create this assignment, the chapters numeric field is moved into the chapters variable, website will hold the string 'devcareermastery.com'. The rest of the fields are moved into the bookData object:


```
> bookData
{author: "Zsolt Nagy", title: "The Developer's Edge"}
```

This is why the ...bookData is called the rest property. It collects the fields not matched before.

The rest property for objects works in the same way as the rest parameter for arrays. Destructuring works in the exact same way as with arrays too.

Similarly to rest parameters, we can use rest properties to make a shallow copy of an object. For reference, check out my article cloning objects in JavaScript


```
let clonedBook = { ...book };
```
 
You can also add more fields to an object on top of cloning the existing fields.

```
let extendedBook = {
    pages: 250,
    ...clonedBook
}
```

The spread syntax can be expressed using `Object.assign`:

```
let book = {
    author: 'Zsolt Nagy',
    title: 'The Developer\'s Edge',
    website: 'devcareermastery.com',
    chapters: 8
}

// let clonedBook = { ...book };
let clonedBook = Object.assign( {}, book );

// let extendedBook = {
//    pages: 250,
//    ...clonedBook
// }
let extendedBook = Object.assign( {pages: 250}, clonedBook );
```

### Symbol keys

In ES6, the `Symbol` type was introduced. Each symbol is unique. Even if two symbols are associated with the same label, they are different:

```
> Symbol( 'label' ) == Symbol( 'label' )
false
```

JavaScript allows both strings and symbols as object keys. This makes it possible to define your own identifiers that are unique, without the need to worry about whether there is another resource using the same identifier. For instance, if we create a global `Symbol( 'jQuery' )`, and there is another global `Symbol( 'jQuery' )` coming from another file, the two values can co-exist, and they will not be equal.

In reality, the above benefit does not result in well maintainable code, but at least it is one way to resolve conflicts.

Without placing judgement on what counts as maintainable or unmaintainable, JavaScript allows you to use Symbol keys:

```
const key = Symbol( 'key' );

const o = {
    [key]: true,
    [Symbol( 'key2' )]: true
}
```

Be aware of the following featues of `Symbol` keys:

`1`. their value does not appear in the `JSON` form of an object:

```
> JSON.stringify(o)
"{}"
```

`2`. their value does not appear in `for..in`, `Object.keys`, `Object.entries`, `Object.getOwnPropertyNames` enumerations:

```
> for ( let p in o ) console.log( p )
undefined

> Object.keys( o )
[]

> Object.entries( o )
[]

> Object.getOwnPropertyNames( o )
[]
```

`3`. their value does appear in `Object.getOwnPropertyDescriptors`:

```
> Object.getOwnPropertyDescriptors( o ) 

```

As a consequence, `Symbol` keys are not a bulletproof way for indicating private properties.

`4`. their value does appear in shallow copies:

```
> {...o}
{Symbol(key): true, Symbol(key2): true}

> Object.assign( {}, o )
{Symbol(key): true, Symbol(key2): true}
```
