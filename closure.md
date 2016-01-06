# Closure
A closure occurs when you return a function from inside a function, and the inner function retains access to the outer scope.

```js
var closureAlert = function(){
  var x = "Help! I'm a variable stuck in a closure!";
  
  var alerter = function(){
    alert(x);
  };

  setTimeout(alerter, 1000);

  console.log('will still run right after');

};

```

* Variable `closureAlert` is defined a function
  - the body of the function is not compiled until called. 
* Call `closureAlert()`
  - now the body is compiled
* Variable `x` is declared 
  - the string "Help! I'm a variable stuck in a closure!" is assigned to `x`
* Variable `alerter` is defined a function
  - skip the body until it is called in the next line
* `setTimeout()` is called, passing in `alerter` and 1000 (ms/1sec)
* log the string 'will still run right after' to the console.
* `setTimeout()` is asyncronous. It doesn't pause. 
  - you see the console.log first
* After 1 second, `alerter()` is called. 
  - The body of `alerter()` is compiled
  - calls `alert()` passing in `x`
  - the alert will delay 1 second rather than immediately
  - the alert alerts with `x`
    + "Help! I'm a variable stuck in a closure!"


___

```js
var closureAlert = function(){
  var x = 0;
  var alerter = function (){
    alert(++x);
  };
  return alerter;
};

var funcStorer = closureAlert();
var funcStorer2 = closureAlert();

funcStorer();
    // alerts 1  on first call, 2 on second, and so on
    // each time, `alerter()` remembers the scope, and value of `x`
funcStorer2();
      // new scope
      // alerts 1  on first call, 2 on second, and so on

```
`funcStorer` holds reference to `alerter()`

