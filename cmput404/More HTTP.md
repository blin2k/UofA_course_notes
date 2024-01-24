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
