* no block scope in JS
* function scope & hoisting
* all declared vars are properties of global object
* global object is available as soon as you load compiler can be printed using this keyword
* 2 types - primitive & object, [arrays & functions are special type of objects]
* wrapper objects - Boolean, String, Number, etc & autoboxing[primitive to objects]
		var s = "test"; // Start with a string value.
		s.len = 4; // Set a property on it.
		var t = s.len; // Now query the property.
* primitive types - string, number, , null, undefined, 
* auto-typecasting - JavaScript converts values liberally from one type to another. If a program expects a string, for example, and you give it a number, it will automatically convert the number to a string for you. If you use a nonboolean value where a boolean is expected, JavaScript will convert accordingly. The rules for value conversion are explained in §3.8. Java- Script’s liberal value conversion rules affect its definition of equality, and the == equality operator performs type conversions as described in §3.8.1
* == & ===
* the following array contains five elements, including three undefined elements
	var sparseArray = [1,,,,5];
* A single trailing comma is allowed after the last expression in an array initializer and does not create an undefined element
* properties of objects can be accessed using . identifier OR [ expression ]
* The .identifier syntax is the simpler of the two property access options, but notice that it can only be used when the property you want to access has a name that is a legal identifier, and when you know then name when you write the program. If the property name is a reserved word or includes spaces or punctuation characters, or when it is a number (for arrays), you must use the square bracket notation. Square brackets are also used when the property name is not static but is itself the result of a computation
* in operator on objects & arrays
	var point = { x:1, y:1 }; // Define an object
	"x" in point // => true: object has property named "x"
	"z" in point // => false: object has no "z" property.
	"toString" in point // => true: object inherits toString method
	var data = [7,8,9]; // An array with elements 0, 1, and 2
	"0" in data // => true: array has an element "0"
	1 in data // => true: numbers are converted to strings
	3 in data // => false: no element 3

* The instanceof Operator - The instanceof operator expects a left-side operand that is an object and a right-side operand that identifies a class of objects
	var d = new Date(); // Create a new object with the Date() constructor
	d instanceof Date; // Evaluates to true; d was created with Date()
	d instanceof Object; // Evaluates to true; all objects are instances of Object
	d instanceof Number; // Evaluates to false; d is not a Number object
	var a = [1, 2, 3]; // Create an array with array literal syntax
	a instanceof Array; // Evaluates to true; a is an array
	a instanceof Object; // Evaluates to true; all arrays are objects
	a instanceof RegExp; // Evaluates to false; arrays are not regular expressions
	
* Compound and Empty Statements :-
		compound -
		{
			x = Math.PI;
			cx = Math.cos(x);
			console.log("cos(π) = " + cx);
		}
		There are a few things to note about this statement block. First, it does not end with a semicolon. The primitive statements within the block end in semicolons, but the block itself does not. Second, the lines inside the block are indented relative to the curly braces that enclose them. This is optional, but it makes the code easier to read and understand. Finally, recall that JavaScript does not have block scope and variables declared within a statement block are not private to the block
		
		empty - 
			;

--------------------
Objects -
--------------------

* Categories of JavaScript objects and two types of properties :
	1. A native object is an object or class of objects defined by the ECMAScript specification. Arrays, functions, dates, and regular expressions (for example) are native objects.
	
	2. A host object is an object defined by the host environment (such as a web browser) within which the JavaScript interpreter is embedded. The HTMLElement objects that represent the structure of a web page in client-side JavaScript are host objects. Host objects may also be native objects, as when the host environment defines methods that are normal JavaScript Function objects.
	
	3. A user-defined object is any object created by the execution of JavaScript code.
	
	4. An own property is a property defined directly on an object.
	
	5. An inherited property is a property defined by an object’s prototype object.

* Objects can be created with object literals, with the new keyword, and (in ECMAScript 5) with the Object.create() function

* literals => var obj = {x=10, y=11}
* Using new =>
		var o = new Object()
		var a = new Array()
		var d = new Date()
		var r = new RegExp('js')

