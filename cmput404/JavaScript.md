# JS in HTML

With a `<script>` tag, you can write JS in HTML.
```html
<script>
	var someJS = "js in html";
</script>
```

Or embed onliners within HTML
```html
<button onClick="alert("help");"> test </button>
```

Using separated JS file, you need the URL
```html
<script src="path/to/script.js"></script>
```
The content file should have `'use strict';` at the top
```html
'use strict';

var someJS = "js in html";
```

# Functions
- return
- parameters
- access all available scope
	- closures

## Anonymous Functions
```js
// normal
function one(){
	return 1;
}

// anonymous
const two = function(){
	return 2;
}

// arrow
const three = ()=>{return 3;}
```
In the two anonymous cases, you are assign a name to the function.
- `two()` will give you a `2`
## Closure
	Functions in functions can see the outer function's variables from when the function was defined. 

```js
// The outer function defines the inner function and then return it
function outer(text){
	// The point is, the inner function can access the parameter of the outer function
	// itn't it amazing?
	function inner(x){
		alert(text);
	}
	return inner;
}

// it just do the definition, thus nothing is printed
f = outer("hi");
// 1 is the parameter for the inner function
// it does nothing but triger the function
// the entire thing do the alert, which prints the outer text
f(1);
// you can also do this
outer("hi")(1);
```

# Scope
By default, a variable is global.
```js
function f(){
	a = "secret";
}
f();
console.log(a); // this can also access what is defined in the function
```

How to make it local?
- `'use strict';`
- `let`
	- scopes the enclosing block
- `const`
	- scopes the enclosing block
	- constant that you cannot change
- `var`
	- scopes the enclosing function

## enclosing block V.S. enclosing function
Enclosing block means the curly bracket which is not necessarily for a function, but also things like `if` statement and `for` statement.

```js
function f(){
	let a=1;
	for (let i=1; i<10; i++){
		var c = i;
		let b = i;
	}
	console.log(c); // gives 9 because c scopes the whole function
	console.log(b); // gives an error because b scopes within the for loop only
}
```

# THIS
`this` in JS is similar to `self` in python

but python is early binding
- bind when declare
JS is late binding
- bind when function called

```js
class MyClass{
	write(){
		console.log(this);
	}
}
// this is not bound yet until function called
i = new MyClass();
// thus there is nothing before the period
x = i.write;

// this will not work
// when the function is called, write() is not bound to MyClass yet
x();

// this will work
i.write; // binding
x.call(i); // .call() change the meaning of this in the parent function
x();

// or this
x.bind(i); // binding
x(); 
```

`.call()` changes the meaning of `this` in the parent function
```js
var outer = function(){
	console.log("printing: " + this);
}
outer(); // printing: [object global]
outer.call("replacement"); // printing: replacement
```
# Arrow Function
```js
class MyClass{
	constructor(){
		this.state = 1;
	}
	getIncrementer(){
		return function(){
			this.state += 1;
		}
	}

	getIncrementer2(){
		return ()=>{
			this.state += 1; // arrow function is not declaring a new function, so no overwritten to this 
		}
	}
}

var i = new MyClass();
var f = i.getIncrementer();
f(); // i is not bound, so this is undefined
```

# Numbers
	Everything is a double. 

# Booleans
false value
- false
- null
- undefined
- ''
	- empty string
- 0
- NaN

All other things are true.

# Equality
Check the comparison table, it is WILD.

`==` is so bad, but `===` is better.
However, lists, objects, list of something, NaN are not equal to themselves.
- to check if something is a Nan, use `isNaN()`
	- NaN never equals itself in any language

# Arrays
`var arr = [1,2,3,'4];`
`arr.length === 4;`
`arr.splice(3,1, 'new')`
- start from index 3
- delete 1 element
- insert 'new'

`var arr = new Array(10);`
`arr[0] === undefined;`
`arr[0] = 'assigned`;
`'assigned' === arr[0];`

Array is not bounded in JS. Elements out of the max index you define has a value `undefined`

Loop over arrays with `for ... of`
```js
let arr = [1,2,3];
for (let i of arr){
...
}
```

# Objects
- Everything ==except Booleans, numbers, and strings==, is an object.
- objects don't have a class
- pass by reference
- work like `dict()` in Python
```js
var empty = {};
var me = {
	"name": "BL",
	"job": "student",
	"age": 23,
	"sayName": function(){
		alert(this.name);
	},
};
me.age === 23;
me["name"] === "BL";
me.name === "BL";

keys(me) === ["name", "job", "age"];

// Prototypes
var child = Object.create(me);
keys(child) === [];
child.name === "BL";
```

