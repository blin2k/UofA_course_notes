```js
// create a server
// the function will be invoked whenever a request is received
var server = http.createServer(function(request, response)){
	// the content of the response
	var body = "Hello world!";
	// header
	// status: 200 OK
	response.writeHead(200, {
		// header content
		'Content-Length': body.length,
		'Content-Type': 'text/plain'
	});
	// after the header is written, write the body
	response.end(body);
};
// make the server listen to port 8080
server.listen(8080);
```
