# W3D2 Notes

## CRUD
- C: Create
- R: Read
- U: Update
- D: Delete

## Bread
- B: Browse
- R: Read
- E: Edit
- A: Add
- D: Delete

## nodemon
- npm install --save-dev nodemon
- "start": ./node_modules/.bin/nodemon -L express_server.js 
  - put this into package.json "script" with the key defined as "start"

## Example 

- When testing, it's good to use a Network tab in chrome and check headers, preview, response 

```javascript
const cars = {
  abcd: {
    color: 'pink',
    model: 'corolla',
    isManual: true,
  },
  efgh: {
    color: 'purple',
    model: 'mini van',
    isManual: false
  }
};

const generateId = () => {
  return Math.foor(Math.random() * 1000) + 1;
}

// Browse // GET /cars
app.get('/cars', (req, res) => {
  // const templateVars = {  // this is to iterate over key over key
  //   cars: cars
  // }
  const templateVars = { cars } // this is equivalent 
  res.render('cars', templateVars)
});

// Read // GET /cars/:id
// this is to specify each car. In case there's hundreds of cars 
app.get('/cars/:id', (req, res) => {
  // console.log('req.params', req.params) // this will show the object
  const id = req.params.id;
  const car = cars[id]

  if(!car) {
    return res.redirect('/cars') // this will default reroute to cars page. need RETURN to stop continuting.
  }

  const templateVars = { car, carID: id }
  res.render('car', templateVars)
});

// Edit // POST / /cars/:id
app.post('/cars/:id', (req, res) => {
  const id = req.params.id; 
  const newColor = req.body.color; // the .body is the body parser added in express

  cars[id].color = newColor;

  res.redirect('/cars');
})

// Add // POST // /cars
add.post('/cars', (req, res) => {
  const newCar = req.body; 
  const newId = generateId(); 

  cars[newId] = newCar; 

  res.redirect('/cars')
})

// Delete // POST /cars/:id/delete
app.post('/cars/:id/delete', (req, res) => { // we can add this in either ejs file
  const id = req.params.id;

  delete cars[id]

  res.redirect('/cars')
})

```

```html
<!-- cars.ejs -->
<body>
  <h1>All the cars!</h1>

  <h1>Create a new car</h1>
  <form method ="POST" action="/cars">

    <label>color</label>
    <input name="color"/>
    <br />

    <label>model</label>
    <input name="model"/>
    <br />

    <label>is manual transmission</label>
    <input name="isManual"/>
    <br />

    <button type="submit">Create new car</button>


  <% for(const carKey in cars) {%>
    <div>
      <h2>color: <%= cars[carKey].color %></h2> <!-- it can't be carKey.color -->
      <h2>model: <%= cars[carKey].model %></h2>
      <h2>is manual: <%= cars[carKey].isManual %></h2>

      <a href = "/cars/><%=carKey>"> See details </a>
    </div>
  <% } %>
</body>
```

```html
<!-- car.ejs -->
<body>
  <h1>A Single Car</h1>

  <a href = "/cars">Go back to all cars!</a> <!-- this will create a hyperlink -->
  <div>
    <h2>color: <%= car.color %></h2> 
    <h2>model: <%= car.model %></h2>
    <h2>is manual: <%= car.isManual %></h2>

    <form method="POST" action="/cars/<%= carId %>/delete">
      <button type="submit">Delete Car!</button>
    </form>
  </div>

  <h2>modify car</h2>
  <form method="POST" action="/cars/<%= carId %>">
    <label>New color:</label>
    <input name="color" value="<%= car.color %>"/> <!-- this will give the current color in the form box -->

    <button type="submit">Update car</button>
  </form>

</body>
```

## EJS (Embedded JavaScript)
- Two types:
  1. `<% %>`: just for logic, non-outputting (ex. for loops)
  2. `<%= %>`: will output some javascript (ex. to show it in the browser)

## Cookies
- it's like a dogtag saving client's information such as language preference is saved uniquly for a single website. 
  - however, think about google ads. If google ad is linked to CNN website, that google ad in the CNN website will be accessible to the client's cookies and show related suggestions based on the client's interest or saved info.
  - each cookie has one unique code. Thus, websites can track unique visitors

## GIT branching
- create branch: git checkout -b `branch name`
- change branch by checkout `branch name`
- check all branches: git branch -a

## cookie-parser 
- Express middleware facilitating with cookies