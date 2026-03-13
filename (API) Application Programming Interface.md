# HTTP-based Network APIs
[[(HTTP-S) Hypertext Transfer Protocol - Secure|HTTP-based]] APIs are one of the most common interprocess connection types.
## RESTful APIs
RESTful APIs work in a client-server pair with the client being an application such as a Python script or a web UI and the server being a network device or controller.
Although HTTP is used the server will not respond with HTML data, but with XML or JSON, which the client must understand.
An interface must conform to six architectural constraints to be considered RESTful
- *Client-Server*
- *Stateless*
The communication between the client and server must be stateless, meaning the client must send all data required for the server to understand and perform the requested operation in a single request.
- *Uniform interface*
Individual resourced in scope within an API call are identified in HTTP request messages and the client should have enough information about a resource to create, modify or delete a resource.

### HTTP request types
RESTful APIs are using HTTP as transport, so they also use the [[(HTTP-S) Hypertext Transfer Protocol - Secure#Request Types|HTTP requests types]], but the meaning is different.

| **Request type** | **HTTP context**               | **network context**                      |
| ---------------- | ------------------------------ | ---------------------------------------- |
| `GET`            | Retrieve a specific resource   | Obtain configuration or operational data |
| `PUT`            | Creates or replaces a resource | Changing a configuration                 |
| `PATCH`          | Creates or updates a resource  | Changing a configuration                 |
| `POST`           | Creates a resource             | Changing a configuration                 |
| `DELETE`         | Deletes a specific resource    | Remove a configuration                   |
>[!note]
>Non-RESTful HTTP APIs do not adhere to these meanings.

