# Simplicity 
Soap is xml based protocol that usual more complex to write and process. Soap using envelope, header and body that require more complex handling.
Meanwhile REST is more simple due to utilization of HTTP methods like post put delete and usually using JSON as body message that easier to process.
# Performance 
The usage of XML in soap increase complexity to parse due to its verbosity. Meanwhile the ability to use JSON as body message, its makes REST more performative than SOAP
# Statelessness
SOAP requires a stateful communication, which means that the server needs to keep track of the state of each client. REST is stateless, which means that each request from a client to the server must contain all the information needed to process the request. This makes REST more scalable and reliable than SOAP.

Example of stateful communication in SOAP:
```xml
<soap:Envelope>
    <soap:Header>
        <transactionId>123</transactionId>
    </soap:Header>
    <soap:Body>
        <getUserDetails>
            <userId>123</userId>
        </getUserDetails>
    </soap:Body>
    </soap:Envelope>
    ```
Above example, the transactionId is used to keep track of the state of the client. The server needs to keep track of the transactionId to process the request.

Example of stateless communication in REST:
```json
GET /users/123
```
In this example, the request contains all the information needed to process the request. The server does not need to keep track of the state of the client.
# Flexibility Data Format
SOAP only support XML format. Meanwhile REST can use different data format like JSON, XML, HTML, and plain text. This makes REST more flexible than SOAP.
# Usage of HTTP Standard
Even SOAP can be used over many protocols including HTTP, it doesn't use HTTP methods and status codes. REST using HTTP methods and status codes which makes it more intuitive and easier to use.
# Caching
REST can be cached, which can improve the performance of the API. SOAP does not support caching.