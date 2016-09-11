**A symbol is a unique and immutable data type and may be used as an identifier for object properties**

You can use it, with this synthax :<br>
`var symbol = Symbol();`<br>
`var symbol = Symbol("keyName");`<br>
_keyName is a description for the symbol_<br>

**Why should I use it ?**<br>
Symbols are values that programs can create and use as property keys without risking name collisions.<br>
Calling Symbol() creates a new symbol, a value that’s not equal to any other value.<br>
Just like a string or number, you can use a symbol as a property key. Because it’s not equal to any string, this symbol-keyed property is guaranteed not to collide with any other property.<br>

**An example**<br>
In this example we want to declare an attribute *type* to our Pet, after that extend it with a function *getType*<br>

**1**<br>
  Pet declare an attribute *type* link to the context. But he can be overwrite outside the context.<br>
  
        var Pet = (function() {
          function Pet(type) {
            this.type = type;
          }
          Pet.prototype.getType = function() {
            return this.type;
          }
          return Pet;
        }());

        var a = new Pet('dog');
        console.log(a.getType());//Output: dog
        a.type = null;
        //Modified outside
        console.log(a.getType());//Output: undefined
        
**2**<br>
To make it private we have to create a closure. Below example illustrates how we can make type private using closure.<br>

        var Pet = (function() {
          function Pet(type) {
            this.getType = function(){
              return type;
            };
          }
          return Pet;
        }());
        
        var b = new Pet('dog');
        console.log(b.getType());//dog
        b.type = null;
        //Stays private
        console.log(b.getType());//dog
        
Disadvantage of above approach: We are introducing extra closure for each Pet instance created.<br>

**3**<br>
Now we introduce Symbol. This can help us getting a property as private without using extra unnecessary closure.<br>
Even if you declare another *Symbol('type')* result will not be the same.<br>

        var Pet = (function() {
          var typeSymbol = Symbol('type');
          function Pet(type) {
            this[typeSymbol] = type;
          }
          Pet.prototype.getType = function(){
            return this[typeSymbol];
          }
          return Pet;
        }());
        
        var a = new Pet('dog');
        console.log(a.getType());//Output: dog
        a.type = null;
        //stays private
        console.log(a.getType());//Output: dog
        
        
**Source for more details**<br>
[ES6 In Depth: Symbols](https://hacks.mozilla.org/2015/06/es6-in-depth-symbols/)<br>
[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)<br>
