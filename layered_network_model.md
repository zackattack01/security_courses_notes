# Link
- shared network infrastructure focuses only on packets

## Layered Network Model: Overview
- allows designing a network to be broken into more manageable sub problems
- TCP/IP "internet protocol suite" is the best known example of this
- ties together
```
   |Application Layer |       |Transport Layer (TCP)|  |Internetwork Layer (IP)|   |Link Layer (Ethernet, WiFi) |
            ↓                           ↓                          ↓                              ↓
|web, email, file transfer|   |reliable connections |    |simple, unreliable |         |physical connections | 
```

- more details about the internet suite [here](https://en.wikipedia.org/wiki/Internet_protocol_suite)

## Link Layer

- connection out of one computer
- can be wire, wireless, fiber optic, etc
- each link is one step in the path
- Common link techs include
  - ethernet
  - WiFi
  - Cable Modem
  - DSL
  - Satellite
  - Optical

#### Ethernet
- invented at PARC
- first local area network
- connected PC's to laser printers
- Inspired by Aloha (an earlier wireless network)
- Bob Metcalfe (one of the inventors of ethernet)
- WiFi is a variation of ethernet

## Internetwork Layer (IP)
- Worries about all of the links, and the sequence to be followed to get from one place to another
- Its goal is to get your data from one computer to another
- Each router knows about nearby routers
- IP puts its best effort in but it is okay to drop data if things go bad

#### IP Adresses
- The IP address is the number which is associated with a particular workstation or server
- Format:
  - prefix of the address is "which network"
  - while the data is traversing the internet all that matters is the network number (first two groups)
- NAT network address translation: your address is changed as packets leave and reenter your local machine
  - so while you're at starbucks your packets know to come back to starbucks and once there they know to go back to you
  - if an IP traces to 192.168 it means it was close/in the server radius
- TTL field- this is changed by each router, decremented and when it hits zero the packet is thrown away
- traceroute sends a series of packets with incrementing TTL's, so they get rejected and sent back one step after the next
- IP cant guarantee delivery, tries to pick best path but doesn't try to do too much

## Transport Protocol (TCP)
- Built on top of IP
- Assumes IP might lose some data
- Keeps a copy of the data until it gets an acknowledgement from the other side, if it doesn't it can send the data again and again
- TCP will send a few packets and will send more as receiver informs them that they've received the packets
- The sender's machine can be held responsible for holding its own copies of the message
- Van Jacobson's Slow Start Algorithm
  - TCP/IP was 'breaking', people across the country were complaining about the speed (10 kb/s)
  - As bandwidth for packets was reduced, time needed to increase
  - Needed to reach a steady state, but this wasn't occurring at the start of a packet transfer
  - Slow start algorithm started up the transfer gradually, which allowed transfers to reach a steady state from the beginning
  - Development and testing of the algorithm took about a month

### Domain name system 
- can be thought of as laying in between internet and link or transport
- add on for user friendly names
- IP addresses reflect technical geography
- read left to right
- domain names reflect organizational structure
- domain names read right to left (from less to more specific)

## Application Layer
- Can now trust that TCP will give us realiable data transfer
- www protocol httpd is the protocol that's the most popular, but there's also mail, file transfer, etc
- There are two basic questions-
  - Who gets the data? Ports (see below)
  - What are the rules for talking with that application? (Protocols)

#### Ports
- like an extension in a telephone number (IP address then port number)
- these are generally used for things like
  - Incoming email: 25
  - login: 23
  - web server: 443 (https) or 80 (http)
  - personal mail box: 109 or 110

#### Application Protocol
- rules for conversation across that port
- HTTP Request/Response cycle. click, request, response, display
- if you're requesting it should be something like METHOD_NAME url HTTP_VERSION

#### Content centric networking
- Thousands of people on the same local network or sitting right next to each other can all request the same video and the routers will return a thousand separate responses of that same video
- This greatly reduces the scalability of many sites.  
- If we're only interested in the data itself and not where it came from, we could instead allow routers to have lots of memory and hold these responses
- Next time there's a request for this response it can just key in and give it back