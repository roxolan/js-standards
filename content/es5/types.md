---
title: ES5 Built In Types
linktitle: Types
date: 2015-01-14T22:52:22+11:00
tags:
  - ES5
  - Types
  - Arrays
  - Objects
  - Booleans
  - Strings
  - Prototype
menu:
  main:
    parent: js
prev: /es5/equality
next: /es5/lint
notoc: true
weight: 2080
---

### Arrays

- Use `[val, val2]` syntax instead of `new Array(len)`, because preallocating memory for an array is not guaranteed, and the former is less verbose

### Objects

- Use `{ key: 'val', key2: 'val2' }` instead of `new Object()`, as it is less verbose
- Do not quote keys of object literals, unless they must contain non-alphabet characters
- Try to use keys in objects which conform to variable naming conventions
- When iterating over all properties in an object,
  and accessing keys from the object's prototype is undesirable,
  be sure to use the `hasOwnProperty` check

Without `hasOwnProperty` check:

```javascript
for (key in myObject) {
  var value = myObject[key];
  //do stuff with key and value
}
```

With the `hasOwnProperty` check:

```javascript
for (key in myObject) {
  if (myObject.hasOwnProperty(key)) {
    var value = myObject[key];
    //do stuff with key and value
  }
}
```

Use the former variation, without the `hasOwnProperty` check,
only when you are absolutely certain that there cannot be any properties
present on the object that come from its prototype.

A better way than rolling your own would be to use functions in libraries such as
UnderscoreJs or LoDash.
If you are using ES6 Javascript, you have even more powerful
[object iteration means](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/for...of)
at your disposal.

### Booleans

- Do not compare to `true` or `false`, simply use the value of the value directly:
  Either `if (myBool) { /*...*/ }`, or `if (!myBool) { /*...*/ }`
- Be aware of the difference between `true` and *truthy*.
  [Reference](http://james.padolsey.com/javascript/truthy-falsey/)

### Strings

- Use `'` to quote string literals, as a preference over `"`
- Use `"` to quote strings literals which would otherwise contain many escapes single quote marks (`\'`)

### Modifying the prototypes of built in types

- Don't!
- It may be convenient to add your own custom implementation of `Array.prototype.forEach`,
  and the like, but generally speaking,
  unless you are developing a low level library, this is a bad idea
