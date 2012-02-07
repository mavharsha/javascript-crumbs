# Built-in objects

## Object
Object is the parent of all JavaScript objects, which means that every object you create inherits from it.  
To create a new empty object you can use the literal notation or the `Object()` constructor function.  

```js
var o = {};
var o = new Object();
```

An empty object already contains some methods and properties:

* `o.constructor` property returns the constructor function
* `o.toString()` is a method that returns a string representation of the object
* `o.valueOf()` returns a single-value representation of the object, often this is the object itself

```js
var o = new Object();
o.toString()   // "[object Object]"
```

`toString()` will be called internally by JavaScript, when an object is used in a string context.  
For example alert() works only with strings, so if you call the alert() function passing an object, the method toString() will be called behind the scenes.

```js
alert(o)
alert(o.toString())
```

Another type of string context is the string concatenation. 
If you try to concatenate an object with a string, the object's `toString()` will be called first.

```js
"An object: " + o   // "An object: [object Object]"
```

`valueOf()` is another method that all objects provide.  
For the simple objects (whose constructor is Object()) the valueOf() method will return the object itself.

```js
o.valueOf() === o   // true
```

## Array
Arrays are objects, but of a special type because:

* the names of their properties are automatically assigned using numbers starting from 0
* they have a length property which contains the number of elements in the array
* they have additional built-in methods in addition to those inherited from the parent object

### Array initializer

```js
var empty = []   // An empty array: no expressions inside brackets means no elements
var plain = [1+2,'four']   // A 2-element array. First element is 3, second is the string 'four'
var matrix = [[1,2,3], [4,5,6], [7,8,9]]; // nested array
var sparseArray = [1,,,,5];
```

### Array constructor function

```js
var empty = new Array();
var plain = new Array(2+1,'four');
var a = new Array(5);
empty.length;   // 0
plain.length;   // 2
a.length;   // 5

/* Array is a constructor function for arrays */
plain.constructor;   // function Array() ...

/* Array is an object */
typeof a;   // "object"
```

### Stack methods: push, pop
A stack is referred to as a last-in-first-out (LIFO) structure.  
The insertion (called a push) and removal (called a pop) of items in a stack occur at only one point: the top of the stack.  
ECMAScript arrays provide `push()` and `pop()` specifically to allow stack-like behavior.  

```js
var colors = new Array();   // create an array
var count = colors.push('red', 'green'); // push any number of items
count;   // 2

count = colors.push('black');   // push another item on
count;   // 3

var item = colors.pop();   // get the last item
item;   // "black"
colors.length;   // 2
```

### Queue methods: shift, unshift
Queues restrict access in a first-in-first-out (FIFO) data structure.  
A queue adds items to the end of a list and retrieves items from the front of the list.  
Already knonw `push()` method adds items to the end of an array.  
`shift()` method retrieve the first item in the array.  
Using shift() in combination with push() allows arrays to be used as queues.  

```js
var colors = new Array();   // create an array
var count = colors.push('red', 'green');   // push two items
count;   // 2

count = colors.push('black');  // push another item on
count; // 3

var item = colors.shift();   // get the first item
item;   // "red"
colors.length;   // 2
```

ECMAScript also provides an `unshift()` method for arrays.  
`unshift()` does the opposite of `shift()`: it adds any number of items to the front of an array and returns the new array length.  
By using `unshift()` in combination with `pop()`, it’s possible to emulate a queue where new values are added to the front of the array and values are retrieved off the back.  

```js
var colors = new Array();   // create an array
var count = colors.unshift('red', 'green');   // push two items
count   // 2

count = colors.unshift('black');   // push another item on
count;   // 3

var item = colors.pop();
item;   // "green"
colors.length;   // 2
```

### Reordering methods: reverse, sort

```js
var values = [1, 2, 3, 4, 5];
values.reverse();
values;   // 5,4,3,2,1

var values = [0, 1, 5, 10, 15];
values.sort();
values;   // 0,1,10,15,5
```

