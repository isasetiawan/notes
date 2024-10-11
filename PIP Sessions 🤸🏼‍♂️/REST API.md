Is an application programing interface that conforms to the design of principles of Representational State Transfer (REST). REST API is a common way to exchange data between web services and clients.
## Principles of REST API

At basic level, an API is mechanism that allows application or service to access resources within another application or service. The resources could be data, services, or other assets. REST API is a type of API that follows the principles of REST.
### Uniform Interface
A REST API should have a uniform interface. This means that the API should have a consistent way of interacting with the resources. The uniform interface should be easy to understand and use.
For HTTP-based REST APIs, the interface consist of:
1. **Resource URI**: A URI that uniquely identifies the resource. For example, `/users` or `/users/1`.
2. **HTTP Methods**: The HTTP methods that are used to interact with the resource. The common HTTP methods are `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.
3. **Headers**: The HTTP headers that are used to provide additional information about the request or response. The common headers are `Content-Type`, `Accept`, and `Authorization`.
4. **Body**: The body of the request or response. The body could be in different formats such as JSON, XML, or HTML.
4. **Representation**: The representation of the resource. The representation could be in different formats such as JSON, XML, or HTML.
5. **Hypermedia**: Hypermedia is the ability to include links in the response that allows the client to navigate to other resources. Hypermedia is used to make the API more discoverable and self-descriptive. For example, the response could include links to related resources as below
 ```json
{
  "id": 1,
  "name": "John Doe",
  "links": [
    {
      "rel": "self",
      "href": "/users/1"
    },
    {
      "rel": "friends",
      "href": "/users/1/friends"
    }
  ]
```
5. **Status Codes**: The HTTP status codes that are used to indicate the result of the request. Status code are divided into:
	  - 1xx: Informational
	  - 2xx: Success
	  - 3xx: Redirection
	  - 4xx: Client Error
	  - 5xx: Server Error
### Client-Server Decoupling
A REST API should be decoupled from the client and server. This means that the client and server should be able to evolve independently. The client and server should not be tightly coupled. This allows the client and server to be developed and maintained separately.
### Stateless
A REST API should be stateless. This means that the server should not store any state about the client. Each request from the client should contain all the information needed to process the request. This allows the server to be more scalable and reliable.
### Cacheable
A REST API should be cacheable. This means that the server should indicate whether the response can be cached by the client. This allows the client to cache the response and reuse it for subsequent requests. This can improve the performance of the API.
### Layered System
A REST API should be a layered system. This means that the client should not be able to tell whether it is connected directly to the server or to an intermediary. This allows the server to be more scalable and reliable.
Layered architecture enable to put proxies, gateways, or load balancers between the client and server to handle different aspects of the communication.


# TODO:
1. What is improved from SOAP
2. Design for resources `users` and `user_activities` 
3. researching standard
4. research remote method invocation and CORBA