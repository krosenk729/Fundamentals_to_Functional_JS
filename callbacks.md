# Higher-Order Functions

1. Takes a function as an input
2. returns a function as the output

___

### Takes a function as an input

```js
element.addEventListener( "click", function(){
  console.log("element clicked!");
  });
```
addEventListener() takes an anonymous function that logs "element clicked!" to the console.

### Returns a function as the output

```js
var add = function(num) {
  var num1 = num;

  return addToNum1 = function (num2){
    return num1 + num2;
  };
};
```
`add` returns `addToNum1();`

___

# Callbacks
Functional Programming is about Using functions as units of abstraction instead of abstracting over data. A simple example is abstracting an if/else statement into a function. 

Here is an example of an if/else statement abstracted into a function. 

```js
var ifElse = function( condition, isTrue, isFalse){

  if(condition){
    isTrue;
  } else {
    isFalse;
  }
};

ifElse( true, 
  function(){ console.log( true); },

  function(){ console.log( false); }

  );
```

To call ifElse(), you would need to pass in three arguments. First a Boolean, and then two functions If the conditional is true, you get the first function, and if it's false, you get the second. 




## Passing Arguments
functions passed as arguments can be invoked using their parameter name. These function can also have their own set of arguments passed to them when they are invoked.

```js
var increment = function(n){ return n + 1; };
var square = function (n){ return n*n; };

var doMathSoIDontHaveTo = function(n, func){ return func(n); };

doMathSoIDontHaveTo( 5, square);

doMathSoIDontHaveTo( 4, increment);
```


___


```js
var funCaller = function(func, arg) {
    return func(arg);
};
```



```js
var firstVal = function(arr, func) {
    func(arr[0], 0, arr);
};
```

change firstVal to work not only with arrays, but also objects. Since objects are not ordered, you can use any key-value pair on the subject


```js
firstVal = function(list, func){
  if( Array.isArray( list )){
    func( arr[ 0], 0, arr );
  } else {
    for(var k in list){
      return func( list[k], k, list);
    }
  }
}
```
Using `Object.keys`: This returns an array of all keys in an object. 

```js
firstVal = function(list, func){
  if( Array.isArray( list )){
    func( arr[ 0], 0, arr );
  } else {
    var propArr = Object.keys( list );
    func( list [ propArr[0] ], propArr[0], list )
```

