# Animal User
[Function Exercises](https://github.com/bgando/function-exercises/)

## 1. 
Write a function, `AnimalTestUser`, that has one string parameter, `username`. It returns an object with a username property.

```js
function AnimalTestUser(username){
  return {
    username : username
  };
}
```

## 2. 
In your `AnimalTestUser` function, create a check that sees how many arguments are passed. If there is more than one argument, create a property, otherArgs that is an array of the remaining arguments. Note: the arguments keyword is not a true array. Remember, it is an array-like object.

```js
function AnimalTestUser(username){
  var args = arguments.length;
  var otherArgs = [];

  if ( args > 1){
    for ( var i = 1; i < args; i++ ){
      otherArgs.push( arguments [i]);
    }
  }
  return { 
    username: username, 
    otherArgs: otherArgs
  };
}

function AnimalTestUser(username){
  var otherArgs = [];

  if (arguments.length === 1){
    return { username : username }
  } 
  else {
    for ( var i = 1; i < arguments.length; i++ ){
      otherArgs.push( arguments [i]);
    } 
      return {
                  username: username, 
                  otherArgs: otherArgs
              };
  }

}


var mySkoog = AnimalTestUser("SkoogDoogin");
var mySkoog2 = AnimalTestUser("SkoogDoogin", "thing", 25, [1,2,3] );

```
#### Pseudocode

Variable Declarations:
`otherArgs` - empty array to push arguments into

Conditional:
  * If there's only one argument
    - *return* `username` 
  * If there's more than one argument
    - loop `arguments.length` starting at 1
    - `push()` every item after `arguments [0]` into `otherArgs`
    - *return* `username` and `otherArgs`

## 3.
Write a constructor function, `AnimalCreator` that returns a single animal object. The constructor function has 4 parameters: `username`, `species`, `tagline`, and `noises`. The animal object should have at least 5 properties: `username`, `species`, `noises`, `tagline`, and `friends`. The values should all be strings except `noises` and `friends`, which are arrays.

```js
function AnimalCreator(username, species, tagline, noises){
  return {
            username: username, 
            species: species, 
            tagline: tagline,
            noises: noises,
            friends: [];
  };
}

var Desdemona = AnimalCreator("SkoogDoogin+", "dog", "I'm professor Skoog, and I approve this message", ['nosewhistle', 'snore', 'yerf'] );

Desdemona.friends = ['me', 'wz', 'luna', 'folks'];

Desdemona;

```
 >    {
       username: "SkoogDoogin+", 
       species: "dog", 
       tagline: "I'm professor Skoog, and I approve this message",
       noises: ['nosewhistle', 'snore', 'yerf'],
       friends: ['me', 'wz', 'luna', 'folks']
      }

___ 

## 4.
Write a function, `addFriend` that takes an animal object (like the one returned from the `AnimalCreator` function) and adds another animal object as a friend.

```js

function addFriend(animal, friend){
  animal.friends.push( friend)
}

```


___
## 5.
Change your `addFriend()` function to only add the `username` of the friend, not the whole object.

```js
function addFriend2 (animal, friend){
  animal.friends.push( friend.username)
}

```

___
## 6.
Create a `myFarm` collection of at least 3 animal objects. Give them some friends using `addFriend()`, too!

```js
var myFarm = [];
var skoog = AnimalCreator("skoogDoogin", "straight up dog", "pffft...okay", ['zzz', 'brrrz', 'vuv']);
var luna = AnimalCreator("loonaTheTuna", "snow monster dog", "i don't say stuff", ['quee', 'yooo', 'riii']);
var moose = AnimalCreator("moooseOnTheLooose", "blockhead dog", "derrr, lookit ma head", ['pzzz', 'pheee', 'gglunpahh']);

myFarm.push(skoog, luna, moose);

addFriends(skoog, luna);
addFriends(skoog, moose);
addFriends(luna, skoog);
addFriends(luna, moose);
addFriends(moose, skoog);
addFriends(moose, luna);
```

___
## 7.
Create a function, `addMatchesArray()`, that takes a farm (array of animal objects) and adds a new property to each animal object called `matches` that is an empty array. Hint: you will need a loop.

Use a for/in loop 

```js

// with a for loop

function addMatchesArray (farm){
  for (var i = 0; i< farm.length; i++){
    farm[i].matches = [];
  }
}

// with a for/in loop

function addMatchesArray(farm, animal){
  for( var animal in farm ){
    farm [animal].matches = [];
  }
}
```

___
## 8.
Create a function, `giveMatches`, that takes a farm collection (aka an array of animal objects) that already has a matches property. It selects a name from the friends array and adds it to the matches array. You can choose how the selection is made (random, the first element, etc). Make sure all your animal objects have friends.

#### with a loop


```js

// with a for loop

function giveMatches(farm){
  for (var i = 0; i< farm.length; i++){
    farm [i].matches.push( farm[i].friends[0] );
  }
}

// with a for/in loop

function giveMatches(farm){
  for (var animal in farm){
    farm [animal].matches.push( farm[animal].friends[0] );
  }
}

```

#### with `forEach()`

```js
function giveMatches(arr, obj){
  arr.forEach( obj => obj.matches.push( obj.friends [1] ));
}

giveMatches(myFarm);
```

___