`sort()` method default behaviour changes order based on lexicographical order.  
It can be changed by passing a comparing function.

```js
function compare(value1, value2) {
  return value2 - value1;
}

var values = [0, 1, 5, 10, 15];
values.sort(compare);
values;   // 0,1,5,10,15
```

### Manipulation methods: concat, slice, splice

#### concat

```js
var colors = ["red", "green", "blue"];
var colors2 = colors.concat("yellow", ["black", "brown"]);
colors;   // red,green,blue
colors2;  // red,green,blue,yellow,black,brown
```

#### slice

```js
var colors = ["red", "green", "blue", "yellow", "purple"];
var colors2 = colors.slice(1);
var colors3 = colors.slice(1,4);
colors2;   // green,blue,yellow,purple
colors3;   // green,blue,yellow
```

If either the start or end position of `slice()` is a negative number, then the number is subtracted from the length of the array to determine the appropriate locations.  
Calling `slice(-3, -1)` on an array with five items is the same as calling `slice(2, 4)`.  
If the end position is smaller than the start, then an empty array is returned.

#### splice
`splice()` is useful for _deletion_, _insertion_ and _replacement_ in the middle of an array.

```js
var colors = ["red", "green", "blue"];
var removed = colors.splice(0,1);   // remove the first item
colors;    // green,blue
removed;   // red - one item array

removed = colors.splice(1, 0, "yellow", "orange");  // insert two items at position 1
colors;    // green,yellow,orange,blue
removed;   // empty array

removed = colors.splice(1, 1, "red", "purple");   // insert two values, remove one
colors;    // green,red,purple,orange,blue
removed;   // yellow - one item array
```

### Location methods: indexOf, lastIndexOf
The `indexOf()` method starts searching from the front of the array (item 0) and continues to the back.  
The `lastIndexOf()` starts from the last item in the array and continues to the front.  
The methods each return the position of the item in the array or –1 if the item isn’t in the array.  
`===` is used in comparison.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

numbers.indexOf(4);   // 3
numbers.lastIndexOf(4);   // 5

numbers.indexOf(4, 4);   // 5
numbers.lastIndexOf(4, 4);   // 3

var person = { name: "Nicholas" };
var people = [{ name: "Nicholas" }];

var morePeople = [person];
people.indexOf(person);   // -1
morePeople.indexOf(person);   // 0
```

### Iterative methods: every, filter, forEach, map, some
Each of the iterative methods accepts two arguments:

  1. a function to run on each item
  2. an optional scope object in which to run the function (affecting the value of `this`)

The function passed into one of these methods will receive three arguments:

  1. the array item value
  2. the position of the item in the array
  3. the array object itself

#### every
Runs the given function on every item in the array and returns true if the function returns true for every item.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var everyResult = numbers.every(function(item, index, array) {
  return (item > 2);
});

everyResult;   //false
```

#### some
Runs the given function on every item in the array and returns true if the function returns true for any one item.

```js
var someResult = numbers.some(function(item, index, array) {
  return (item > 2);
});

someResult;   //true
```

#### filter
Runs the given function on every item in the array and returns an array of all items for which the function returns true.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var filterResult = numbers.filter(function(item, index, array){
  return (item > 2);
});

filterResult;   //[3,4,5,4,3]
```

#### forEach
Runs the given function on every item in the array. This method has no return value.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

numbers.forEach(function(item, index, array){   
    //do something here
});
```

#### map
Runs the given function on every item in the array and returns the result of each function call in an array.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var mapResult = numbers.map(function(item, index, array){
    return item * 2;
});

