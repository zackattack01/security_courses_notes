# Link
- shared network infrastructure focuses only on packets

### Layered Network Model
- allows designing a network to be broken into more manageable sub problems
- TCP/IP "internet protocol suite" is the best known example of this
- ties together
```
|Application Layer |          |Transport Layer (TCP)|  |Internetwork Layer (IP)|   |Link Layer (Ethernet, WiFi) |
        ↓                             ↓                           ↓                               ↓
|web, email, file transfer|   |reliable connections |    |simple, unreliable |         |physical connections | 
```

- more details about the internet suite [here](https://en.wikipedia.org/wiki/Internet_protocol_suite)

### Link Layer

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
  