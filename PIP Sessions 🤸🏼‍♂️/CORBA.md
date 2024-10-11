![[Pasted image 20240906153747.png]]
Common Object Request Broker Architecture is an architecture and standard to manage distributed object in a network

## Main Component
- Object Request Broker (ORB): act as a mediator between client and server, handle request and response
- Interface Definition Language (IDL): a neutral language to define object interface
## Process
* Object is defined in IDL
* IDL is compiled to generate stub and skeleton on client and server
* Client call object method through stub