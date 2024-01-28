# App calls http.request()
1. app call make a function call by `http.request()`
2. the Node.js framework receives the call and send HTTP request to web server
3. the framework immediately return the status to the call
	1. http.clientRequest object
4. the web server receives the HTTP request and sends a response message back
5. the framework starts a callback function to handle the response and sends it to the app

In the case that the app make the request through a module, the framework will contact the module first, then the module return the status to the app. 

# Sending an HTTP Request
```js
// optional variables claims the host and URL
// US national weather here
let options={
	host:'w1.weather.gov',
	path:'/xml/current_obs/KSFO.xml'
};
// the optional variables are the first parameter
// the second one is a anonymous callback function which takes response as parameter
// this function is called when part of the HTTP resonse message is received
// you can discard the response by left the callback parameter empty
http.request(options,
function(response){
	let buffer = '';
	let result = '';
	// .on() defines an event handler
	// the 1st parameter is the event name
	response.on('data',function(chunk){
		buffer+=chunck;
	});
	response.on('end',function(chunk){
		console.log(buffer);
	});
}).end();
```

```js
let request = http.request(options, function(response{...}));
// error handler
request.on('error', function(e){
	resultCallback(e.message);
});
// .end() completes sending request
request.end()
```

The return of http.request() returns an object of type HTTP.clientRequest
```js
let options={
	hostname:'www.ibm.com',
	port:80,
	method:'POST',
	headers:{
		'Content-Type':'application/x-www-form-urlencoded',
		'Content-Length':data.length
	}
};
let req=http.request(options, function(res){...})
```

# Creating Callback Functions
The first parameter of the callback function is an error object as a convention.

`function(error, param1, param2, ...){...}`

A callback function will check if the first parameter is holding an error object.
- if it is, the callback function will handle the error and clean up any open network or database connections
- if not, the callback function examines the  result from the call

```js
weather.current(location, function(error, tem_f){
	// error check
	if (error){
		console.log(error);
		return;
	}
	// success and print the weather
	console.log(
		"The current weather reading is %s degree.", tem_f
	);
});
// print it in the browser
response.end("... ${tem_f}...")
```
## Pass the Error
```js
// module property
exports.current=function(location,resultCallback){
	// send a request
	http.request(options, function(response){
		let buffer='';
		let result='';
		// string the data chunks into a buffer
		response.on('data', function(chunk){
			buffer += chunk;
		});
		// when it reachs the end, the callback function calls parseString()
		// if it parses an error, you put it into resultCallback()
		// the function calls this function will get this error
		response.on('end', function(){
			parseString(buffer, function(error, result){
				if (error){
					resultCallback(error);
					return;
				}
				// success, error is null
				// pass the result instead of the error
				resultCallback(null, result.current_observation.tem_f(0));
			});
		});
	});
}
```

# Promises
- an object returned by an asynchronous method
- states
	- pending
		- initial state
	- resolved
	- rejected
- uses
	- API requests
	- I/O operations

You can create your own new Promise() object, or use Axios lib

```js
// importing the axios lib
const axios = require('axios').default;
// arrow function: (input) => output
const connectToURL = (url)=>{
	// send a GET request to the input url
	// it will return a Promise that represents the asynchronous operation of making the HTTP request
	const req = axios.get(url);
	// print the pendding request that contains URL, headers, and method
	console.log(req);
	// Promise handler 
	// .then() will be executed if Promise is a resolved
	// it takes the response and print it
	req.then(resp => {
		console.log("Fulfilled")
		console.log(resp.data);
	})
	// .catch() will be executed if Promise is a rejected
	// it takes the error and print "rejected"
	.catch(err =>{
		console.log("rejected")
	});
};
```

# JSON
```js
// create a json string
let json='{"result":true, "count":42}';
// json.parse() parses a json string into a JS object
obj = JSON.parse(json);
console.log(obj.count);
console.log(obj.result);
// json.stringify() converts a JS object into a json string
console.log(JSON.stringify({x:5, y:6}));
```

# Async/Await
```js
const axios = require('axios');

const connectToURL = (url)=>{
	const req = axios.get(url);
	console.log(req);
	// if the promise is resolved
	req.then(resp => {
		// get the data of the response and make it a list
		let listOfEntries = resp.data.entries;
		// print data entries line by line
		listOfEntries.forEach((entry)=>{
			console.log(entry.Category);
		});
	})
	// if the promise is rejected
	.catch(err => {
		console.log(err.toString())
	});
}
console.log("Before connect URL")
connectToURL('https://api.publicapis.org/entries');
console.log("After connect URL")
```
Without Async/Await, the code can be complicated due to the nested .then()

We can do the same thing with Async/Await, and it provides a clean and readable code.
```js
const axios = require('axios');
const connectToURL = async(url)=>{
	const outcome = axios.get(url);
	let listOfEntries = (await outcome).data.entries;
	listOfEntries.forEach((entry)=>{
		console.log(entry.Category);
	});
}

console.log("Before connect URL")
connectToURL('https://api.publicapis.org/entries');
console.log("After connect URL")
```

Here is a better example:
```js
const axios = require('axios');

/*
In the following code we try to get list of all entries from remote url and then based on that make request about`
each of the category. Finally print them all out. We are using axios get, which returns a promise.` 
*/
const connectToURL = (url)=>{
	const req = axios.get(url);
	req.then(resp => {
		let listOfEntries = resp.data.entries;
		return listOfEntries.map((entry)=>{
	         return entry.Category
	         })
     }).then((categories)=>{
	    let Categories = categories.filter(function(item, pos, self) {
	         return self.indexOf(item) == pos;
	     })

         Categories.forEach((category)=>{
             const req = axios.get("https://api.publicapis.org/entries?Category="+category);
             req.then(resp=>{
                 console.log(category+" - "+resp.data.count);
             }).catch(err => {

             })
         });
     })
   .catch(err => {
       console.log(err.toString())
   });
 }
 connectToURL('https://api.publicapis.org/entries');



const axios = require('axios');

/*
In the following code we try to get list of all entries from remote url and then based on that make request about each of the`
category starting with 'A'. Finally print the API counts of the category. We are using axios get, which returns a promise.`
*/
const axios = require('axios');

async function connectToURL(url){
   const resp = await axios.get(url);
   let listOfEntries = resp.data.entries;
   let Categories = listOfEntries.map((entry)=>{
         return entry.Category
   });
   Categories = [...new Set(Categories)];

   Categories.forEach(async (Category)=>{
     if (Category.startsWith("A")) {
             try {
               const resp = await axios({
                 method: 'get',
                 url: "https://api.publicapis.org/entries?Category="+Category,
                 responseType: 'json'
               })
               console.log(Category+"   "+resp.data.count);
             }
             catch(e) {
               console.log(e);
             }
     }
   });
}
connectToURL('https://api.publicapis.org/entries').catch(err => {
   `console.log(err.toString())
});
```

You can only `await` a promise inside an `async` method.
This is because `await` blocks the thread. This will defeat the primary purpose.