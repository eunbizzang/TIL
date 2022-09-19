Cross-Origin resource sharing(CORS)
1. CORS is a protocol that enables scripts running on a browser client to interact with resources from a different origin.
2. For example, if a UI app wishes to make an API call running on a different domain, it would be blocked from doing so by default due to CORS. so CORS is not a security issue/attack but the default protection provided by browsers to stop sharing the data/communication between different origins.
3. "other origins" means the URL being accessed differs from the location that the JavaScript is running from, by having : 
- a different scheme(HTTP or HTTPS)
- a different domain
- a different port
4. But what if there is a legitimate scenario where cross-origin access is desirable or even necessary.
5. When a server has been configured correctly to allow cross-origin resource sharing, some special headers will be included. Their presence can be used to determine that a request supports CORS. Web browsers can use these headers to determine whether a request should continue or fail.
6. First the browser sends a pre-flight request to the backend server to determine whether it supports CORS or not. The server can then respond to the pre-flight request with a collection of headers : 
- Access-Control-Allow-Origin : Defines which origins may have access to the resource. A '*' represents any origin
- Access-Control-Allow-Methods : Indicates the allowed HTTP methods for cross-origin requests
- Access-Control-Allow-Headers : Indicates the allowed request headers for cross-origin requests
- Access-Control-Allow-Credentials : Indicates whether or not the response to the request can be exposed when the credentials flag is true.
- Access-Control-Max-Age : Defines the expiration time of the result of the cached preflight request
