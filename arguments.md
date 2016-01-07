## Arguments/ Parameters

```js
var nameImprover = function (name, adj) {
  return 'Col ' + name + ' Mc' + adj + ' pants';
};

nameImprover( 'Tanner', 'Buff' );

$('body').hide();

var myArr = ['this', 'that', 'and', 'the', 'other'];
myArr.forEach( val => console.log( val) );

$('button').on('click', function(){
  console.log('Don\'t press my buttons!');
  });

```
## Return / Side Effects
* the *return* keyword immediately breaks out of a function and returns.
* Without an explicit 'return' statement, return is 'undefined'
* Any other work done is considered a side effect

```js
var add = function(a, b){
  return a+b;
}

add(3,4,5);
add(4,10,3);

function addSecondTwo(a, b, c){
  return b + c;
}

addSecondTwo(4,10,3);

```

## Arguments Keyword

```js
var add = function(a, b){
  console.log(arguments);
  return a + b;
};

var add = function( a, b){
  return ( arguments.length > 2) ? 
    ( a + b + arguments[2] ) : (a + b);
};

add(3,10,5);
```
* `arguments` is an array-like object, not an array.  
* You cannot use array methods on it.  

___
## Constructors
A function that returns an object

```js
function AnimalMaker(name){
  return {
    speak: function(){
      console.log("My name is", name);
    }};
}

var myAnimal = AnimalMaker('the skoog');

myAnimal.speak();
```
> "My name is the skoog"

```js
myAnimal ['speak'] ();
```
