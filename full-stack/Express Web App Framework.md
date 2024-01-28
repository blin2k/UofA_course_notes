There are many downsides of manual parsing XML 
- string matching ignores the structure of XML data
- the message body might contain malformed XML data
- depending on the complexity of the XML data, string matching might be more efficient than building an XML tree of the data
- string matching is less tolerant to changes in the XML data structure
- if the message adds or removes any XML elements, you must change the regular expression on the string match function

Third-party packages are a nice choice
- xml2js Node.js package parses a string of XML elements into a JS object
- unlike other XML parsing Node.js packages, xml2js uses only JS
- it does not require an XML parsing library that is written in another language
- third-party packages might have a different software license than the Node.js framework
- confirm that the licensing terms work with your company and your application before installing the package

You can use `npm` application manages Node.js packages in your Node framework installation
- `npm install xml2js`
- Node Package Manager
```js
// import
let parseString = require('xml2js').parseString;
// set a export property
exports.current = function(location, resultCallback){
	...
	// send a request
	let request = https.request(options, function(response){
		...
		// when the response is end
		response.on('end', function(){
			// parse the string
			// this function takes two params
			// the 1st one is the XML string
			// the 2nd one is a handler function
			parseString(buffer, function(error, result){
				if (error){
					console.log(error);
					return;
				}
				console.log(result);
			});
		});
	});
}
```

```js
// the xml string look like this
const xml2js = require('xml2js');

const xmlString = `
  <bookstore>
    <book>
      <title>Harry Potter</title>
      <author>J.K. Rowling</author>
    </book>
    <book>
      <title>The Hobbit</title>
      <author>J.R.R. Tolkien</author>
    </book>
  </bookstore>
`;

xml2js.parseString(xmlString, (err, result) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(result);
});



// the console print would be this
{
  bookstore: {
    book: [
      { title: ['Harry Potter'], author: ['J.K. Rowling'] },
      { title: ['The Hobbit'], author: ['J.R.R. Tolkien'] }
    ]
  }
}

```

# Express framework
Express is a third-party module that provides a framework for building web apps.
- based on Node.js runtime environment
- abstracts low-level details
- purposes
	- as an API
		- `res.json()`
			- notifies the client of the content type being sent
			- stringify data
	- setup templates with server-side rendering (SSR)
		- `res.render()`

## How Express Works
1. declare Express as a dependency in the package manifest of a Node.js project
	1. create a package.json file in your project folder
	2. it stores information about the contents of a Node.js module
		1. name
			1. `"name": "temperature"`
		2. version
			1. `"version": "1.0.0"`
		3. description
			1. `"description": "Retrieve current weather conditions in the US"`
		4. main
			1. `"main": "app.js"`
		5. dependencies
			1. `"dependencies": {"express": "4.x"}`
2. run the `npm` command to download any missing modules
	1. `npm install` inside the Node.js module directory to download Express
	2. `npm install <module_name>`
3. import the Express module and create an Express application
	1. `let express=require('express');`
	2. `let app = express();`
4. create a new route handler
 ```js
 // handler for GET request
 app.get('/temperature/:location_code', function(request, response){
	 let location = request.params.location_code;
	 weather.current(location, function(error, tem_f){
		 ...
	 });
 });
 ```
5. start an HTTP server on a given port number
```js
let server = app.listen(port, function(){
	console.log('Listening on URL http://localhost: ${port}');
})
```

# Routing, Middleware, and Templating
## Routing
- GET / POST / PUT / DELETE
- can be handled at app level or router level
app level
```js
const express = require('express');
const app = new express();
app.get("user/about/:id", (req, res)=>{
	res.send("Response about user"+req.params.id)
})
app.get("item/about/:id", (req, res)=>{
	res.send("Response about item"+req.params.id)
})
app.listen(3333, ()=>{
	console.log('Listening at http://localhost:3333')
})
```
Router level
```js
const express = require('express');
const app = new express();
let userRouter = express.Router()
let itemRouter = express.Router()
app.use("/item", itemRouter)
app.use("/user", userRouter)
userRouter.get("/about/:id", (req, res)=>{
	res.send("Response about user"+req.params.id)
})
itemRouter.get("/about/:id", (req, res)=>{
	res.send("Response about item"+req.params.id)
})
app.listen(3333, ()=>{
	console.log('Listening at http://localhost:3333')
})
```

When there are many routes to handle, code maintenance is better with routers.

## Middleware
- functions that have access to the request and response objects and the next function
- can be chained
- categorized based on purpose, use, and source
- useful to parse requests, add authentication, handle errors, and other common activities
- types
	- app level
	- router level
	- error-handling
	- built-in
	- third-party

app level
```js
// bound to app.use()
app.use(function(req, res, next){
	if (req.query.password !== "pwd123"){
		return res.status(402).send("This user cannot login")
	}
	console.log('Time:', Date.now())
	next()
})
```

router level
```js
// bound to router.use()
let userRouter = express.Router()
userRouter.use(function(req, res, next){
	console.log('User query time:', Date());
	next();
})
// bound the router with the app
app.use('/user', userRouter)
```

error-handling
```js
// app.use() or router.use()
app.use(function(err, req, res, next){
	if (err != null){
		res.status(500).send(err.toString())
	}
	else{
		next();
	}
})
```

built-in
- static files, cookie parser, JSON
```js
app.use(express.static('cad220_staticfiles))
```

third-party
- open source, user defined
```js
function myLogger(req, res, next){
	req.timeReceived = Date();
	next();
}
app.use(myLogger)
```

template rendering
- rendering dynamic content
```js
app.set('view engine', 'jsx');
app.set('views', 'myviews');
app.engine('jsx', jsxEngine);
app.git("/:name", (req, res)=>{
	res.render('index', {name:req.params.name});
});
```