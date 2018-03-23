Basics
======

Scope
-----
Global or function scope.
Global scope is top level above all functions.

Objects
=======

Declaration
-----------
```javascript
var myObj = {};
```

Accessing Properties
--------------------
```javascript
var person = {
   name: 'ham',
   age: 29
};

person.name;   // Dot notation
person['name'] // Bracket notation
```

`this` keyword
--------------
Represents the current object
```javascript
var person = {
   firstName: 'jack',
   lastName: 'jones',
   fullName: function() {
         return this.firstName + this.lastName;
   }
};
```

Copy Object properties
----------------------
To copy all properties from *object1* to *object2* use [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) - 
`Object.assign(object1, object2)`

Prototypes
==========

Types
-----
Class-based languages are founded on two entities - *Classes* and *instances* of those classes.
Prototype languages are founded on one entity - objects, such a lamguage has the notion of a *Prototype* object which serves as a template for all other objects. Properties and methods can be added to these objects. [Ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Details_of_the_Object_Model)

Basics
------
All Javascript objects inherit from a prototype object. Array from `Array.prototype`, string from `string.prototype`.

To add a new property to all instances of an object, modify the objects prototype as-
```javascript
function Person(name, age) { // object constructor
   this.name = name
   this.age = age
}

prototype.person.gender = "M/F"

prototype.person.adult = function() { if (age > 21) {return true}}
```
[Ref](https://www.w3schools.com/js/js_object_constructors.asp)

Prototype Inheritance
---------------------
Extend the *Person* object type above, use [object.call](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)-
```javascript
function Teacher(name, age, school) {
   Person.call(name, age)
   this.school = school
}
```
`Object.call` function enables a prototype constructor call from anywhere in the source and invokes the prototype within the current context. See furthe details in the reference link.

Hoisting
--------
[Reference](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)

Functions
=========

Functions vs Methods
--------------------
Methods are functions defined as an attribute of an object. [Ref](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions)

Anonymous Functions
-------------------
```javascript
button.onClick = function() {
  console.log('Hi');
}
```
