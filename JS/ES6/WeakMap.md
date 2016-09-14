**The WeakMap object is a collection of key/value pairs in which the keys are weakly referenced.  The keys must be objects and the values can be arbitrary values.**

You can use it, with this synthax :<br>
`var weakMap = new WeakMap([iterable])`<br>
_iterable is an Array or other iterable object whose elements are key-value pairs_<br>
`var weakMap = new WeakMap([[new Date(), 'foo'], [() => 'bar', 'baz']])`<br>

**Why should I use it ?**<br>
In native WeakMaps, references to key objects are held "weakly", which means that they do not prevent garbage collection in case there would be no other reference to the object.
Because of references being weak, WeakMap keys are not enumerable.

**An example**<br>
In this example you have a Map and a WeakMap object, after remove the key we want to print our Map / WeakMap.

        var k1 = {a: 1};
        var k2 = {b: 2};
        
        var map = new Map();
        var wm = new WeakMap();
        
        map.set(k1, 'k1');
        wm.set(k2, 'k2');
        
        k1 = null; //set k1 to null
        map.forEach(function (key, val) {
            console.log(key, val); // even after k1 set to null you can still access to key/value with forEach function k1 {a: 1}
        });
        wm.has(k2); // true
        k2 = null;
        wm.has(k2); // false
        wm.get(k2); // undefined and there aren't a method to list the keys

<br><br>**More**

_Not working :_<br>

        w = new WeakMap;
        w.set('a', 'b');

_If you really want to use a primitive type key ( string, number, boolean, null, undefined, symbol ), use Map object :_<br>
        
        m = new Map
        m.set('a', 'b');

**Source for more details**<br>
[Example at stackoverflow](http://stackoverflow.com/questions/15604168/whats-the-difference-between-es6-map-and-weakmap)<br>
[Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/WeakMap)<br>
