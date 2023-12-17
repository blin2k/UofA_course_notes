# Intro
Shared memory and files allow communication between processes/threads on the same machine.

How to communicate between machines?
- send information
	- data
	- data structure
	- signals
using message passing

# Network Code
Use sockets as the internal endpoint for network transmission
- analogous to an electrical connector

# Usage
- parallel applications
	- multiple processes on multiple machines
		- each contributing to performing a computation
	- message passing interface (MPI)
- network devices
	- printers
	- scanners
	- file servers on local network
- internet
	- sending/receiving data from remote sites
	- world wide web
	- search engines
	- ecommerce

# Messages
Each machine has an address,
- content -> letter
- router -> post office
- network -> delivery bus

# IP Address
Every machine is given an Internet Protocol Address and a symbolic name
- ccid.cs.ualberta.ca
- 129.128.243.70
	- four fields
	- 3 networks id
	- 1 host id

Principal functions
- identifies the host
	- the network interface
- provides the location of the host in the network
	- the capability of establishing a path to the host

IPv4
- 32 bit address
IPv6
- 128 bit address

Internet Service Provider (ISP)
- maintain its own local IP address
- all internet traffic goes through the ISP who translates external addresses to internal ones
![[Pasted image 20231215024238.png]]

# Behind the Scenes
TCP: Transmission Control Protocol
IP: Internet Protocol
![[Pasted image 20231215024737.png]]

![[Pasted image 20231215030016.png]]

# Overview
![[Pasted image 20231215030204.png]]
![[Pasted image 20231215030210.png]]

# Socket()
```c
int listenfd;

if((listenfd = socket(AF_INET, SOCK_STREAM, 0)) < 0){
	perror("socket");
	exit(-1);
}
```

AF_INET: use the address family for the internet

# Ports
IP address provides the address to send to the message to.
The port number is the mailbox at that address.

# Bind()
```c
struct sockaddr_in serv_addr;

serv_addr.sin_family = AF_INET;
# htons/htonl convert values between host byte order and net work byte order
serv_addr.sin_addr.s_addr = htonl(INADDR_ANY);
serv_addr.sin_port = htons(8888);

if (bind(listenfd, (struct sockaddr*) &serv_addr, sizeof(serv_addr)) < 0){
	perror("bind");
	exit(-1);
}
```

# Listen()

```c
if (listen(listenfd, 10) < 0){
	perror("listen");
	exit(-1);
}
```

# Accept()

```c
if((confd = accept(listenfd, &clnt_addr, &clnt_len)) < 0){
	perror("accept");
	exit(-1);
}
```

confd: "file" descriptor for the connection
clnt: who made the connect
- client

# Read() / Write()
socket IO is just like file IO
```c
if (read(connfd, &msg, sizeof(msg)) != sizeof(msg)){
	perror("read");
	exit(-1);
}

if (write(connfd, &msg, sizeof(msg)) != sizeof(msg)){
	perror("write");
	exit(-1);
}
```

# Sockets == Files
Convert a socket into a file descriptor

```c
FILE *fin, *fout;
fin = fdopen(socket, "r");
fout = fdopen(socket, "w");

fscanf(fin, "%30s%d", &name, &age);
fprintf(fout, "Hello to %s age %d\n", name, age);
```

# Close()
`close(connfd)`

`shutdown(connfd, how)`
how: disallow sending any more messages, receiving any more messages, or both

# Client
```c
connfd = socket(AF_INET, SOCKET_STREAM, 0);
serv_addr.sin_addr.s_addr = inet_addr("127.0.0.1");
serv_addr.sin_family = AF_INET;
serv_addr.sin_port = htons(8888);

if (connect(connfd, (struct sockaddr*) &serv_addr, sizeof(serv_addr)) < 0){
	perror("connect");
	return 1;
}
read() / write()
close() / shutdown()
```

# Protocol
The client and the server should have the same protocol.