# Objects

### What is the point of an object?

Its a data structure- a container for holding stuff (in the form of key/value pairs)

## Property Access
How to get at stuff in an object


___
## Bracket Notation
It's one way of accessing properties 


___
## Dot Notation
This is the other way to access properties.  


```js
var box = {};

box.material = "cardboard";
```
I just added a new property to an empty object and gave it a value. 



Where do we see dots in JS?
chaining function calls, jQuery, 

___
## Dots vs. Brackets
Brackets are much more powerful. You can really only use dot notation for strings. You can use brackets for pretty much anything.  

Don't use dot notation with a variable ??
Don't put quotation marks around variable name




___
## Nested Objects 
Objects that have objects in their objects


___
## Object Literals
It's literally an object


___
## Iteration
A fancy way of saying 'looping'...
Accessing a bunch of properties over and over really fast


___
## Storing Data


```js
var box = {};
box['material'] = "cardboard";

box['size'] = {
  'height' : 2,
  'width' : 80
};

box.area = function(){
  return box.size * box.size 
}
```

