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
