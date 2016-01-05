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

