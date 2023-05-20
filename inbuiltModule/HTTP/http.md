## Classes
Sure, here's a brief summary of the important objects related to the Node.js `http` module:

1. **`http.Agent`**: This is a class that is responsible for managing HTTP client connections. An Agent object is associated with each ClientRequest and it manages connection persistence and reuse for HTTP clients. It maintains a queue of pending requests for a given host and port and reuses a single socket connection for each.

2. **`http.ClientRequest`**: This is a writable stream and an instance of this class is created internally when making a request using `http.request()`. It represents an in-progress request whose header has already been queued. The header is still mutable using the `setHeader(name, value)`, `getHeader(name)`, `removeHeader(name)` methods. The actual header will be sent along with the first data chunk or when calling `request.end()`.

3. **`http.Server`**: This is an EventEmitter that represents an HTTP server. It listens for the 'request' event, which is triggered each time a request is received. You can create a new server using `http.createServer([options][, requestListener])`.

4. **`http.ServerResponse`**: This is a writable stream and an instance of this class is created internally by an HTTP server--not by the user directly. It is passed to the 'request' event as the second parameter. It represents the response to be sent back to the client for the incoming request.

5. **`http.IncomingMessage`**: This is a readable stream that is passed to the 'request' event of `http.Server` and the 'response' event of `http.ClientRequest`. It represents the response from the server (as received by the client) or the request from the client (as received by the server).

6. **`http.OutgoingMessage`**: This is the abstract base class for `http.ServerResponse` and `http.ClientRequest`. It's not intended to be used directly but contains functionality common to both server and client-side messages, like setting headers and sending the message body.

Keep in mind that the ServerResponse and IncomingMessage objects are created internally by an HTTP server, not by the user directly. They are created when an HTTP request is received, and they are passed as arguments to the 'request' event listener.

On the other hand, ClientRequest objects are created when you're making an HTTP request. These could be created directly using `new http.ClientRequest(options[, callback])`, but in most cases, you'd use `http.request()` or `http.get()` instead, which create the ClientRequest object for you.

## Create a basic server
```JS
const http = require('http');  // import http module

const server = http.createServer((req, res) => {  // create an HTTP server
    res.statusCode = 200;  // set the status code to 200, indicating success
    res.setHeader('Content-Type', 'text/plain');  // set the content type of the response to text/plain
    res.end('Hello, World!\n');  // send a response back to the client
});

server.listen(3000, '127.0.0.1', () => {  // set the server to listen on port 3000
    console.log('Server is listening on port 3000');
});
```

## `http.IncomingMessage` and `http.ServerResponse`

1. **http.IncomingMessage**: This object is created by the HTTP server or client (depending on whether it's a server request or client response object respectively). It's passed as the first argument to the 'request' event of the server and the 'response' event of the client. It has several properties and methods to help you extract information from the HTTP request. Here are a few key ones:

    - **method**: The HTTP method used for the request (e.g., 'GET', 'POST').
    - **url**: The request URL string.
    - **headers**: An object containing the incoming HTTP headers.
    - **httpVersion**: The HTTP version sent by the client.
    - **statusCode** (response only): The 3-digit HTTP response status code.
    - **statusMessage** (response only): The HTTP response status message (e.g., 'OK' for a 200 status code).

    Additionally, `http.IncomingMessage` is a readable stream, so you can use stream methods (like `pipe()`, `read()`, etc.) and events (like 'data', 'end', etc.) to process the body of the HTTP message.

2. **http.ServerResponse**: This object is created internally by an HTTP server, and it's passed as the second argument to the 'request' event. The ServerResponse object represents the response to be sent to the client for the HTTP request. Key properties and methods include:

    - **statusCode**: The HTTP status code to send to the client.
    - **statusMessage**: A message corresponding to the status code.
    - **setHeader(name, value)**: Sets a single header value for implicit headers.
    - **getHeader(name)**: Reads out a header that's already been queued.
    - **removeHeader(name)**: Removes a header that's queued for implicit sending.
    - **write(chunk[, encoding][, callback])**: Sends a chunk of the response body. This method may be called multiple times to provide successive parts of the body.
    - **end([data][, encoding][, callback])**: Signals to the server that all of the response headers and body have been sent.

Remember, both of these are streams - `http.IncomingMessage` is a readable stream, and `http.ServerResponse` is a writable stream. This means you can use the Node.js stream APIs to handle data in a highly efficient way. This is especially important when dealing with large amounts of data, such as files or data streams.

## Headers
HTTP headers allow the client and the server to pass additional information with an HTTP request or response. Headers are defined by their names and values, which are written as "name: value".

Here's a brief overview of the methods you can use to manipulate headers in Node.js using the `http` module:

1. **`response.setHeader(name, value)`**: This method sets a single header's value. If this header already exists in the to-be-sent headers, its value will be replaced. Note that header names are case-insensitive.

    ```javascript
    response.setHeader('Content-Type', 'text/html');
    response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
    ```

2. **`response.getHeader(name)`**: This method reads the value of a header. The name is case-insensitive. This can be useful for conditional processing of the response.

    ```javascript
    var contentType = response.getHeader('content-type');
    ```

3. **`response.removeHeader(name)`**: This method removes a header that's in the headers to-be-sent list.

    ```javascript
    response.removeHeader('Content-Encoding');
    ```

4. **`response.hasHeader(name)`**: This method checks if a specified header is present in the headers to-be-sent list.

    ```javascript
    if (response.hasHeader('Content-Type')) {
      console.log('Content-Type is set');
    }
    ```

Note that headers cannot be manipulated after they've been sent. You'll get an error if you try to use these methods after headers have been sent to the client (e.g., after `response.end()` or `response.flushHeaders()` have been called). So, be sure to set, get, check, or remove headers before you start sending the response body.

Additionally, remember that the `http` module does not automatically set many headers. For example, while it sets the `Date` and `Connection` headers, you're responsible for setting headers like `Content-Type` and `Content-Length`.

You should familiarize yourself with common HTTP headers like `Content-Type`, `Content-Length`, `Set-Cookie`, `Cache-Control`, and others, and understand how they affect the behavior of the client and server.

## Methods
HTTP methods, sometimes referred to as HTTP verbs, indicate the desired action to be performed on the resource identified by the given URL. The most common methods include GET, POST, PUT, DELETE, PATCH, etc.

In Node.js using the `http` module, the `request.method` property can be used to determine which HTTP method was used in a request. Here's an example of a simple HTTP server that handles different methods:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    switch (req.method) {
        case 'GET':
            // Handle GET request
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Received a GET request\n');
            break;

        case 'POST':
            // Handle POST request
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Received a POST request\n');
            break;

        case 'PUT':
            // Handle PUT request
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Received a PUT request\n');
            break;

        case 'DELETE':
            // Handle DELETE request
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Received a DELETE request\n');
            break;

        default:
            res.statusCode = 404;
            res.end('Invalid Method\n');
    }
});

server.listen(3000, () => {
    console.log('Server is listening on port 3000');
});
```
