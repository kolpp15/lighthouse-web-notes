# W3D1 Notes

## TCP
- persistent connection between client and server
- either party can shout down the pipe at any time

## HTTP
- built on top of TCP
- request => response

## Address
- IP home address of a server
- port (this acts like a unit # in an apartment) 

## Request
- verb => what do we want to do?
  1. GET => retrieve information 
      - what we see in a browser will ALWAYS be a GET
  2. POST => send information (ex. i want to log in/out)
- path => what do we want to do it to? 
  - always going to be a string
  - `/users`, `/photos` 
- ex) 
  - `GET /users`, `POST /maps`

## HTTP example (not a good way to create server)
- goto nodejs.org to check the NODE HTTP info (not npm)
- it will always be asynch because it'll take some time to load
- http.createServer([options][,requestListener])
  - requestListener will ALWAYS be a callback
```javascript
const http = require('http');

const server = http.createServer((request, response) => {
  const url = request.url;
  const method = request.method;
  const requestInfo = `${method} ${url}`;

  console.log(requestInfo);

  if (requestInfo === 'GET /home') {
    resonse.write('thanks for visiting the home page');
  } else if (requestInfo === 'GET /about') {
    response.write('you are on the about page');
  } else {
    response.write('this is not the page you are looking for');
  }
  
  // response.write('hello world');
  response.end(); // you need this to execute 
});

server.lister(23456);
```
  - when you run the file by node, if you see that the command line is on the empty line, it's a good sign!!

## Express example (better than HTTP to create server)
1. initialize for package.json (npm init -y)
    - npm init -y will skip the package.json inputting steps (-y means yes)
2. command: npm install express 
    - this will download all the necessary node_modules
3. create server.js to create a server
```javascript
const express = require('express');
const morgan = require('morgan');
const app = express(); 

const cats = {
  abcd: {
    name: 'Mika',
    fluffy: true
  },
  defg: {
    name: 'Scruffy',
    fluffy: false
  }
}; 

const printCat = (id) => {
  console.log(cats[id]);
};

// how to use MIDDLEWARE app.use() for all middleware. third parameter next will tell express to continue on and look for it 
// app.use((req, res, next) => {
//   console.log(`${req.method} ${req.url}`)
//   next();
// }); 

// USING morgan library for middleware
app.use(morgan('dev'));

// GET /home 
app.get('/home', (req, res) => { // if request comes into home, we will call this callback. ALWAYS need a callback
  res.write('welcome to our site!'); 
  //like HTTP, we have to end to see it in the browser. same as end() in http
  res.send();
  // res.send('welcome to our site!'); will work too
});

app.get('/cats', (req, res) => {
  res.json(cats); // because cats is an object. this will output a raw java dats in the browser
})

// GET /cats/:cat_id using URL parameters
app.get('/cats/:cat_id', (req,res) => {
  console.log(req.params);
  const catID = req.params.cat_id;
  const cat = cats[catId];

  res.json(cat);
});
// by using this generic endpoint, we don't have to GET specifically
// now, goto localhost:6543/cats/abcd OR whatever cat key

app.listen(6543);
```
  - then we run node and check browser (localhost:6543/home)
    - localhost:6543 will output error404 because localhost:6543/ is not set up in the server page

## Express middleware 
- function that runs between the request and the response 
- we'll use it for: parsing the incoming request 
- when we request credential:
`email=a@a.com&password=1234` <== url encoded
```javascript
{
  email: 'a@a.com',
  password: '1234'
}
```
- body-parser will return above object 

## TIP library 
- npm install morgan
- this will give middleware information in command. You have to specify which info you want. 'dev' is simple and enough
- ALWAYS USE MORGAN FOR ALL PROJECTS

- http.cat url will give all the statuscodes 

## Another Sample
```javascript
const http = require("http");
const PORT = 8080;

// a function which handles requests and sends response
const requestHandler = function(request, response) {
  // console.log('In requestHandler'); //checking: Prints when client requests
  
  if (request.url === '/') {
    response.end('Welcome!');
  } else if (request.url === '/urls') {
    response.end('www.lighthouselabs.ca\nwww.google.com');
  } else {
    response.statusCode = 404;
    response.end('404 Page Not Found');
  }
  // response.end(`Requested Path: ${request.url}\nRequest Method: ${request.method}`);
};

const server = http.createServer(requestHandler);
// console.log('Server created'); //checking: Prints 1st

server.listen(PORT, () => {
  console.log(`Server listening on: http://localhost:${PORT}`); //checking: Prints 3rd
});

// console.log('Last line (after .listen call)'); //checking: Prints 2nd
```

## Setting up EJS
1. npm init -y => npm install express => npm install ejs
2. refer to w3 'ejs-demo' folder for reference!!!

## Object Tips & res.render()
```javascript
const sayHello = (variables) => {
  return `hello ${variables.name}. You are ${variables.age} years old and you birthday is on ${variables.birthdate}.`
};

let result = sayHello({
  name: 'brian',
  age: '31',
  birthdate: 'feb 19'
});

console.log(result);
```
- object can be set as a variable too: 
```javascript
const sayHello = (variables) => {
  return `hello ${variables.name}. You are ${variables.age} years old and you birthday is on ${variables.birthdate}.`
};

const templateVars = {
  name: 'brian',
  age: 31,
  birthdate: 'feb 19'
};

let result = sayHello(templateVars);
console.log(result);
```
- to implement this to res.render:
    - res.render -> html -> browser
```javascript
app.get('/', (req, res) => {
  const templateVars = {
    name: 'brian',
    age: 31,
    birthdate: 'feb 19'
  };

  res.render('user-profile', templateVars);
})
```
```html
<body> 
  <div>
    <h2>Hello <%= locals.name %></h2>
    <p>You are <%= locals.age %> years old and were born on <%= locals.birthdate %></p>
  </div>
</body>
```
