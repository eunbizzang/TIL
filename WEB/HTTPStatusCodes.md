https://www.baeldung.com/cs/http-status-codes

https://developer.mozilla.org/ko/docs/Web/HTTP/Status


HTTP takes the form of requests and responses between a client (e.g. a browser) and a server. When we click on a link, type a URL in our browser, or submit a form, the browser is initiating an HTTP request to a server telling that server what we would like it to do. For example, a typical HTTP request/response communication between two computers could look like this:

Client Request:

```
GET / HTTP/1.1 
Host: www.google.com
```

Server Response:
```
HTTP/1.1 200 OK 
Date: Sat, 12 Sep 2020 14:26:56 GMT 
Expires: -1 
Cache-Control: private, max-age=0 
Content-Type: text/html; charset=ISO-8859-1 
Set-Cookie: ...truncated... 
Accept-Ranges: none 
Vary: Accept-Encoding 
Transfer-Encoding: chunked 

(html)
```

HTTP Status Codes

According to the IETF, an HTTP status code is a three-digit integer code giving the result of the server’s attempt to understand and satisfy the request. Status codes are not meant for the human user; instead, they’re intended for the client to interpret and act accordingly. A client can be a browser, another server, or any application making an HTTP request.

HTTP status codes are divided into 5 classes based on the first digit of the status code:

* 1xx – informational – the request was received, continuing process
* 2xx – successful – the request was received successfully and accepted
* 3xx – redirection – further action needs to be taken to complete the request
* 4xx – client error – request contains bad syntax or cannot be fulfilled
* 5xx – server error – the server failed to fulfill an apparently valid request

---
* 200 OK

A 200 status code indicates that the request was successful and could be the result of any of the following operations: GET, POST, PUT, PATCH, and DELETE. When a server responds with a 200, the response must also contain a payload that is appropriate for the action. For example, the payload of a 200 response to a GET request would typically contain the requested resource, like the requested Html page.


* 201 Created
A 201 response indicates that a request was successful and resulted in a new resource being created. An example of a request which could result in a 201 status code is when we submit a form to create a new resource.

* 301 Found
A 301 response tells us that the resource we’re requesting has moved permanently. A 301 response must contain a Location header with the URI of the new location. This Location can then be used by the client to repeat the request successfully at the new location.

* 400 Bad Request
This status code means that the HTTP request sent over to the server has incorrect syntax. For example, if we have submitted a form with incorrectly formatted data or the wrong data type, this could result in a 400 response.

*  401 Unauthorized
This means that the user who is trying to access the resource by sending the request has not been properly authenticated. According to the HTTP standards, when a server responds with a 401 it must also send a WWW-Authenticate header with a list of the authentication schemes that the server uses.

* 403 Forbidden
A 403 response is commonly confused with 401; however, the 403 response means that the server is refusing our request due to insufficient access or permissions. Even if we’re authenticated, we may not be allowed to make a certain request.

*  404 Not Found
This status code is returned when the requested resource is not found. For instance, if we entered a URL for a page that does not exist on a website or was deleted for some reason, it would result in a 404 response.

    example:

    ```
    POST /test HTTP/1.1 
    Host: www.google.com
    ```
    This will result in a 404 status code from Google:
    ```
    HTTP/1.1 404 Not Found 
    Content-Type: text/html; charset=UTF-8 
    Referrer-Policy: no-referrer 
    Content-Length: 1565 
    Date: Sat, 12 Sep 2020 16:38:02 GMT 

    (html)
    ```

*  405 Method Not Allowed
A 405 response means that the server does not support the method used in the request. For example, if an endpoint only accepts GET requests and we try to send a POST, it will result in a 405 response code. If this is the case, servers must also send back an Allow header field with the list of the allowed methods.

    example:
```
    DELETE / HTTP/1.1 
    Host: www.google.com
    Will result in the response:

    HTTP/1.1 405 Method Not Allowed 
    Allow: GET, HEAD 
    Date: Sat, 12 Sep 2020 15:39:35 GMT 
    Content-Type: text/html; charset=UTF-8 
    Server: gws 
    Content-Length: 1591 
    X-XSS-Protection: 0 
    X-Frame-Options: SAMEORIGIN 

    (html)
```

* 408 Request Timeout
This status code is an indication from the server that the request message was not completed within the time that the server was prepared to wait. If a client is too slow in sending its HTTP request, this could happen. This could be due to many reasons, including a slow internet connection.

* 413 Request Entity Too Large
This status code tells us that the server is unable or unwilling to process the request because the request payload is too large. This could happen if we try to upload a file that is too large and exceeds the server limits.

* 500 Internal Server Error
An internal server error means that for some reason the server could not process the request due to an error. This is generally due to a bug or an unhandled exception on the server.

* 429 Too Many Requests
Occasionally, services may want to limit the number of requests being made to their resources. The 429 response code indicates to the client that the number of allowed requests has been exceeded. This is useful for rate-limiting users and even for monetizing APIs.

* 418 I’m a Teapot
The 418 status code was published as an April Fools joke in April 1998. It has not been registered as an official response code but has been adopted by many frameworks and libraries such as Node.js and ASP.Net as an “easter egg” joke. In fact, we could even visit https://www.google.com/teapot to see this in action.