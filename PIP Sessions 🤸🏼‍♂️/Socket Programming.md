Is a programming technique in networking that enables the communication between two computers. It is a way of connecting two nodes on a network to communicate with each other. 
In socket programming, socket act as endpoint of communication, including TCP/IP and UDP. 

## Socket Type

### TCP (Transmission Control Protocol)
- Connection-oriented protocol: requires a connection to be established between the two processes before they start communicating.
- Handshaking process: involves three-way communication to set up a connection.
- Reliable and ordered: data is delivered in the same order in which it was sent.
### UDP (User Datagram Protocol)
- Connectionless protocol: no connection is established before data is sent.
- No handshaking process: data is sent without any prior communication.
- Unreliable and unordered: data may arrive out of order, appear duplicated, or get lost.

## Main Components
### IP Address
- Unique address assigned to each device connected to a network.
- Used to identify the device on the network.
### Port Number
- Unique number assigned to a process running on a device.
- Used to identify the process on the device.