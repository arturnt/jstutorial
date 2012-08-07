Let's talk about Javascript.
==========

First off, Javascript is an object oriented language(hence refered to as JS). What does that mean? Everything is an object. Yes, you read that right, everything is an object. Understanding how objects work in the JS world is a key to understanding the language itself.


### Objects

What are objects? They are just a list of properties: `color: blue, height: 5"11', sex: M`. You are an object. That's it. Some objects have behaviors, those are functions and we'll talk about those later.

How do we make objects? There are fundamentally 2 ways of making objects, only 2:

##### Object Literal Notation
This creates an object from thin air. Wierd, huh?

    {
      color: "blue",
    	height: 71,
    	sex: "M"
    }

That's all it takes! You might think, isn't this a map? Good point. There is no difference between a map/hashmap/associated-array/whathaveyou and a JS object. They are the same exact thing, and every object can be reduced to a map.

##### With another Object of type Function. 
In other languages we call this a constructor:

    function Person() {
	     this.color = "blue"
	     this.height = 71
	     this.sex = "M"
	     return this;
    }

Here is the trick with this method, you cannot do:

    var person = Person(); // Doesn't make an object, just calls the method.

You have to do:

    var person = new Person(); // Makes an object

The 'new' keyword in Javascript indicates that you calling this function as a function or you actually want to make a new object.

**Note**: The Javascript overloards thought that method (2) was too confusing so they introduced a new method in ECMAScript5 that replaces method (b). This though is more of a shortcut, you can do it yourself. It's called: `Object.create()`. Here is a glimpse into what it looks like:

    Object.create = function(anotherObject) {
	     var obj = new function() {}
	     obj.prototype = anotherObject;
	     return obj;
    }

and it is used like so:

    var person = Object.create()
    person.color = "blue"

What is it doing? Well it's using method (2) above, and then using something called prototypes which we will talk about later to say inherit things from anotherObject if I don't define them. It gets rid of the concept of a constructor in the traditional sense.



### Types

Before we delve any further we should really talk about types, and the important operator "typeof".Objects that we talked about above will have types. For the most part, the built in objects will have more interesting types like "string" or "number", and the ones we create will be a little more boring like "object". Let's talk about types in terms of examples:

    typeof "hello" // = string
    typeof Infinity // = number, Infinity is a built-in number.
    typeof NaN // = number, means Not a Number.
    typeof .0123 // = number
    typeof true // = boolean
    typeof [] // = object
    typeof null // = object
    typeof new Number(4) // = object
    typeof SomethingIDidntDefine // = undefined
    typeof Object.create // = function

First 3 are objects, but the result of their type is pretty predictable. Why is an array(4th) an object? The dirty secret is that an array is well also a map/object. So if you take `["a", "b", "c"]`, it's being stored as `{ "1": "a", "2": "b", "3": "c" }`. Arrays have a lot of other operations that make them valuable, which we'll talk about later.

Another interesting thing is doing a typeof on something that is not defined, this is the only operator that will not give you an error trying to access something that you have never seen before. This is commonly a good way to check if the variable has been defined. 

Why is `null` an object? Wierd, right? `Null` in Javascript is an object with no properties or behaviors that has a sole responsibilty of representing the concept of I know this variable is unknown. This is different from undefined, which is it could be unknown or known but you don't know that. This is the same as Donald Rumsfeld's Known Unknowns and Unknown Unknowns.


### Equality

The world of Javascript is fraught with confusion over equality. I'm not talking about civil rights. The strength or weakness depending on how you look at is that JS does a lot of type coersion or in other words taking one type and using some rules to convert it into another to compare them. This might be something you want or not, but usually not! There are two operations `==` and `===`. The `===` operator is prefered(faster and more predictable), because it guarantees to match types up first. Let's go through some examples:

    "" == 0 // true???
    "b" == 0 // false!
    true == 1 // true
    null == undefined // true
    "5" == 5 // true
    5 === 5 // true
    "5" === 5 // false

A lot of the coersions here can be explained, but the lesson is that the double equals is not predictable and hard to read and is best to not use in practice, unless you are coding with a bunch of JS ninjas and trying to save a few bytes from your file. 

**Note**: The real reason for why you see the above wierd behavior is that JS will convert certain things to true or false, when forced to. The following are *falsy* in JS, or in otherwords get converted to false during type coersion:

    false
    null
    undefined
    ""
    0
    NaN

Everything else is *truthy*. 
