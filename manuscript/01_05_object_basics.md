## The Object type

This section will introduce the Object type. We will only learn the basics here.

An object is data structure with String or Symbol keys and arbitrary values. Imagine it like a machine that accepts a key, and gives you a value. Some people call this data structure *associative array*, others call it *hashmap*. These names may sound fancy, but essentially we mean the same damn thing.

*Side note: we will only deal with `String` keys for now. `Symbol` keys are also allowed for strings. This is an advanced topic, you will learn it later.*

```
let author = {
  name: null,
  website: "zsoltnagy.eu",
  age: 35
}

author.name = "Zsolt";
console.log( author.name, author[ "website" ] )
// Prints: Zsolt zsoltnagy.eu

delete author.name
console.log( "Author name: ", author.name )
// Prints: Author name: undefined
```

An object contains *fields*. A *field* in an object can be referenced in the following ways:

- dot notation: `object_name.member_name`
- bracket (associative array) notation: `object_name[ string_or_symbol_value ]`

The `delete` operator deletes a field from an object. 

If a field in an object is deleted or not even declared, the value of this field is `undefined`.

```
let o = {};

> o.name 
undefined
```

We will learn a lot more about objects later.
