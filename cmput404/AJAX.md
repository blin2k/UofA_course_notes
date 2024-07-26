Asynchronous JavaScript and XML
- allow JS to make HTTP requests and use the results without redirecting the browser
- enable heavy-clients and lightweight webservices
- can be used to avoid presentation responsibility on the webservice
- JSON is a common replacement for XML
- modern social media is heavy on AJAX

Disadvantages
- you have to manage history, back button, bookmarks in JS
- security
	- browsers heavily restrict AJAX to prevent abuse
		- same-origin policy
- even more HTTP requests, CPU and RAM

	AJAX let the client do the job instead of the server.

# Making Requests
- old
	- `new XMLHttpRequest()`
- modern
	- fetch API
	- `new Request("some-url")`
	- promises

```js
// final position
var img = document.querySelector("img#fetchexaple");
// where it is
var request = new Request("../images/target.gif");
var promise1 = fetch(request);
// after fetch the gif, make it a binary data
var promise2 = promise1.then(function(response){
	console.log("Got headers");
	// BLOB = Binary Large OBject
	return response.blob(); // return a promise for raw binary data
});
// after having the binary data, put it to the final position
promise2.then(function(blob){
	console.log("Got data blob");
	var objectURL = URL.createObjectURL(blob);
	img.src = objectURL;
});
```

# Promises
```js
// return a promise object after the task is done
function makePromise(data){
	return new Promise((resolve, reject)=>{
		// resolve() pass the argument to the next promise
		// reject() deal with another case
		resolve(data);
	});
}
function promiseExample(){
	// resolve X, then return a promise
	var promise1 = makePromise("X");
	// after X is resolved, create a new promise after alerting data2
	// data2 is the result of the last promise's task, which is the resolved X
	var promise2 = promise1.then((data2)=>{
		alert("data2:" + data2);
		return "Y";
	});
	// after the alert, take Y and alert it
	var promise3 = promise2.then((data3)=>{
		alert("data3:" + data3);
	});
}
```

A promise will return a promise.
`.then()` will return a promise as well
- the argument of the function inside `.then()` is the result of the task of the last promise

# Promise Dot-Chaining
```js
var request = new Request("images/img.gif");
var promise1 = fetch(request);
var promise2 = promise1.then(function(response){
	console.log("got headers");
	return response.blob();
});
promise2.then(function(blob){
	console.log("got data blob");
	var objectURl = URL.createObjectURL(blob);
	img.src = objectURL;
});

// same as below
fetch(request).then(function(response){
	// return blob
}).then(function(blob){
	//stuck it in
})
```

# Fetching JSON
```js
function fetchJSON(url){
	var req = new Request(url);
	return fetch(request).then((res)=>{
		if (res.status === 200){
			retuurn res.json();
		}
		else{
			alert("error" + res.status);
		}
	});
}

var getterID
function stattGetting(){
	getterID = window.setInterval(()=>{
		var now = new Date();
		var s = 1 + (now.getSeconds()%4); // remainder
		var url = s + ".json"; // 1.json 2.json ...
		// after the json is fetched, replace it into #ajaxy 
		fetchJSON(url).then((json)=>{
			console.log(json);
			text = json.message;
			document.querySelector("#ajaxy").innerText = text;
		});
	}, 1000); // .setInterval(..., 1000): repeat every 1000ms
}
function stopGetting(){
	window.clearInterval(getterID);
}
```

# Timers
`window.setInterval` lets you run a function every so many ms
`window.setTimeout` lets you run a function once after so many ms

# JSON
- JavaScript Object Notation
- strict subset of JS
- `JSON.parse` parses JSON text into an Object
- `JSON.stringify` turns an Object into JSON

`JSON.down` and `JSON.load` in Python

# ASYNC And AWAIT
- `async`
	- return a promise
- `await`
	- in a `async`
	- blocks code execution
		- stop and wait for the promise to resolve

```js
var getterID;
async function get2(){
	var now = new Date();
	var s = 1 + (now.getSeconds()%4);
	var url = "../" + s + ".json";
	var json = await fetchJSON(url);  
}
```

Disadvantages
- execution stops at `await`, instead of continuing in parallel
- with `.then()` in a loop, the loop completes instantly and each callback function can run in parallel as soon as its ready
- with `await` in a loop, the loop will keep stopping each time it gets to the `await`

# Function Passed To `then` Can Return a Promise
```js
const promise2 = promise1.then((value)=>{
	console.log(value);
	return new Promise((resolve,reject)=>{
		window.setTimeout(()=>{
			console.log("time out");
			resolve(777);
		}, 2000);
	});
});
```