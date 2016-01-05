## Nesting

```js
var box = {};
box.innerBox = {};
box['innerBox']['full'] = true;

var box3 = {};
box3 ['innerBox'] = {};
box3.innerBox.full = false;
```
*returns* -->
>>>```js
var box =
  {
    "innerBox" : {
      full : true
    }
  }
```

```js
var box = {};
box.innerBox = {};
box.innerBox.babyBox = {};
box.innerBox['babyBox'];
box.innerBox['babyBox'].says = "What's up!?";
```

*returns* -->

>>>```js
var box =
  {
    innerBox : { babyBox : { says : "What's up!?" } }
   }
```

Let's represent a relationship between two animals in our collection. Imagine that our app has a 'friendslist' on an animal's profile which lists out all of the animal's friends. Let's walk through the process together.

### Create a Friendslist
* Create an array for the list of friends' usernames.
* Create a variable called friends and assign it to the empty data structure.

```js
function addFriend (animal, friend){
  animal.friends.push( friend.username)
}
```
___

### Create a Relationships Object
Imagine now that we have more than one kind of relationship in our app, we have friends and then we have romantic matches. Let's create an object to organize these different relationships!

* Create a variable called relationships assign it to an empty object.

```js
function AnimalCreator(username, species, tagline, noises){
  return {
            username: username, 
            species: species, 
            tagline: tagline,
            noises: noises,
  };
}


function addRelationships(farm){
  for( var i = 0; i < farm.length; i++ ){
    farm [i].relationships = { friends : [], matches : [] };
  }
}


function addFriends (animal, friend){
  animal.relationships.friends.push( friend.username)
}


addFriends(skoog, luna);
addFriends(skoog, moose);
addFriends(luna, skoog);
addFriends(luna, moose);
addFriends(moose, skoog);
addFriends(moose, luna);


function giveMatches(arr, obj){
  arr.forEach( obj => obj.relationships.matches.push( obj.relationships.friends [1] ));
}
```

___
