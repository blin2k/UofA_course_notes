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