mapResult;   // [2,4,6,8,10,8,6,4,2]
```

### Reduction methods: reduce, reduceRight
Both methods accept two arguments:

  1. a function to call on each item
  2. an optional initial value upon which the reduction is based

The passed function accepts four arguments:
  1. the previous value
  2. the current value
  3. the item's index
  4. the array object

Any value returned from the function is automatically passed in as the first argument for the next item.  
The first iteration occurs on the second item in the array.  
`reduce()` perform reduction in left-to-right order.  
`reduceRight()` perform reduction in right-to-left order

```js
var values = [1,2,3,4,5];

var sum = values.reduce(function(prev, cur, index, array){
  return prev + cur;
});

sum;   // 15


var values = [1,2,3,4,5,15];

var sum = values.reduceRight(function(prev, cur, index, array){
  return prev - cur;
});

sum;   // 0
```

## Function

### Properties of the Function objects
Like any other object, functions have a constructor property that contains a reference to the `Function()` constructor function.

```js
function myfunc(a){return a;}
myfunc.constructor   // Function()
```

Functions also have a `length` property, which contains the number of parameters the function accepts.

```js
function myfunc(a, b, c){ return true; }
myfunc.length   // 3
```

The most important property of a function is the `prototyp`e property.  
The `prototype` property of a function contains an object.  
It is only useful when you use this function as a constructor.  
All objects created with this function keep a reference to the `prototype property and can use its properties as their own.

```js
var some_obj = {
    name: 'Ninja',
    say: function(){
        return 'I am a ' + this.name;
    }
}

/* A hollow function automatically has a prototype
 * property that contains an empty object */
function F() {}
typeof F.prototype   // "object"

F.prototype = some_obj;

var obj = new F();
obj.name    // "Ninja"
obj.say()   // "I am a Ninja"
```

### Methods of the Function objects
Two useful methods of the function objects are `call()` and `apply()`.  
They allow your objects to borrow methods from other objects and invoke them as their own.


#### call

```js
var some_obj = {
    name: 'Ninja',
    say: function(who) {
        return 'Haya ' + who + ', I am a ' + this.name;
    }
}

some_obj.say('Dude');   // "Haya Dude, I am a Ninja"

my_obj = {name: 'Scripting guru'};

some_obj.say.call(my_obj, 'Dude')   // "Haya Dude, I am a Scripting guru"
```

When `say()` was invoked with `call`, the references to `this` value that it contains, pointed to `my_obj`.  
This way `this.name` didn't return `Ninja`, but `Scripting guru` instead.  

If you have more parameters to pass when invoking the `call()` method, you just keep adding them

```js
some_obj.someMethod.call(my_obj, 'a', 'b', 'c');
```

If you don't pass an object as a first parameter to `call()` or pass `null`, the global object will be assumed.

#### apply
The method `apply()` works the same way as `call()` but with the difference that all parameters you want to pass to the method of the other object are passed as an array.

```js
/* Two following code line are equivalent */
some_obj.someMethod.apply(my_obj, ['a', 'b', 'c']);
some_obj.someMethod.call(my_obj, 'a', 'b', 'c');

some_obj.say.apply(my_obj, ['Dude']);   // "Haya Dude, I am a Scripting guru"
```

## Boolean
`Boolean()` Function is the constructor for the wrapping object of the Boolean values.

```js
var booleanObject = new Boolean(true);
```

Pay attention to not use Boolean object as Boolean expression.

```js
var falseObject = new Boolean(false);
var result = falseObject && true;
result;   // true

var falseValue = false;
result = falseValue && true;
result;   // false

typeof falseObject;   // object
typeof falseValue;    // boolean
falseObject instanceof Boolean;   // true
falseValue instanceof Boolean;    // false
```

The `Boolean()` function is useful when called as a normal function, without `new`.  
This converts non-booleans to booleans (which is the same as using a double negation `!!` value).

```js
Boolean("test")   // true
Boolean("")   // false
Boolean({})   // true
```

### Number
`Number()` Function is the constructor for the wrapping object of the numeric values.

```js
var numberObject = new Number(10);
```

Pay attention to use Number instead of primitive Number value.

