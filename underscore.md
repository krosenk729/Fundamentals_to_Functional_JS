# UNDERSCORE

## _.each()
Just like `forEach()`, it iterates an array calling a function on each item. It takes a callback function that may consist of the parameters 
value, index, and array (always in that order). 

`callback( val, i, arr )`
You can call them whatever you want as long as they match in the function body. 
If you're chaining it to an array, then you'll normally just use the `val` parameter.  

The native JS `forEach()`


```js
var pocketmon = ['Charisaur', 'Bulbazard', 'Twomew'];
var logger = function(val) {
    console.log(val);
};

_.each(pocketmon, logger);
```
___

## Looping with `_.each()`

```js
function AnimalMaker (name) {
  return {
    speak : function () { 
      console.log("my name is ", name);
    }
  };
};
var animalNames = ['',,'',''];
var farm = [];

_.each(animalNames, function(name) {
  farm.push(AnimalMaker(name));
});
```

When using Underscore’s `each()` method, you aren’t able to return a value in the supplied function. The map() method not only loops through an array, but returns a new array of values as the result.

```js
var pocketmon = ['Charisaur', 'Bulbazard', 'Twomew'];
var excitedArr = function(val){
  return val + '!!!';
};

_.map(pocketmon, excitedArr);
```

___

## `_.map()` Defined
* Produces a new array of values by mapping each value in `list` through a transformation function (iterator)
* Each invocation of iterator is called with three arguments:(element, index, list).  
* If list is a JavaScript object, iterator's arguments will be (value, key, list)

```js
_.map([1,2,3], function(v, i, list){console.log(v)} )
```

## _.map() usage

```js
var pocketmon = ['Charisaur', 'Bulbazard', 'Twomew'];
var excitedArr = function(val){
  return val + '!!!';
};

var excitedPocketmon = _.map(pocketmon, excitedArr);
```

## Looping with `_.map()`

The Difference Between each and map

You cannot return anything from `each`
___
