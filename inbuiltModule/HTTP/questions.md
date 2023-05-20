## 1: How does the HTTP request-response cycle work in Node.js?

Answer:

In Node.js, the HTTP request-response cycle is managed using the HTTP module, which provides a way of creating HTTP servers and making HTTP requests. Here's a basic breakdown of how the cycle works:

1. **HTTP Request:** When a client (like a web browser) wants to communicate with a server, it sends an HTTP request to the server. This request includes things like the method (GET, POST, DELETE, etc.), URL, headers, and possibly a body (like form data or JSON).

2. **Server Processing:** The Node.js server receives this request and processes it. The HTTP module's `createServer()` method is used to create a server instance. This method takes a callback function, which will be called each time a request is received. The callback function is given two arguments: an `IncomingMessage` object (representing the request) and a `ServerResponse` object (used to send a response).

   Here's a simple example:
   ```javascript
   const http = require('http');

   const server = http.createServer((req, res) => {
       // handle request and send response
   });

   server.listen(8000);
   ```
   
3. **Routing and Handlers:** Inside the callback function, you typically have logic to handle different routes (based on the request URL) and methods. For example, a GET request to "/users" might return a list of users, while a POST request to the same URL might create a new user.

4. **Sending a Response:** To send a response, you use the `ServerResponse` object. This includes setting the status code, headers, and body. For example:
   ```javascript
   res.statusCode = 200;
   res.setHeader('Content-Type', 'application/json');
   res.end(JSON.stringify({ message: 'Hello World' }));
   ```

5. **HTTP Response:** Once the `end()` method of `ServerResponse` is called, the HTTP response is complete and is sent back to the client.

This is a basic explanation. In a real-world application, you would likely use a framework like Express.js, which provides a higher-level interface for handling HTTP requests and responses.

## 2: What is the purpose of the `http.createServer()` method

Answer:

The `http.createServer()` method in Node.js is used to create an HTTP server. This method returns a new instance of `http.Server`. The `http.Server` class is an EventEmitter, meaning it can emit events, the most fundamental of which is the 'request' event.

When the HTTP server is started and begins listening for connections, it will call a requestListener function (the callback function) each time a client makes a request to the server. This function takes two arguments: a request (an instance of `http.IncomingMessage`) and a response (an instance of `http.ServerResponse`).

Here's a simple example:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // req is an instance of http.IncomingMessage
    // res is an instance of http.ServerResponse

    // Send a 'Hello, World!' response to the client
    res.end('Hello, World!');
});

// Start the server and listen on port 8000
server.listen(8000, () => {
    console.log('Server is listening on port 8000');
});
```

In this example, the `http.createServer()` method is used to create a new HTTP server that listens on port 8000. Whenever a client makes a request to this server, the server will send back a response of 'Hello, World!'.

## 3: How can you stream data using the HTTP module?

Answer:

Streaming is a critical concept in Node.js that allows handling data in chunks as they arrive or get processed, rather than loading all data into memory upfront. This is particularly useful when dealing with large amounts of data.

In the context of the HTTP module, both the `http.ServerRequest` and `http.ServerResponse` objects are stream interfaces. Here's an example of how you might use streaming:

**Example 1 - Streaming a Request:**

If you are receiving a large file as a part of the request, you can handle it as a stream to prevent overloading your server's memory:

```javascript
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    const writeStream = fs.createWriteStream('./largeFile');
    req.pipe(writeStream);

    req.on('end', () => {
        res.end('File received and saved successfully.');
    });
});

server.listen(8000);
```

In this example, the incoming request (which we're assuming is a large file upload) is piped to a write stream, which writes the file to the disk as data comes in.

**Example 2 - Streaming a Response:**

Conversely, if you are sending a large file as a response, you can stream it to the client:

```javascript
const http = require('http');
const fs = require('fs');

const server = http.createServer((req, res) => {
    const readStream = fs.createReadStream('./largeFile');
    readStream.pipe(res);
});