```js
var numberObject = new Number(10);
var numberValue = 10;
typeof numberObject;   // "object"
typeof numberValue;   // "number"
numberObject instanceof Number; // true
numberValue instanceof Number;  // false
```

`Number()` function contains some interesting built-in properties (which you cannot modify):

```js
Number.MAX_VALUE   // 1.7976931348623157e+308
Number.MIN_VALUE   // 5e-324
Number.POSITIVE_INFINITY   // Infinity
Number.NEGATIVE_INFINITY   //-Infinity
Number.NaN   // NaN
```

`Number()` function without `new` converts any value ti a number.

```js
var n = Number('12.12');
n   // 12.12
typeof n   // "number"
```

### Number object's methods
#### toString
It optionally accepts a single argument indicating the radix in which to represent the number

```js
var num = 10;
num.toString();   // "10"
num.toString(2);   // "1010"
num.toString(8);   // "12"
num.toString(10);   // "10"
num.toString(16);   // "a"
```
#### toFixed
It returns a string representation of a number with a specified number of decimal points.  
It accepts an arguments indicating how many decimal places should be displayed.

```js
var num = 10;
num.toFixed(2);   // "10.00"

var num = 10.005;
num.toFixed(2);   // "10.01"
```

#### toExponential
It returns a string with the number formatted in exponential notation.  
It accepts one argument, which is the number of decimal places to output.

```js
var num = 10;
num.toExponential(1);   // "1.0e+1"
```

#### toPrecision
It returns either the fixed or the exponential representation of a number, depending on which makes the most sense.  
It takes one argument, which is the total number of digits to use to represent the number (not including exponents).

```js
var num = 99;
num.toPrecision(1);   // "1e+2"
num.toPrecision(2);   // "99"
num.toPrecision(3);   // "99.0"
```

## String
String type is the object representation for strings.  
`length` property indicates number of character.

```js
var stringObject = new String('I love JavaScript!');
console.log(stringObject.length);   // > 11
```

Strings allow for bracket notation access to single character.

```js
var stringValue = 'hello world';
console.log(stringValue[1]);   // > "e"
```

`String()` function without `new` converts the parameter to a primitive string.

```js
String(1)   // "1"
String({p: 1})  // "[object Object]"
String([1,2,3])   // "1,2,3"
```

### String object's methods

#### charAt(pos)
It returns the character in the given position as a single-character string, like bracket notation access.  
It accepts a single argument, which is the character’s zero-based position.

```js
var stringValue = 'hello world';
console.log(stringValue.charAt(1));   // > "e"
```

#### charCodeAt(pos)
It returns the character code in the given string position.  
It accepts a single argument, which is the character’s zero-based position.

```js
var stringValue = 'hello world';
console.log(stringValue.charCodeAt(1));   // > 101
```

#### concat(str...)
It concatenates one or more strings to another.  
It accepts any number of strings to concatenate as arguments.

```js
var stringValue = 'hello, ';
var result = stringValue.concat('my ', 'name ', 'is ', 'Bob');
console.log(result);   // > "hello, my name is Bob"
console.log(stringValue);   // > "hello, "
```

#### indexOf(searchString, position)
It searches for a searchString within a string.  
If it is found, it returns the position of the first matched character;  
otherwise, it returns –1.  
The optional position parameter causes the search to begin at some specified position in the string.

```js
var text = 'Mississippi';
var p = text.indexOf('ss');
console.log(p);   // > 2
p = text.indexOf('ss', 3);   // > 5
p = text.indexOf('ss', 6);   // > -1
```

#### lastIndexOf(searchString, position)
Like the `indexOf` method, except that it searches from the end of the string instead of the front:

```js
 var text = 'Mississippi';
 var p = text.lastIndexOf('ss');
 console.log(p);   // > 5
 p = text.lastIndexOf('ss', 3);
 console.log(p);   // > 2
 p = text.lastIndexOf('ss', 6);   // > 5
```

