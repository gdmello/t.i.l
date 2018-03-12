Prototype
---------
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
`Object.call` function enables a prototype constructor call from anywhere in the source and invokes the prototype within the current context.

Copy Object properties
----------------------
To copy all properties from *object1* to *object2* use [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) - 
`Object.assign(object1, object2)`
