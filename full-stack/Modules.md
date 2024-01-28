- Every JavaScript file is a module in Node.js
- A package consists of one or more modules
	- Every package has a package.json file that describe details about a Node.js module
		- the module manifest
	- If the package does not have a package.json file, Node.js assume the main class' name is ==index.js==

To specify a different main script for your module, specify a ==relative path== to the Node.js script ==from the module directory==
```json
{"name": "mod_today",
 "version": "1.0.0",
 "main": "./lib/today",
 "license": "Apache-2.0"
}
```
- The 'main' field lists a path to the main node.js script

---
# Importing Node.js modules
- use `require()`
	- `let today=require('./today')`
		- assume the script has a file extension of .js
			- today.js
- to import a Node.js module that consists of a ==single== script,
	- use `require()` with a relative path to the script file
		- today.js -> hello.js
		- `require('./today')`
- to import a Node.js module that is ==packaged in a subdirectory==, 
	- use `require()` with the name of the subdirectory
		- /mod_today/index.js -> hello.js
		- `require('./mode_today')`

When Node.js is looking for the required module, it assumes the input is a path to a script. If there is no script fits the name, it takes it as a subdirectory. 

Remember the default manifest is index.js

---
# Export Functions and Properties
```js
let date = new Date();
let days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
// make the function available to Node.js apps that import this module 
// as a property
exports.dayOfWeek = function(){
	return days[date.getDay()-1];
};
```
# Accessing Exported Properties
```js
// import the module
let today = require('./moduleName');
// use the property of the module
let dayOfWeek = today.dayOfWeek();
console.log("Happy %s!", dayOfWeek);
```
