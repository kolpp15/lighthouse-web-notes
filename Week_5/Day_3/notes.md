# W5D3 Notes

## Connecting to database
- first `npm install pg`
```javascript
const pg = require('pg');
const Client = pg.Client;

const configObj = {
  user: 'postgres',
  host: 'localhost',
  database = 'spot',
  password: 'postgres',
  port: '5433'
}

const client = new Client();

client.connect()
.then(() => {
  console.log('db connected');
})
.catch((err) => {
  console.log('db connection error:', err.stack);
});

const verb = process.argv(2);

switch (verb) {
  case 'browse':
    cleint.query('SELECT id, question FROM objectives ORDER BY id;')
    .then((response) => {
      console.log('response.rows: ', response.rows);
      client.end();
    })
    .catch((err) => {
      console.log('db browse query error:', err.stack);
    });
    break;
  case 'read':
    const id = process.argv[3];
    cleint.query(`SELECT * FROM objectives WHERE id = $1;`, ${id};)
    .then((response) => {
      console.log('response.rows: ', response.rows);
      client.end();
    })
    .catch((err) => {
      console.log('db read query error:', err.stack);
    });
    break;
  default:
    console.log('please enter a recognized verb: browse, read, ...');
    client.end();
}
```
Using Express Version to connect to the Database
```javascript
// Express Version
const express = require('express');
const app = express();
app.set('view engine','ejs');

const dbFns = require('./db/queries');

app.get('/', (req,res) => {
  dbFns.getAllObjectives((rows) => { // callback getting rows from the database query call sent as a parameter. REFER TO THE queries.js
    res.render('home', {rowarray: rows});
  });
});

const port = process.env.PORT || 7887;
app.listen(port, () => {
  console.log(`Server is listening on port=${port}`);
});
```
CREATE a .env file to save privacy info and not be public on git repo. upload only an empty env.example
```javascript
DB_USER=postgres
DB_HOST=;pca;jpst
DB_NAME=spot
DB_PASS=postgres
DB_PORT=5433
```

```javascript
//queries.js for the express server

// first downlowd 
requie('dotenv').config(); // this will pull out from .env file
const pg = require('pg');

const Client = pg.Client;

const configObj = {
  user: process.env.DB_USER,
  host: process.env.DB_HOST,
  database = process.env.DB_NAME,
  password: process.env.DB_PASS,
  port: process.env.DB_PORT
}

const client = new Client();

client.connect()
.then(() => {
  console.log('db connected');
})
.catch((err) => {
  console.log('db connection error:', err.stack);
});

// (rows) => {res.render('home', {rowarray: rows}); // REFERRING TO THE SERVER line
const getAllObjectives = (cb) => {
  cleint.query('SELECT id, question FROM objectives ORDER BY id;')
    .then((response) => {
      // console.log('response.rows: ', response.rows);
      cb(response.rows);
      client.end();
    })
    .catch((err) => {
      console.log('db browse query error:', err.stack);
    });
};

module.exports = {
  getAllObjectives
}
```

```html
<!-- lastly, create an ejs to show on the browser -->

<body>

  <tr>
    <th>ID</td>
    <th>QUESTION</td>
  </tr>
  <tbody>
    
  </tbody>

  <%
  rowarray.forEach((item) => {
  %>
  <tr>
    <td>
      <%= item.question %>
    </td>
    <td>
      <%= item.id %>
    </td>
  
<%= item.question
JSON.stringify(item) %>
  <%
  })
  %>
</body>


```