* Prototypes -
	* Every JavaScript object has a second JavaScript object (or null, but this is rare) associated with it. This second object is known as a prototype, and the first object inherits properties from the prototype.
	* All objects created by object literals have the same prototype object, and we can refer to this prototype object in JavaScript code as Object.prototype
	* Objects created using the new keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype. So the object created by new Object() inherits from Object.prototype just as the object created by {} does. Similarly, the object created by new Array() uses Array.prototype as its prototype, and the object created by new Date() uses Date.prototype as its prototype.
	* Prototype chain => Object.prototype is one of the rare objects that has no prototype: it does not inherit any properties. Other prototype objects are normal objects that do have a prototype.
	All of the built-in constructors (and most user-defined constructors) have a prototype that inherits from Object.prototype. For example, Date.prototype inherits properties from Object.prototype, so a Date object created by new Date() inherits properties from both Date.prototype and Object.prototype. This linked series of prototype objects is known as a prototype chain.

* Object.create() =>
	* Object.create(), that creates a new object, using its first argument as the prototype of that object. Object.create() also takes an optional second argument that describes the properties of the new object.
		var o1 = Object.create({x:1, y:2}); // o1 inherits properties x and y.
		var o2 = Object.create(null); // o2 inherits no props or methods.
		
		2nd object does not have any prototype, but if you do this, the newly created object will not inherit anything, not even basic methods like toString() (which means it won’t work with the + operator either):
		
		* If you want to create an ordinary empty object (like the object returned by {} or new Object()), pass Object.prototype
			var o3 = Object.create(Object.prototype); // o3 is like {} or new Object().
		
		* The ability to create a new object with an arbitrary prototype (put another way: the ability to create an “heir” for any object) is a powerful one, and we can simulate it in ECMAScript 3 with a function.
			// inherit() returns a newly created object that inherits properties from the
			// prototype object p.
			eg function inherit(p){
				if(p==null) throw TypeError();
				if(Object.create)
					return Object.create(p);
				return null;
			}
			
			* One use for our inherit() function is when you want to guard against unintended (but nonmalicious) modification of an object by a library function that you don’t have control over. Instead of passing the object directly to the function, you can pass an heir. If the function reads properties of the heir, it will see the inherited values. If it sets properties, however, those properties will only affect the heir, not your original object.

* Querying and Setting Properties =>
	* To obtain the value of a property, use the dot (.) or square bracket ([]) operators
	* If using square brackets, the value within the brackets must be an expression that evaluates to a string that contains the desired property name
	* the identifier that follows the dot operator cannot be a reserved word:
		eg o.class OR o.for // assuming class is key in object o, use o['class'] & o['for']
		

* Inheritance =>
	* JavaScript objects have a set of “own properties,” and they also inherit a set of properties from their prototype object.
	* Suppose you query the property x in the object o. If o does not have an own property with that name, the prototype object of o is queried for the property x. If the prototype object does not have an own property by that name, but has a prototype itself, the query is performed on the prototype of the prototype. This continues until the property x is found or until an object with a null prototype is searched. As you can see, the prototype attribute of an object creates a chain or linked list from which properties are inherited.
		var o = {} // o inherits object methods from Object.prototype
		o.x = 1; // and has an own property x.
		var p = inherit(o); // p inherits properties from o and Object.prototype
		p.y = 2; // and has an own property y.
		var q = inherit(p); // q inherits properties from p, o, and Object.prototype
		q.z = 3; // and has an own property z.
		var s = q.toString(); // toString is inherited from Object.prototype
		q.x + q.y // => 3: x and y are inherited from o and p
	
	* Suppose you assign to property x to an object o,
		1. if o already has own(non-inherited) property named x, then the assignment simply changes the values of this existing property.
		2. if o does not have property already, the assignment craetes a new property named x on the object o.
		3. if o already has own(inherited) property x, it still creates a new property and old inherited property will be hidden now. but can still be accessible using o.__proto__...
	* Property assignment examines the prototype chain to determine whether the assignment is allowed. If o inherits a read-only property named x, for example, then the assignment is not allowed. If the assignment is allowed, however, it always creates or sets a property in the original object and never modifies the prototype chain. The fact that inheritance occurs when querying properties but not when setting them is a key feature of JavaScript because it allows us to selectively override inherited properties.
	
	* NOTE : 