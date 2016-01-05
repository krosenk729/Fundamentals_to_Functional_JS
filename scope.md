## Scope
defines where variables live, and can be accessed

Scope is where our variables have meaning. Scope is created dynamically when we call our function. When a variable is declared inside a function, it is only accessible from inside that function because it has local scope. On the other hand, a variable has global scope when it’s declared outside of any functions. Global variables can be accessed from anywhere.



#### Function Declaration / Expression
If the first word is *'function'*, its a **declaration**.  
If it's assigned to a variable, it's an **expression** 

```js
// this is a function declaration

function func(){
  var local = true;
};

// this is a function expression

var func = function(){
  var local = true;
}
```

The difference is in how the browser loads them into the execution context.  

**Declarations are hoisted**. They load before any code is executed.  
Expressions load only when the interpreter reaches that line of code. 

___

### Local Scope
Create local scope by wrapping it in a function

```js
var func = function(){
  var local = true;
};
```

```js
console.log(local);
// !! ReferenceError: local is not defined 
```

`local` exists inside the scope of `func`. It cannot be accessed from the global scope.  
 
### Global Scope
Global variables can be accessed anywhere in your application. You generally want to avoid creating variables in the global

Declare a variable in the global scope outside of a function, or if you initialize it inside of a function without `var` it becomes part of the global scope.   

___

## Parent / Child Scope
Nested functions create a “child” scope within the containing function. The parent scope does not have access to the child scope. However the child scope does have access to the parent scope.  

```js
var g = 'global';

function blender(fruit){
  var b = fruit;
  var y = 'yogurt';

  function bs(){
    var x = 'asdf'
    console.log( b + ' and ' + y + ' makes ' + b + ' swirl' );
  }
  bs();
}

blender('blueberry');
```

> "blueberry and yogurt makes blueberry swirl"
<

The child scope has access to the parent scope, but parent doesn't have access to child scope.  

___

## Precedence
In JavaScript, there can be conflicts when two variables have a the same name. Bianca demonstrates how precedence works when a global variable has the same name as a local variable.  


### Privacy 
Create privacy by storing variables in a function

```js
var g = 'global';

function go(){
  var l = 'local';
  var g = 'in here!';
  console.log(g + " inside go");
}
go();
console.log(g + " outside go");

```

