**The WeakSet object lets you store weakly held objects in a collection.**

You can use it, with this synthax :<br>

```
var weakSet = new WeakSet();
```
or
```
var weakSet = new WeakSet([iterable]);

/**
var value1 = { foo: 1 };
var value2 = { foo: 2 };
var weakSet = new WeakSet([value1, value2]);
**/
```

**Why should I use it ?**<br>
WeakSets are a collection of Objects where each object can only appear once in the set similar to Set. Unlike Set, WeakSet does not allow iterating over its values. If WeakSet would be the only object holding on to the value, the value will be released from memory. The values stored in WeakSet cannot be primitive values (Boolean, Number, String, or undefined).

**An example**<br>
First we don't want to fill memory with useless data, and let the garbage collector do all the work. <br />
This a story about a warrior named JARoot

```
// Warrior Class
var Warrior = (function () {
  let _name = Symbol('name');

  let _story = new WeakSet();

  function Warrior(name) {
    this[_name] = name;

    console.log(name + ' is now created!');
  }

  Warrior.prototype.getName = function () {
    return this[_name];
  };

  Warrior.prototype.addStory = function (object) {
    return _story.add(object);
  };

  Warrior.prototype.removeStory = function (object) {
    return _story.remove(object);
  };

  Warrior.prototype.verifyStory = function (object) {
    return _story.has(object);
  }

  return Warrior;
}());

//Warrior is alive!
var jaRoot = new Warrior('JARoot');
```

This warrior have a mission, he must save the princess in a castle._such originality_ <br />
To fulfill his mission, he must do three quests for acquire three rings and open the castle _wow originality kicks again_ <br />
One year was necesary to get the three rings.

```
//Rings
var ringOfGlory = {'name':'ring of glory', 'description':'Some epic description about his creation'};
var ringOfWisdom = {'name':'ring of wisdom', 'description':'Some epic description about his creation++'};
var ringOfNakama = {'name':'ring of nakama', 'description':'Some epic description about the power of Nakama that is so powerful that you can beat every boss...'};

//All quests done by the warrior
jaRoot.addStory(ringOfGlory);
jaRoot.addStory(ringOfWisdom);
jaRoot.addStory(ringOfNakama);

//At the door of the castle a voice ask him if he has accomplished all the quests
console.log(jaRoot.verifyStory(ringOfGlory)); //output : true
console.log(jaRoot.verifyStory(ringOfWisdom)); //output : true
console.log(jaRoot.verifyStory(ringOfNakama)); // output : true
```
The released princess come to the warrior and say:
_"Did you just assume that I need your help for escaping?!! I can care of myself!!"_

```
//The warrior tired of all this shit destroy all the ring
ringOfGlory = null;
ringOfNakama = null;
ringOfWisdom = null;

console.log(jaRoot.verifyStory(ringOfGlory)); //output : false
console.log(jaRoot.verifyStory(ringOfWisdom)); //output : false
console.log(jaRoot.verifyStory(ringOfNakama)); //output : false
```
*END*

**Source for more details**<br>
[Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/WeakSet)<br>
[Sitepoint](https://www.sitepoint.com/preparing-ecmascript-6-set-weakset/)<br>
