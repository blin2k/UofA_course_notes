We use web to
- information
	- request
	- search
	- navigate
	- share
- software
	- access
	- operate

## Ethernet
- the protocol runs over the wire or WIFI
- the packet of ethernet is called frame, 64 to 1526 bytes 
	- preamble 7
	- SFD 1
		- start frame delimiter
	- Destination 6
	- Source 6
	- Length 2
	- Payload 46-1500
		- keep your message sizes smaller than 1.5kb to ensure you stay inside of packets
		- sending 1 byte, incurs many headers
	- CRC 4
		- error detection
- it can only connect computers on the same network
	- the size is way smaller than internet

# IPv4
Internet is the network of networks
- routable
- IP was a compromise to address computers
- was put into the ethernet payload
- stateless
- backbone of the internet
- over large distance
- connecting many computers
- ran out of IPv4 addresses

## Header
![[Pasted image 20240118110724.png]]
- at least 128 bits = 16 bytes
	- the maximum amount of data can be sent is 1500 - 16 = 1484 bytes
- at most 32 bytes

# IPv6
- more address space
	- 128 bits (16 bytes) instead of 32 (4 bytes)
- not compatible with IPv4
- surrounded in brackets and square brackets
	- https:// \[2001:db8::1\]:443
	- easier to parse
- ![[Pasted image 20240118112242.png]]
- 128x2 +32x2 == 320 bits == 40 bytes
	- the maximum amount of data can be sent is 1500 - 40 = 1460 bytes

# Routers
==Ethernet allows us to network within a single network, like a campus or a house. The internet is the network of networks. It is passed along IP packets from ethernet network to ethernet network.==

==The router receives something sent by your computer that needs to go to the internet. It takes the IP packet out of the ethernet packet, make a new Ethernet packet, put it back in, then sent it over the cable link or fiber optic link or DSL link.==

# UDP
- user datagram protocol
	- user-space applications can use it
	- checksums
		- integrity
	- port numbers
	- stateless
	- lossy, not ordered
		- sent: 0 1 2 3 4 5 6 7 8 9
		- received: 0 1 2 4 3 5 6 9
	- no connections
	- no guarantees
- simple and basic
- ![[Pasted image 20240118211850.png]]
- UDP is inside an IP packet which is inside an Ethernet packet
- the maximum data size loses 32 bits == 8 bytes
	- using IPv6, 1500 - 40 - 8 = 1452 bytes

# DNS
- domain name service
- turn the name of a computer into numerical IP address
	- google.com -> IPv4/IPv6
- inside IP packet

# TCP
- transmission control protocol
- inside IP packet
- UDP sends basic messages, TCP got some fancy features
	- connection
		- if a packet goes missing in the middle of a conversation between two computers, TCP is responsible to request a copy of the thing went missing
	- order
		- not like UDP
		- receive in order that they were sent
	- guarantee
	- ![[Pasted image 20240119191141.png]]
	- 20 bytes

# Firewalls
- prevent communications

I want to go to slashdot.org
- python requests tell the OS to connect to slashdot.org via TCP on port 80
- OS have no idea what slashdot.org is
	- needs to contact a nameserver
- OS sends a UDP packet to the name server on port 53
	- UDP inside IP inside Ethernet
- cable modem accepts the packet through Ethernet
- cable modem contacts Shaw's DNS server behalf of my computer
- DNS server receives my query but doesn't know slashdot.org
	- asks a more authoritative server
		- sent DNS request 
			- over UDP over IP over Ethernet
			- to datacenter -> edge router
				- edge router to the root DNS server over internet, asking about org
		- gets a DNS response indicating the address of the org server
		- sends a DNS request to the org server
			- asking for the SOA of slashdot.org
				- start of authority
		- gets a DNS response indicating the DNS server knows about slashdot.org
		- sends a DNS request to the authoritative server for slashdot.org
		- gets a response back on UDP port containing a record listing an IP of slashdot.org
- DNS server makes a DNS response packet
- DNS server sends the packet to me over UDP over IP over Ethernet
- over private network back to my cable modem back to my computer over Ethernet IP UDP
- OS receives the DNS response recording IP address
- OS initiates a TCP connection to port 80 of slashdot.org IP
- OS sends a TCP SYN packet to slashdot.org IP at port 80 over IP over Ethernet to the cable modem through Shaw and internet to slashdot's dataserver
	- copy appears on some ethernet cable
- datacenter sends a TCP SYN+ACK packet back
	- IP -> ethernet -> network -> internet -> network -> cable modem -> ethernet -> IP -> my computer
- OS sends a TCP ACK packet to datacenter
- connection is established
	- OS and datacenter send data packets across TCP connection
- webserver waits on the connection and reading bytes from the connection after the packet is delivered
- webserver's TCP layers sends a TCP ACK packet back to my IP address
	- acknowledging the receipt of the packet that contained the GET request I sent
- webserver sends an HTTP response which is over 40 kb, broken up across 29 packets
	- each packet is sized in 1500 (payloads)- 40 (ip header) - 20 (tcp header)
	- all of them needs to be acknowledged by my computer

![[Pasted image 20240119201313.png]]