#### match(regexp)
...

#### replace(searchValue, replaceValue)
...

#### search(regexp)
...

#### slice(start, end)
It returns a new string by copying a portion of another string.  
It accepts two arguments: _start_ and _end_ position of the string portion.  
End argument is optional, its default value is _string.length_.  
If _start_ or _end_ are negative then _string.length_ is added to them.

```js
 var text = 'and in it he says "Any damn fool could"';
 var a = text.slice(18);
 console.log(a);   // > ""Any damn fool could"
 var b = text.slice(0, 3);
 console.log(b);   // > "and"
 var c = text.slice(-5);
 console.log(c);   // > "could"
 var d = text.slice(19, 32);
 console.log(d);   // > "Any damn fool"
```

#### split(separator, limit)
...

#### substr(?)
...

#### substring(star, end)

#### toLowerCase()
...

#### toUpperCase()
...

#### fromCharCode(char...)
...


## Date
the Date type stores dates as the number of milliseconds that have passed since midnight on January 1, 1970 UTC (Universal Time Code)

```js
var now = new Date();

now.toDateString();
now.toString();
```

Date constructor accept many format:

* month/date/year (such as 6/13/2004)
* month_name date, year (such as January 12, 2004)
* day_of_week month_name date year hours:minutes:seconds time_zone (such as Tue May 25 2004 00:00:00 GMT-0700)
* ISO 8601 extended format YYYY-MM-DDTHH:mm:ss.sssZ (such as 2004-05-25T00:00:00)

```js
var someDate = new Date("May 25, 2004");
var someDate = new Date("25/5/2004");
var someDate = new Date('Tue May 25 2004 00:00:00 GMT-0700');
var someDate = new Date('2004-05-25T00:00:00');
```

### now
`now()` method is useful for profiling functions: it returns elapsed time since January 1, 1970 UTC in milliseconds

```js
var start = Date.now();   //get start time   //call a function doSomething();

var stop = Date.now();   //get stop time
var result = stop – start;
```


## RegExp

### Regex literals

