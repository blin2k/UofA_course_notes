# FTP vs. HTTP
FTP
- 1971
- sending directories
- out of band communications
- heavily relies on TCP
- 2 connections
	- control connection
		- send commands back and forth
	- file connection
- must log in every time

HTTP
- 1991
- sending contents, not files
- responds to requests
	- GET/POST/DELETE/PUT/HEAD
	- single connection
- allow extra information (headers) and arguments (queries) with commands
- default no login, anonymous
- dynamic content
	- can put together contents of things

gopher
- 1991
- sends directories
- limited file types
- hypertext
- death by licensing and adoption while HTTP is free

# Closer Look at HTTP
- hypertext
	- over text
- transport
	- move/sent/receive/communicate
- protocol
	- an agreed-upon method of communication
- accept custom headers
	- allowing extension and new features
- allow more request/command oriented pattern
- relies on URIs to describe resources
	- allow more than one resource to be hosted on one server
- RFC
	- request for comments
	- standard for HTTP

Basics
- TCP
	- port 80
- HTTPS allow encrypted HTTP
	- use port TCP 443
- work over IPv4 and IPv6
- URIs
	- HTTP requests made to addresses

Commands: made to a URI
- GET
	- retrieve information from that URI
- POST
	- run search, login, append data, change data
- HEAD
	- GET without a message body
		- for caching
- PUT
	- store the entity at the URI
- DELETE
	- delete the resource at the URI
- PATCH
	- modify the entity at the URI
- OPTIONS

# URIs
- universal resource identifier
	- identifies a resource by pointing to it
- most URIs are URLs
	- uniform resource locator
	- tells you how to get to a resource
	- http://ualberta.ca/
- some are URNs
	- uniform resource name
	- tells you the unique name or number given to a resource by some body like IETF
	- urn:letf:rfc:3986

# URLs
- scheme
	- common
		- http/https/mailto/file/data
	- older
		- ftp/gopher/irc
	- new
		- spotify:track:35zrlBOjpfDPMcZzglWOuv
- everything else

URL HTTP scheme
- scheme
- :
- authority
	- username:password@
		- optional
	- hostname
	- :port
		- optional
- path
	- /path/to/destination
- ?query
	- optional
- \#argument
	- what part of a resource we want to go to
	- optional

https://duckduckgo.com/?key1=value1&key2=value2#/9
- scheme
	- https
- authority
	- duckduckgo.com
	- host
- path
	- NA
- query
	- key1=value1
	- key2=value2
- argument
	- 9

# Absolute And Relative URLs
- http://[::1]:800/images/web-server.svg
	- absolute authority
	- absolute path
- http://[::1]:800/images/../index.html
	- absolute authority
	- relative path
- /images/web-server.svg
	- implied authority
	- absolute path
	- this would take you to somewhere start from the same authority
- images/web-server.svg
	- implied authority
	- relative path
	- this would take you to somewhere inside the same directory

# Encoding
For characters that are not in
- .
- -
- _
- ~
- 0-9
- a-z
- A-Z
We use % encoding to avoid abusing function signs like / ? # :
- RFC 3986
	- %20 is a space
		- according to ascii code
	- %e2%98%83 is a snowman emoji
- punycode encoding
	- for domain name
		- http://xn--n3h.net/
			- xn--n3h represents the same snowman emoji

GET /relative/path 
- 301 Moved Permanently
	- what you want is not here anymore
	- but you can find a redirect link in the header
		- Location: /new/path
	- the browser will bring you there automatically
- 200 OK
	- everything went fine

# HTTP GET
- a simple request to be sent to the resource
	- dynamic
		- the server generates the resource when request is received
	- static
		- the server sent the file already there
- we can send query parameters along an HTTP get in the URL
- it is considered ==bad== if GET request ==causes the server to change data==

# HTTP POST
- a request to
	- update
	- create
	- generally interact with URL
- used to submit HTML forms
- is expected to add or mutate data
- URL-encoded parameters
	- percent-encoded
		- or RFC 2388's format
			- multipart/form-data
	- parameters are usually send in POST body as
		- application/x-www-form-urlencoded
- `<input name="occupation">` 
	- `name` matches the key
	- occupation=
	- the content of the input element becomes the value
# HTTP 2
- 2015
	- 24 years after HTTP
- based on proposed SPDY protocol by Google
	- designed to ==reduce latency==
- only supported over TLS
	- HTTPS
- binary protocol
	- not viewable/debuggable/writable in plain text
	- compress headers for ==less bandwidth==
- pipelining
	- request request .... response response
- multiplexing

# HTTP 3
- 2022
	- 7 years after HTTP 2
- get webpages loaded ==faster==
- TCP stopped multiplexed streams if a packet went missing
- TCP handshake before TLS handshake
- run over QUIC inside of UDP packets

# QUIC
- quick UDP internet connections
- same guarantees that TCP provides
	- nickname: TCP 2
- ==lower latency== than TCP
- multiple streams
	- TCP only provides one
	- avoid using multiple TCP connections to a single server
		- reduce high-latency TCP handshapes
		- reduce high-CPU TLS handshakes
- integrates with TLS 1.3
- requests and responses in both directions happening at the same time
	- data is interleaved
	- no need for pipelining
- request and responses can be prioritized