# W2D6 Notes

## Creating HTTP Web Server in Node.js

- By requiring built-in http library, we can create the server. Have to set the content header and send the string to the response. Also, we make the server listen on port 7000 in the example below. After running from command and from the browser, access to localhost:7000
```javascript
const http = require('http');


const server = http.createServer((function(request,response) {

  response.writeHead(200,
      
    {
      'Content-Type': 'text/plain'
    }
  );

  response.end('Hello World\n');
}));

server.listen(7000);
```
- Another way:
```javascript
//Load HTTP module
const http = require('http');
const hostname = '127.0.0.1';
const port = 3000;

//Create HTTP server and listen on port 3000 for requests
const server = http.createServer((req, res) => {

  //Set the response HTTP header with HTTP status and Content type
  res.statusCode = 200;
  res.setHeader('Content-Type', 'test/plain');
  res.end('Hello World\n');
});

//listen for request on port 3000, and as a callback function, have the port listened on logged
server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```


## Starting express on node 
1. create a project directory
2. npm install express --save 
3. create a server.js or index.js file: 
4. in the server.js file, add express on top
```javascript
const express = require('express');
const app = express(); 
```
5. using port number, create pages like this. In this example, there are two pages: 
```javascript
const express = require('express');
const app = express();
const port = 3000;

//to get the server up and running:
app.listen(port, function () {
  console.log('Server running');
});

//now, make something happen on a page. Run node and goto page: "localhost:3000"
app.get('/', function(req, res) {
  res.send('Hello World!');
});

//create another page at the address /parks. Run node and goto page: "localhost:3000/parks"
app.get('/parks/', function(req, res) {
  res.send('The Parks you have seen');
});
```