### Block Scope
blocks are the stuff in between squiggly brackets *(that isn't JSON)*

```js
function mrFunction(whatever){
  // this whole damn thing is a block
  for (loop){
    // this is also  a block -- telling the loop to do stuff
    if (condition){
      // another block -- telling you what to do if ...
    } else {
      // this is a block. do it. 
    }
    return 
    {
      // Not a block. This is an object.
      something: 'xyz'
      somethingElse: 'wee'
    };
  };
}
```

* JavaScript doesn't have block scope.  
* The `let` keyword deals with block scope, but we're not getting into all that just yet.  

```js
var inBlock = false;

for (var i = 0;  i < 5; i++){
  var inBlock = true;
};

if (inBlock){
  console.log( 'Is there block scope? ' + !inBlock );
}
```
* There is no function here. Everything is in the global scope. 

> "Is there block scope? false"

___


## a function has access to its own local scope variables

```js

var fn = function () {
  var name = 'inner';
  ACTUAL = name;
};
fn();
expect(ACTUAL === 'inner').to.be.true;

```

* because `name` is 'inner' and `ACTUAL` references `name`;

___

## inputs to a function are treated as local scope variables

```js

var fn = function (name) {
  ACTUAL = name;
};
fn('inner');
expect(ACTUAL === 'inner').to.be.true;

```


___

## a function has access to the variables contained within the same scope that function was created in

```js

var name = 'outer';
var fn = function () {
  ACTUAL = name;
};
fn();
expect(ACTUAL === 'outer').to.be.true;

```


___

## a function's local scope variables are not available anywhere outside that function

```js

var firstFn = function () {
  var localToFirstFn = 'inner';
};
firstFn();

expect(function () {
  ACTUAL = localToFirstFn;
}).to.throw();

expect(ACTUAL === null).to.be.true;

```



___

## a function's local variables aren't available outside that function, regardless of the context it's called in

```js

        var firstFn = function () {
          var localToFirstFn = 'first';
          // Although false, it might seem reasonable to think that the secondFn (which mentions the localToFirstFn variable), should have access to the localToFirstFn variable, since it's being called here from within the scope where that variable is declared.
          secondFn();
        };
        
        var secondFn = function () {
          ACTUAL = localToFirstFn;
        };

        expect(function () {
          // of course, calling the secondFn should throw an error in this case, since secondFn does not have access to the localToFirstFn variable
          secondFn();
        }).to.throw();

        expect(function () {
          // in addition, calling the firstFn (which in turn calls the secondFn) should also throw, since it the calling context of secondFn has no influence over its scope access rules
          firstFn();
        }).to.throw();

        expect(ACTUAL === null).to.be.true;

```


___

## Precedence 
If an inner and an outer variable share the same name, and the name is referenced in the inner scope, the inner scope variable masks the variable from the outer scope with the same name. This renders the outer scope variables inaccassible from anywhere within the inner function block 

```js

var sameName = 'outer';
var fn = function () {
  var sameName = 'inner';
  ACTUAL = sameName;
};

fn();
expect(ACTUAL === 'inner').to.be.true;

```



___

## Precedence 2
if an inner and an outer variable share the same name, and the name is referenced in the outer scope, the outer value binding will be used.

```js
‣
var sameName = 'outer';
var fn = function () {
  var sameName = 'inner';
};
fn();
ACTUAL = sameName;
expect(ACTUAL === 'outer').to.be.true;

```



___

## A new variable scope is created for every call to a function.
This is exemplified here with a counter, `innerCounter`

```js

    var fn = function () {

      var innerCounter = innerCounter || 10;
      innerCounter = innerCounter + 1;

      ACTUAL = innerCounter;
    };


    fn();
    expect( ACTUAL === 11).to.be.true;

    fn();
    expect( ACTUAL === 11).to.be.true;
      
```

the `||` symbol here is being used to set a default value for `innerCounter`.  

If `innerCounter` already contains a truthy value, then the value in that variable will be unchanged. If it is falsey however (such as if it were completely uninitialized), then this line will set it to the default value of 10.


___

## Alpha and Omega
This is a longer form of the same observation as above, using strings in stead of numbers. A new variable scope is created for each call to a function, as exemplified with uninitialized string variables 

```js
var fn = function () {
  var localVariable;

  if (localVariable === undefined) {
    ACTUAL = 'alpha';
  } else if (localVariable === 'initialized') {
    ACTUAL = 'omega';
  }

  localVariable = 'initialized';
};


fn();
expect( ACTUAL === 'alpha').to.be.true;

fn();
expect( ACTUAL === 'alpha').to.be.true;

```

`localVariable` is always undefined when the conditional occurs.  
It is set to 'initialized' afterwards, but the since a new variable scope occurs every time `fn()` is called, `localVariable` is created from scratch. It might seem like the second call should return 'omega', but this is not the case.


___

## Inner Scope can Access Parent Scope Variables
An inner function can access both its local scope variables and variables in its containing scope, provided the variables have different names

```js

    var outerName = 'outer';

    var fn = function () {
      var innerName = 'inner';
      ACTUAL = innerName + outerName;
    };

    fn();
    expect( ACTUAL === 'innerouter').to.be.true;

```



___

## Inner Scope can Access and Change Outer Scope Variables
Between calls to an inner function, that inner function retains access to a variable in an outer scope.  
Modifying those variables has a lasting effect between calls to the inner function.  

```js
    var outerCounter = 10;

    var fn = function () {
      outerCounter = outerCounter + 1;
      ACTUAL = outerCounter;
    };

    fn();
    expect(ACTUAL === 11).to.be.true;
    fn();
    expect(ACTUAL === 12).to.be.true;

```


___

## Even After the Outer Function has Returned
The rule about retaining access to variables from an outer scope still applies, even after the outer function call (that created the outer scope) has returned.  

```js
      var outerFn = function () {

          var counterInOuterScope = 10;

          var innerIncrementingFn = function () {
              counterInOuterScope = counterInOuterScope + 1;
              ACTUAL = counterInOuterScope;
          };

          innerIncrementingFn();
          expect(ACTUAL === 11 ).to.be.true;

          innerIncrementingFn();
          expect(ACTUAL === 12 ).to.be.true;
          
          window.retainedInnerFn = innerIncrementingFn;

      };

      expect( window.retainedInnerFn).to.equal.undefined;


      outerFn();
      expect(window.retainedInnerFn).to.be.a('function');

      window.retainedInnerFn();
      expect(ACTUAL === 13 ).to.be.true;

```

___
