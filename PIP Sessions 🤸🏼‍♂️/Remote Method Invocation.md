![[Pasted image 20240906152638.png]]
RMI enable JVM object to invoke to call other method in another JVM object
## Architecture
- Client: JVM object that call remote method
- Server: JVM object that provide remote method
## Main Components
* Remote Interface: Define the method that will be called remotely
* Remote Object: Implement the remote interface
* Stub: Client side proxy object
* Skeleton: Server side proxy object
## Process
*  Server create remote object and register it to RMI registry
* Client look up the remote object from RMI registry
* Client get the stub object from the remote object