```js
var alerter = function(){
  alert(++x);
}
```
* `++x` adds 1 to `x` and returns it -- as opposed to `x++`, which returns x, and THEN increments it. (which is why it doesn't just stay zero)

* Is returning alerter the same as invoking alerter?
  - absolutely not. 
  - returning it without invoking it just returns the definition.
  - if you invoke it in the return statement, you couldn't call it with the `funcStorer()`

`closureAlerter();` returns the definition of the alerter function:

```js
  var alerter = function (){
    alert(++x);
  };
```
* We want `funcStorer()` to be a function, and not the result. This gives us a window into the parent scope that we can access later. 


___
## Recipe for Closure

```js
function checkscope(){
  var innerVar = 'localscope';

  function innerFunc(){
    return innerVar;
  }

  return innerFunc;
}
```

1. Create your parent function
2. Define some variables in the parent's local scope
3. Define a function inside the parent function (child function)
4. Return that function from inside the parent



## ah-HA! !!!
Closure isn't just about inner scopes retaining value of parent scope variables...

```js
function checkscope(){
  var innerVar = 'localscope';
  function innerFunc(){
    return innerVar;
  }
  return innerFunc;
}
```

All `checkscope()` does is return `innerFunc()` WITHOUT PARENTHESIS. It returns the function. IT DOESN'T INVOKE IT.  

call `checkscope()` and all it returns is the child function. Even with parenthesis. It's as if you left the parenthesis off of a function expression, only returning the definition. That is what `checkscope()` does. It returns the function, not the value. 

```js
//returns
  function innerFunc(){
    return innerVar;
  }
```

To call `innerFunc()`, `checkscope()` must be assigned to a variable. it has to be assigned to a variable, and then called with parenthesis. 

```js
var har = checkscope();
```

Now that it is assigned to `har`...

call `har;` and you only get the reference, but call har with parenthesis, and you call `innerFunc()`

```js
har();
```
*returns* -->
>>>"localscope"

Once more...

```js
var scope = "global scope";
function checkscope(){
  var scope = "localscope";
  function innerFunc(){
    return scope;
  }
  return innerFunc;
}
```

### Setup
1. Create your parent function
2. Define some variables in the parent's local scope
3. Define a function inside the parent function (child function)
4. Return that function from inside the parent

```js
var test = checkscope();
```
let's see what `test` holds:

```js
test; 
```

*returns* -->
>>>function innerFunc(){
  return scope;
}

Looks good. To call it, just use the invocation operator `()`

```js
test();
```

*returns* -->
>>>"localscope"

### Execution
1. run parent function and save to variable. This variable will hold whatever that function RETURNS.
2. *optional: check what that variable holds as a value. (It should be the inner function)*
3. run the inner function 


___

# More CLOSURE(s) and CLOSURE notes

```js
var sayAlice = function(){

  var makeLog = function(){
    console.log(alice);
  };

  var alice = 'Why hello there, Alice!';
  return makeLog;
};

var what = sayAlice();
```
### The browser is all like
* Define a function called `sayAlice`
  - Skip function body

* Declare variable `what` 
* assign it `sayAlice()`
  - now go inside function body
* Declare variable `makeLog`
  - recognize that it's a function
  - skip the body
* Declare variable `alice`
  - assign it the string "Why hello there, Alice!"
* return `makeLog`
  - go inside function body
  - log the variable `alice`, which we just defined. 
  - Print string to the console


```js
what();
```

*returns* -->
>>>"Why hello there, Alice!"

___

```js
var makeStopwatch = function(){

  console.log('initialized');
  var elapsed = 0;
  console.log(elapsed);

  var stopwatch = function(){
    console.log('stopwatch');
    return elapsed;
  };

  var increase = function(){
    elapsed++;
  }

  setInterval(increase, 1000);

  return stopwatch;
};

var x = makeStopwatch();
x();
```

___

## Add to Number

```js
var add = function( num ){
  var num1 = num;
  var addToNum1 = function( num2 ){
    return num1 + num2;
  };
  return adToNum1;
};


var add5 = add(5);

```

`add` returns the entire function. 
`add()` returns the inner function `addToNum1()`  

To make use of this, it needs a variable to act as a handler.  
I think this variable that refers to our inner/outer function is what is specifically called the 'closure'.  

```js
var add5 = add(5);
```
`add5` is our closure. Here, it's invoked, passing 5 as `num1`.  
Now it's a function that can actually do something. Whatever is passed into `add5()` will be `num2`.

```js
add5(4);
```

*returns* -->
>>> 9

```js
add5(20);
```

*returns* -->
>>> 25

## NOTE
The only thing `add()` is capable of is returning `addToNum1()`.  Passing numbers into it returns the exact same result. 

```js
add(9);
```

*returns* -->
>>> function addToNum1(num2){
>>>   
>>> }

It also doesn't seem to make a difference if you use function declarations. This might have some different effects with regards to hoisting. 

```js
function add (num) {
  var num1 = num;
  function addToNum1 (num2) {
    return num1 + num2;
  }
  return addToNum1;
}
```
Works exactly the same as above. But it needs the closure. On it's own it is pretty useless. 

```js
var add5 = add(5);
```
We've got a function called `add5()` now. 5 is sewn up inside as it's `num1`
Now we've got ourselves a sweet little closure that adds 5 to stuff. Super useful. Add 5 to everything.

### The only purpose of the outer function is to return the inner function.

It's job is to pass the inner function (which retains access to previous enviornment/scope.  

___

# CLOSURE EXERCISES

```js
function nonsense(string){
    var blab = function(){
        alert(string)
    }
    blab();
}
```

Alerts, but `string` is undefined.

```js
function nonsense(string){
    var blab = function(){
        alert(string);
    };
        setTimeout(blab, 2000);
}
```

Waits two seconds before alerting, but string is still undefined.

```js
function nonsense(string){
    var blab = function(){
        alert(string)
    }
    return blab;
}
```

`nonsense()` calls `blab()`

```js
var blabLater = nonsense("trigitty-troggity! Up on the fence sayin nonsense!");
var blabAgainLater = blabLater("picture me! JUS' chewin on some bubbleYum!");
```


```js
blabLater();
```

*returns* -->
>>>trigitty-troggity! Up on the fence sayin nonsense!

```js
blabAgainLater();
```

*returns* -->
>>>Uncaught TypeError: blabAgainLater is not a function

___
## travis's custom closure
Write a function with a closure. The first function should only take one argument, someone's first name, and the inner function should take one more argument, someone's last name. The inner function should console.log both the first name and the last name.

```js
function outerScope(firstName){
  function innerScope(lastName){
    console.log(firstName + " " + lastName);
  }
  return innerScope;
}
```

`outerScope()` calls `innerScope()` and that is all it can do. 

```js
var nameThing = outerScope("Travis");
```

*returns* -->
>>>Travis Undefined

```js
nameThing("Gorman");
```

*returns* -->
>>>Travis Gorman


```js
nameThing('Finnigan');
```

*returns* -->
>>>Travis Finnigan

___

# example story function 


```js
function storyWriter(){
    var story = "";
    return {
         addWords : function addWords(word){ story += word; return story; },
         erase : function(){ story = ""; } 
           }
}
```

```js
var farmLoveStory = storyWriter();
farmLoveStory.addWords("there once was a lonely cow. ");
farmLoveStory.addWords("It saw a friendly face.");

var storyOfMyLife = storyWriter();
storyOfMyLife.addWords('my code broke. ');
storyOfMyLife.addWords('I ate some ice cream. ');
```

*returns* -->
>>>'my code broke. I ate some ice cream.'


```js
storyOfMyLife.erase();
```

*returns* -->
>>>undefined


```js
farmLoveStory();
```

*returns* -->
>>>Uncaught TypeError: farmLoveStory is not a function(…)



* the closure holds the function that returns an object.  
* The closure can then call on methods on that object. 

## Using the module pattern, DESIGN A TOASTER.  

Use your creativity here and think about what you want your users to be able to access on the outside of your toaster vs what you don't want them to be able to touch.


```js
var Toaster = function (){
    // some private methods and properties
        return {
            // some public methods and properties, etc
        }
}
```


#### Extra Credit
## Use the module pattern to DESIGN A CHARACTER in a Super Mario game. 

Think about what actions you can control in the game and other aspects you can't control directly (example: you can only affect your health indirectly by eating a mushroom). If you are not familiar with Super Mario, choose another simple game for this example.



___

# Extra Credit
Why doesn't the code below work? This is a function that should return an array of functions that console.log() each person's name as a string when invoked. Fiddle with this function and inspect how it works, then try to fix it using a closure. Be prepared to explain to a partner how it worked before, and how it works now with a closure.

```js
var checkAttendanceFunc = function(nameArr){
    var resultArr = [];
    for(var i = 0; i < nameArr.length; i++){
        resultArr.push(function(){ console.log('Is', nameArr[i], 'present?', i)})
    };
    return resultArr;
};
```




___
# Extra Credit
Write a function that takes another function* as an argument and creates a version of the function that can only be called one time. 

Repeated calls to the modified function will have no effect, returning the value from the original call. How could you do this without using a closure? Is it even possible? How could you do this with a closure? *Note: This original input function should not have any parameters.



___