server.listen(8000);
```

In this example, we're creating a read stream from a large file and piping it to the response. The file will be streamed to the client as soon as the server starts reading it, rather than reading the entire file into memory before sending it.

## 4: What are the differences between `http.get()` and `http.request()` methods in the HTTP module?

Answer:

The `http.get()` and `http.request()` methods in Node.js are used to make HTTP requests from the server. However, there are some differences between the two methods.

1. **http.request():** This method is the most generic way of making an HTTP request. It allows you to specify the method (GET, POST, PUT, DELETE, etc.), headers, and other options. You also need to manually end the request by calling `request.end()`. Here's an example:

    ```javascript
    const http = require('http');

    const options = {
        hostname: 'www.example.com',
        port: 80,
        path: '/',
        method: 'GET'
    };

    const req = http.request(options, (res) => {
        // handle the response
    });

    req.end();
    ```

2. **http.get():** This is a convenience method for making GET requests. It is identical to `http.request()` but automatically sets the method to GET and calls `request.end()` for you. As a result, you don't need to call `request.end()` manually. Here's an equivalent example using `http.get()`:

    ```javascript
    const http = require('http');

    const options = {
        hostname: 'www.example.com',
        port: 80,
        path: '/'
    };

    const req = http.get(options, (res) => {
        // handle the response
    });
    ```

In summary, `http.get()` is a simpler method specifically for GET requests. It automatically ends the request for you. In contrast, `http.request()` is more versatile and allows you to specify the HTTP method and other options. However, it requires you to manually end the request.

## 5: How does error handling work in the HTTP module? What happens when an 'error' event is emitted?

Answer:

Error handling in the HTTP module in Node.js typically revolves around listening to the 'error' event that can be emitted on instances of `http.Server`, `http.ServerRequest`, and `http.ServerResponse`.

Here's a simple example of error handling on an HTTP server:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    // Handle request and send response
});

server.on('error', (err) => {
    console.error('An error occurred:', err);
});

server.listen(8000);
```

In this example, if an error occurs within the server, such as a problem with the network or a thrown exception within the request handling code, the 'error' event is emitted. The event listener then logs the error to the console.

For requests and responses, you can also attach error listeners:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    req.on('error', (err) => console.error('Request error:', err));
    res.on('error', (err) => console.error('Response error:', err));

    // Handle request and send response
});

server.on('error', (err) => {
    console.error('Server error:', err);
});

server.listen(8000);
```

In this example, separate 'error' event listeners are attached to the request and response objects. If an error occurs while reading the request or writing the response, the respective error event is emitted and the error is logged to the console.

Proper error handling is important in Node.js, as unhandled exceptions will cause the server to stop. Hence, listening for and handling 'error' events is a crucial part of working with the HTTP module.

## 6: Can you explain how the `http.Agent` class works and its role in the HTTP module?

Answer:

In Node.js's HTTP module, the `http.Agent` class is responsible for managing connections for HTTP clients. When you make an HTTP request, an instance of `http.Agent` is used to manage the pooling of sockets used in these client requests.

By default, Node.js uses a global Agent instance, which provides a default connection pool. However, it is also possible to create a new Agent instance to customize how connections are pooled. For example, you can change the maximum number of sockets allowed, or disable pooling altogether.

Here's an example of creating a new Agent with a higher maxSockets value:

```javascript
const http = require('http');
const keepAliveAgent = new http.Agent({ keepAlive: true, maxSockets: 50 });

http.request({
    hostname: 'localhost',
    port: 8000,
    path: '/',
    agent: keepAliveAgent  // Use our custom Agent
}, (res) => {
    // Handle the response
});
```

In this example, we've created a new Agent that allows up to 50 sockets and keeps sockets around even when they're not in use (this is what the `keepAlive: true` option does).

The `http.Agent` is an important part of the HTTP module because it controls how requests are made. By pooling sockets, it can greatly increase the efficiency of your HTTP client, especially under high load. However, it's also important to manage your Agent properly, as too many sockets can lead to high memory usage.

## 7: What is the role of the `http.ServerResponse` object and which are its most important methods?

Answer:

The `http.ServerResponse` object in Node.js represents the server's response to a client's HTTP request. It's created internally by an HTTP server, not by the user directly. It's passed as the second parameter to the server's request event handler function.

Here are some of its important methods:

1. **response.setHeader(name, value):** This method sets the headers for the response. The name and value are both strings. Note that this method must be called before the response headers are sent to the client using the `response.writeHead()` method.

2. **response.writeHead(statusCode, [statusMessage], [headers]):** This method sends a response header to the request. It must be called before `response.end()`.

3. **response.write(chunk, [encoding], [callback]):** This method sends a chunk of the response body. This method can be called multiple times to provide successive parts of the body.

4. **response.end([data], [encoding], [callback]):** This method signals to the server that all of the response headers and body have been sent; that server should consider this message complete. The method, `response.end()`, must be called on each response. If any data is specified, it is equivalent to calling `response.write(data, encoding)` followed by `response.end(callback)`.

5. **response.statusCode:** This property indicates the status code of the response (e.g., `200` for "OK" or `404` for "Not Found"). It should be set before the response headers are written to the client.

Here's a basic example of using a `http.ServerResponse` object:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello, World!');
});

server.listen(8000);
```

In this example, we create a new HTTP server and handle each request by sending a response with a status code of 200, a content type of 'text/plain', and a body of 'Hello, World!'.


