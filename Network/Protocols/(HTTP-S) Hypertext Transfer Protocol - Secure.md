When using a browser HTTP and HTTPS are mainly used, which relies on TCP and defines your web browser communicates with the web servers.

HTTP and HTTPS usually use TCP ports 80 and 443, less commonly 8080 and 8443
# Request and Response
## Requests
The commands and methods used by the web browser to the web server are:
- `GET` retrieves data from a server (HTML file or an image)
- `POST` submits new data to the server (submitting a form or uploading a file)
- `PUT` used to create a new resource on the server and to update and overwrite existing information
- `DELETE` used to delete a specific file or resource on the server
- `PATCH` used to update a resource object

>[!note]
>[[(Telnet) Teletype Network|Telnet]] can be used to connect to web servers and communicate with them.

## Responses

| **Response Code** | **Description** |
| ----------------- | --------------- |
| 1XX               | Informational   |
| 2XX               | Successful      |
| 3XX               | Redirect        |
| 4XX               | Client error    |
| 5XX               | Server error    |

# HTTPS
HTTPS is the secure version of HTTP, meaning that the data is encrypted when transferred.
This is made possible by using (TLS) Transport Layer Security.
A HTTPS request consists of the following steps:
1. Establish a TCP three-way handshake
2. Establish a TLS session
3. Communicate using the HTTP protocol