Not like arrays, looping over properties of an object uses `for...in`
```js
for (let property in me){
	alert(property + ":" + me[property]);
}
```
print out the property's name and the output

# Classes
- JS has several ways of creating "classes"
- ECMAScript 2015 classes
- constructor functions
```js
class Pokemon{
	constructor(name, level){
		this.name = name;
		this.level = level;
	}
	levelUp(){
		this.level += 1;
	}
}
pika = new Pokemon("Pika", 1);
pika.levelUp();
pika["name"] === "Pika";
// pika.name
```

2022 classes
```js
// inheritance
class Something extends Superthing{
	// static thing
	static count = 0;
	constructor(param){
		super(param);
		// private thing
		this.#private = Math.random();
	}
	static someMethod(){
	}
	#privateMethod(){
	}
}
```

constructor function
- before 2014 we have no classes
```js
function Pokemon(name, level){
	this.name = name;
	this.level = level
}

Pokemon.prototype.levelUp = function(){
	this.level += 1;
}

Pika = new Pokemon("Pika", 1);
Pika.levelUp();
```

Prototype properties are add-on, they are not properties of the original model. If you do `JSON.stringify()` to the original model, the original properties will be printed, but nothing will be printed if you do it to a prototype.

`Object.create(prototype)`
- awkward and rarely used

# Manipulating The DOM
Document Object Model

- DOM from HTML
```html
<p>some text<\p>
<div>
	another text
	<a href="https://google.ca">link</a>
<\div>
```

Top of the DOM
- document
	- root element: HTML(document.children\[0])
		- element: head(document.children\[0].children\[0])
		- element: body(document.children\[0].children\[1])
			- element: p(document.children\[0].children\[1].children\[0])
				- text: some text
			- element: div(document.children\[0].children\[1].children\[1])
				- text: another text
				- element: a; attribute href
					- text: link

```js
function domRecurse(start, depth){
	var out = "";
	for (child of start.childNodes){
		indent = "    ".repeat(depth);
		out += indent + "* " + child.nodeName;
		if (child.nodeName === "#text"){
			out += " " + JSON.stringify(child.wholeText);
		}
		out += "\n";
		out += domRecurse(child, depth+1);
	}
	return out;
}
```

# Queryselector
```js
function domRecurseExample2(){
	var start = document.querySelector("#domexample2");
	alert(domRecurse(start, 0));
}
```

```html
<p id="domexample2">target<\p>
<button type="button" onclick="domRecurseExample2()">Try it<\button>
```

- jump straight to an element
- use CSS-style selector
- you don't need jQuery

hash`#` means ID in CSS

# Finding DOM Elements
Other than querySelector
- `document.getElementsByTagName("div")`
- `document.getElementsByClassName("divider")`
- `document.getElementById("main")`
- `document.getElementsByName("up")`

# jQuery
Available form APIs built-in to browsers

# Changing Document Content
```js
function fillExample(){
	fillme = document.getElementById("fillme");
	fillme.textContent = "what ever i want";
	a = document.createElement("a");
	a.textContent = "make a link";
	a.href = "https://google.ca/";
	fillme.appendChild(a);
}
```

# Changing Document Style
```js
// find and reset
function styleExaple(){
	var divs = document.getElementsByClassName("styleme");
	divs = Array.prototype.slice.call(divs);
	divs.map(
		(div)=>{
			console.log(div);
			div.style.border = "5px solid";
			// rbg(redDeg, greenDeg, BlueDeg)
			div.style.borderColor = "rgb(" + (256*Math.random()) +
				", " + (256*Math.random()) +
				", " + (256*Math.random()) + ");"
		};
	)
}
// injection
function styleExaple2(){
	old = document.getElementsByClassName("styleme");
	if (old){
		old.parentNode.removeChild(old);
	}
	var css = "div.styleme2{ border: 5px solid " +
		"rgb(" + (256*Math.random()) +
		", " + (256*Math.random()) +
		", " + (256*Math.random()) + ");}"
	style = document.createElement('style');
	style.type = "text/css";
	style.id = "styleme2sheet";
	style.textContent = css;
	document.head.appendChild(style);
}
```

