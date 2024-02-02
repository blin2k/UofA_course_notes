# PUT
- like POST except the URI does not handle the request
	- it is the request
- URI identifies an entity (file, db, entry...)
	- POST URI identifies a service/handler/script/process
- arguments are stored in the URI query string or HTTP headers
	- POST arguments are stored in HTTP request body
- request body contains the entire entity
	- POST body is interpreted by some software and processed
- usage
	- ==create== a new entity at the URI
	- replace an existing entity at the URI
	- add/replace an entry to a DB
	- entity can be retrieved later with GET and the same URI
	- POST:
		- login/logout
		- reply
		- post on a forum/blog
		- upload multiple files somewhere
		- make an order
		- fill out a survey/poll

# DELETE
- like PUT
- args in URI query or HTTP headers
- request body and response body are usually empty
- after DELETE, GET will be responded with a 404

# WEBDAV
- rfc
	- request for comments
- like FTP but for the web
	- let you create and upload to a URI using PUT
	- download from a URI using GET
	- delete using DELETE
	- make directories using HTTP MKCOL
		- MaKe COLlection

---
POST can do both PUT and DELETE, but using the latter two give you more information.

---
# HTTP USER AGENT
- a client/browser
	- chrome / edge / firefox
- mobile device will have a user agent string with the word Mobile

user-agent: mozilla/5.0 (windows nt 10.0; win64; x64) applewebkit/537.36 (khtml, like gecko) chrome/64.0.3282.140 safari/537.36 edge/17.17134
![[Pasted image 20240123195321.png]]

# Status Code
- 1xx
	- informational
		- 100 continue
			- used in multipart and uploads
			- tells the client to send the request body/data
			- the server had a choice to accept the request or not
		- 101 switching protocols (rare)
			- upgrade: header specifies the new protocol
			- protocol switch immediately after the blank line at the end of the header
			- switch from HTTP/1.1 to HTTP/2 on unencrypted connections
				- but browsers don't support HTTP/2 over unencrypted connections
				- so it is basically never used
			- browsers select HTTP/1.1 or HTTP/2 during the TLS handshake for https URLS
				- TLS application-layer protocol negotiation
				- occurs at the same as cipher suite negotiation
				- no additional round-trip latency
				- RFC 7301
- 2xx
	- success
		- 200 ok
		- 201 created
		- 202 accepted
		- 203 non-authoritative (rare)
		- 204 no content
			- 200 but has no body
		- 205 reset content (rare)
		- 206 partial content
			- used to resume downloads
- 3xx
	- redirection
		- 300 multiple choice (rare)
		- 301 moved permanently
			- HTTP to HTTPS
		- 302 found
		- 303 see other
		- 304 not modified
		- 305 use proxy (rare)
		- 307 temporary redirect
			- same like 302
		- 308 permanent redirect
			- same like 301
- 4xx
	- client error
		- 400 bad request
		- 401 unauthorized
		- 402 payment require (rare)
		- 403 forbidden
		- 404 not found
		- 405 method not allowed
		- 406 not acceptable
		- 407 proxy authentication required
		- 408 request time out
		- 409 conflict
		- 410 gone
		- 411 length required
		- 412 precondition failed
		- 413 request entity too large
		- 414 request-URL too long
		- 415 unsupported media type
		- 416 request range not satisfiable
		- 417 expectation failed
		- 418 I'm a teapot
		- 422 unprocessable entity
		- 426 upgrade require
		- 428 precondition required
		- 429 too many requests
		- 431 request header fields too large
		- 451 unavailable for legal reasons
- 5xx
	- server error
		- 500 internal server error
		- 501 not implemented
		- 502 bad gateway
		- 503 service unavailable
		- 504 gateway timeout
		- 505 HTTP version not supported
		- 511 network authentication required

---
# Headers
- headers have an effect on
	- authentication
	- caching
	- encoding
	- partial downloading
	- content type
	- more... 