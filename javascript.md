Basics
======

Scope
-----
Global or function scope.
Global scope is top level above all functions.

Objects
=======

Initilaization
--------------
Objects can be initialized with the *Object initializer* or *literal*, as below-
```javascript
var myObj = {};
var tom = {
   name: 'Thomas',
   age: 40
};
```
or with a *constructor function*-
```javascript
function Person(name, age) {
   this.name = name,
   this.age = age
};

var jack = new Person('jack', 23);
```
or with `Object.create()`-
```javascript
var Car = {
   type: 'sedan'
   mode: 'sports'
};

mustang = Object.create(Car)
mustang.type = 'convertible'

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

Getters And Setters
-------------------
[Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)

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

var person1 = new Person('Jane', 30)

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
Funtions can be defined in three ways-
* `Function declaration` statement
```javascript
function add(num1, num2) {
   return num1 + num2;
}
```
* *Function expressions*
```javascript
let func = function(num1, num2) {
   return num1 + num2;
}
```
* *Arrow function*
```javascript
let func = (num1, num2) => {
   return num1 + num2;
}

let newfunc = () => {
   alert('hi!');
}
```

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
Asynchronous Functions
----------------------
* [callbacks](https://javascript.info/callbacks) - *Medieval times*
* [Promise](https://javascript.info/promise-basics), and [Promise chaining](https://javascript.info/promise-basics)
* [Async/ await](https://javascript.info/async-await)

Arrow Functions
---------------


Classes
=======
* Not hoisted like functions
```javascript
var c = new Car(); //Error

class Car{}
```
* Can we declared with the class keyword or via an expression
```javascript
class Mercedes {
   constructor(name, model) {
    ...
   }
};
``` or
``` javascript
mercedes = var class Mercedes{
...
}; //named

mercedes = var class {
...
}; // unnamed
```
[Ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

Subclassing
-----------
* Possible with the `extends` keyword.
* Works on both classes defined with the `class` keyword or via an expression.
* `species` property enables subclass to override the default constructor of an object.
* ECMAScript classes can only inherit from a single class.

Modules
=======

Export/ Import
--------------
A class can be one of the objects exported by a module. Here is a way to import the Class properties directly -
```javascript
// a.js
class A {
...
}
A.new_prop1 = "some_prop1";
A.new_prop2 = "some_prop2";

//b.js
const {new_prop1, new_prop2 } = require('a.js');

```

Tips & Tricks
=============

* [Method Definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions) Short hand for assigning functions to object attributes.
* `[species](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/species)` property enables subclass to override the default constructor of an object.
* `[Strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)`

Reference
=========
* [Standard Built-in objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)
