# Fundamentals_to_Functional_JS
"JavaScript: From Fundamentals to Functional JS" taught by Bianca Gandolfo at Frontend Masters - 

* [Callbacks](https://github.com/travisgorman/Fundamentals_to_Functional_JS/blob/master/callbacks.md)
* [Closure](https://github.com/travisgorman/Fundamentals_to_Functional_JS/blob/master/closure.md)
* [Functions](https://github.com/travisgorman/Fundamentals_to_Functional_JS/blob/master/functions.md)
* [Nesting](https://github.com/travisgorman/Fundamentals_to_Functional_JS/blob/master/nesting.md)
* [Scope](https://github.com/travisgorman/Fundamentals_to_Functional_JS/blob/master/scope.md)
* [Underscore](https://github.com/travisgorman/Fundamentals_to_Functional_JS/blob/master/underscore.md)

# Front-End Masters Workshop Series
## JavaScript: Fundamentals to Functional JavaScript


Objects {}:
- a data structure in which we store data
- store properties, functions, sting, Array, Numbers
- key/value pairs
- blueprint of a class (something that has properties)

Objects Overview:
- property access
- bracket notation
- dot notation
- dot notation vs bracket
- nested objects
- object literals
- iteration

Whatever is to the left of a dot is an object (syntax rules of dot notation or bracket notation apply)

```js
// store an empty object in literal form
var box = {};

// assignments with dot notation
box.material = "cardboard";

// access with dot notation
box.material;

// store by value
var cb = box.material;
cb;
box.material = "titanium";
cb;
```

## Objects, Arrays, and Functions are stored by reference.

### Access & Assignment
- Dot notation and bracket notation can be used to ASSIGN values to objects and arrays
- Dot notation and bracket notation can be used to ACCESS values stored in objects and arrays
-
- `undefined` is its own type
- occurs if you do a property look up on something that does not exist on the object

### Bracket Notation

```js
var box = {};
box["material"] = "cardboard";
var cb = box["material"];
```

### Variables
Difference between new `Object();` and `{};` is a constructor and object literal notation.  
`Object( );` this is a constructor
`{ };` this is an object literal

```js
var box = {};
box ["material"] = "cardboard";
var key = "material";
box [key];
```

### Expressions
Bracket notation evaluates expressions

```js
var b = {};
b["material"] = "cardboard";
var f = function() {
  return "material";
};

b[f()];
```

### Dot notation 
is limited and not as flexible as bracket notation when using it for property names.

### Brackets
- strings
- weird characters
- variables
- numbers
- expressions

### Storing data using Objects, etc.

```js
var a = {};
a["material"] = "cardboard";
a["size"] = {
  "height": 2,
  "width": 80
};

a.area = function() {
  return a.size.height * a.size.height;
};
```

### Iteration
No guaranteed order of objects

```js
var browsers = {
IE: 'Internet Explorer',
Mozilla: 'Firefox',
Google: 'Chrome',
0: 'No browser found.'
};

for (var type in browsers) {
  console.log(browsers[type]);
}
```

## Solve Exercises

Arrays vs. Objects
- data structure used for ordering items
- zero indexed
- Objects that have string properties don't have inherent order
- Array is an Object and thus share the same rules
- how are they different?

Overview
- Arrays vs Objects
- Access && Assignment
- Native Methods && Properties
- Iteration

Use Arrays if it doesn't make sense to have named properties or if you need elements to be ordered.

Iterations

```javascript
var e = [];
e['new'] = 'element';
e['0'] = 'value';
for (var i in e) {
  console.log(e[i])
}
```

```javascript
var iterateObject = {};

iterateObject['one'] = 1;
iterateObject['two'] = 2;
iterateObject['three'] = 3;
iterateObject['four'] = 4;
iterateObject['five'] = 5;

for (var index = 0; index > iterateObject.length; index++) {
  console.log("Iterated Object: " + index);
}
```

Functions
- 'arguments' keyword
- lives inside functions
- gets the values of the arguments in the form of Array Object

Looping
Functions as Constructors


```javascript
// function that returns an Object
function AnimalMaker(name) {
  return {
    speak: function() {
      console.log("my name is ", name)
    }
  };
};

var animalNames = ['Sheep','Liger','Big Bird'];

```
