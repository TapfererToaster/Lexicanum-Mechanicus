# HTTP-based Network APIs
[[(HTTP-S) Hypertext Transfer Protocol - Secure|HTTP-based]] APIs are one of the most common interprocess connection types.
## RESTful APIs
RESTful APIs work in a [[Server#Server-Client|server-client]] pair and although HTTP is used for the request, the server responds with XML or JSON.
An interface must conform to six architectural constraints to be considered RESTful
- *Client-Server*
- *Stateless*
The communication between the client and server must be stateless, meaning the client must send all data required for the server to understand and perform the requested operation in a single request.
- *Uniform interface*
Individual resourced in scope within an API call are identified in HTTP request messages and the client should have enough information about a resource to create, modify or delete a resource.

### HTTP request types
RESTful APIs are using HTTP as transport, so they also use [[(HTTP-S) Hypertext Transfer Protocol - Secure#Requests /Methods|HTTP requests]] but the meaning is different.

| **Request type** | **HTTP context**               | **network context**                      |
| ---------------- | ------------------------------ | ---------------------------------------- |
| `GET`            | Retrieve a specific resource   | Obtain configuration or operational data |
| `PUT`            | Creates or replaces a resource | Changing a configuration                 |
| `PATCH`          | Creates or updates a resource  | Changing a configuration                 |
| `POST`           | Creates a resource             | Changing a configuration                 |
| `DELETE`         | Deletes a specific resource    | Remove a configuration                   |
>[!note]
>Non-RESTful HTTP APIs do not adhere to these meanings.