[Regular expressions](http://www.regular-expressions.info/) are easy to create.

```js
var expression = /pattern/flags;
```

Flags can be:

* `g` — global mode, meaning the pattern will be applied to all of the string instead of stopping after the first match is found
* `i` — case-insensitive mode, meaning the case of the pattern and the string are ignored when determining matches
* `m` — multiline mode, meaning the pattern will continue looking for matches after reaching the end of one line of text


### Regexp examples

```js
/* Match all instances of "at" in a string. */
var pattern1 = /at/g;

/* Match the first instance of "bat" or "cat", regardless of case. */
var pattern2 = /[bc]at/i;

/* Match all three-character combinations ending with "at", regardless of case. */
var pattern3 = /.at/gi;
```

_metacharacter_ : `( [ { \ ^ $ | ) ] } ? * + .`

```js
/* Match the first instance of "bat" or "cat", regardless of case. */
var pattern1 = /[bc]at/i;

/* Match the first instance of "[bc]at", regardless of case. */
var pattern2 = /\[bc\]at/i;

/* Match all three-character combinations ending with "at", regardless of case. */
var pattern3 = /.at/gi;

/* Match all instances of ".at", regardless of case. */
var pattern4 = /\.at/gi;

/* Match the first instance of "bat" or "cat", regardless of case. */
var pattern1 = /[bc]at/i;

/* Same as pattern1, just using the constructor. */
var pattern2 = new RegExp("[bc]at", "i");
```

### Instance methods: exec, test

### exec
It is intended for use with capturing groups `( ... )`.  
It accepts a single argument, which is the string on which to apply the pattern.  
It returns an array of information about the first match or _null_ if no match was found.  
The returned array, though an instance of Array, contains two additional properties:

  1. `index`, which is the location in the string where the pattern was matched
  2. `input`, which is the string that the expression was run against.

In the array, the first item is the string that matches the entire pattern, any additional items represent captured groups inside the expression.

```js
var text = "mom and dad and baby";
var pattern = /mom( and dad( and baby)?)?/gi;
var matches = pattern.exec(text);
￼￼￼￼matches.index;   // 0
matches.input;   // "mom and dad and baby"
matches[0];   // "mom and dad and baby"
matches[1];   // " and dad and baby"
matches[2];   // " and baby"

var text = “cat, bat, sat, fat";
var pattern1 = /.at/;

var matches = pattern1.exec(text);
matches.index;   // 0
matches[0];   // cat
pattern1.lastIndex;   // 0

matches = pattern1.exec(text);
matches.index;   // 0
matches[0];   // cat
pattern1.lastIndex;   // 0

var pattern2 = /.at/g;

var matches = pattern2.exec(text);
matches.index;   // 0
matches[0];   // cat
pattern2.lastIndex;   // 0

matches = pattern2.exec(text);
matches.index;   // 5
matches[0];   // bat
pattern2.lastIndex;   // 8
```

#### test
It accepts a string argument and returns _true_ if the pattern matches the argument and _false_ if it does not.

```js
var text = “000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;
if (pattern.test(text)) {
  "The pattern was matched.";
}
```

## Math object
ECMAScript provides the `Math` object as a common location for mathematical formulas and information.  
The computations available on the `Math` object execute faster than if you were to write the computations in JavaScript directly.

### Math object properties
The Math object has several properties, consisting mostly of special values in the world of mathematics.

```js
Math.E        // the value of e, the base of the natural logarithms
Math.LN10     // the natural logarithm of 10
Math.LN2      // the natural logarithm of 2
Math.LOG2E    // the base 2 logarithm of e
Math.LOG10E   // the base 10 logarithm of e
Math.PI       // the value of π
Math.SQRT1_2  // the square root of 1⁄2
Math.SQRT2    // the square root of 2
```

### Math object methods

#### min() and max()

```js
var max = Math.max(3, 54, 32, 16); alert(max);   // 54
var min = Math.min(3, 54, 32, 16); alert(min);   // 3
```

To find the maximum or the minimum value in an array, you can use the `apply()` method

```js
var values = [1, 8, 3, 5, 6, 7, 2];
var maxValue = Math.max.apply(Math, values);   // 8
var minValue = Math.min.apply(Math, values);   // 1
```

#### ceil(num)
It rounds numbers up to the nearest integer value.

```js
Math.ceil(25.9);   // 26
Math.ceil(25.5);   //26
Math.ceil(25.1);   // 26
```

#### floor(num)
It rounds rounds numbers down to the nearest integer value.

```js
Math.round(25.9);   // 26
Math.round(25.5);   // 26
Math.round(25.1);   // 25
```

#### round(num)
It rounds up if the number is at least halfway to the next integer value (0.5 or higher) and rounds down if not.

```js
Math.floor(25.9);   // 25
Math.floor(25.5);   // 25
Math.floor(25.1);   // 25
```

#### random()
It returns a random number between the 0 and the 1, not including either 0 or 1.

```js
/* To select a number between 1 and 10 */
var num = Math.floor(Math.random() * 10 + 1);
```

### Other Methods

```js
Math.abs(num)        // Returns the absolute value of num
Math.exp(num)        // Returns Math.E raised to the power of num
Math.log(num)        // Returns the natural logarithm of num
Math.pow(num, power) // Returns num raised to the power of power
Math.sqrt(num)       // Returns the square root of num
Math.acos(x)         // Returns the arc cosine of x
Math.asin(x)         // Returns the arc sine of x
Math.atan(x)         // Returns the arc tangent of x
Math.atan2(y, x)     // Returns the arc tangent of y/x
Math.cos(x)          // Returns the cosine of x
Math.sin(x)          // Returns the sine of x
Math.tan(x)          // Returns the tangent of x
```