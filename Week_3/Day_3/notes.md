# W3D3 Notes

## Forms
- We need at least: `<form action="" method="">`
  - What HAS to match is:
```javascript
app.post('/register-submit)
```
AND
```HTML
<form action="/register-submit">
<input name=""> <!-- this has to match with the object body (req.body) -->
<input type="password"> <!-- this will hide when inputting -->
```
- To associate the `<label>` with an `<input>` element, you need to give the `<input>` an id attribute. The `<label>` then needs a for attribute whose value is the same as the input's id. 

## Object Body
- You can check the entire object values by console logging `req.body`

```javascript
//array of objects
const user = [
  {
    username: 'brian',
    password: 'abc'
  }
];

app.post('/register-submit', (req, res) => {
  const newUser = {
    username: req.body.username,
    password: req.body.password
  }
  users.push(newUser); // this will push to the users array
  console.log('users:', user); // this is a test log if newUser has been added. This will print when new user registers
  res.render('/homepage');
});
```

## Checking Key and Values
```javascript
for (const user of users) // values
for (const user in users) // keys
```

## login Submit Handler
```javascript
app.post('/login', (req, res) => {
  for (user of users) {
    if (user.username === req.body.username && user.password === req.body.password) {
      res.cookie('user', user.username); // second paramenter: value of the user who logged in
      const templateVars = {
        user: req.body.username,
        password: req.body.password
      };
      
      res.render('profile', templateVars); // this will render the profile.ejs
      return; // we want to return because if a person successfully logs in, we want to return. 
    }
  }
  res.render('homepage'); // if loop checks all and there's no user, take back to homepage
  return;
});

app.get('/profile', (req, res) => {
  console.log('req.cookies:', req.cookies); // we need a cookieParser extension to use this.

  for (user of users) {
    if (user.username === req.cookies.user) { // if the username matches the cookie username
      const templateVars = {
        user: req.cookies.user,
        password: user.password
      };
      res.render('profile', templateVars);
      return;
    }
  }
  res.redirect('homepage'); // if for loop can't find a user
});
```

## Logout 
```javascript
app.get('/logout', (req, res) => {
  res.render('logout');
})

// from GET, if user clicks logout button, it'll POST and follow the below POST code
app.post('/logout', (req, res) => {
  res.clearCookie('user');
  res.redirect('homepage');
}
```

## How to edit cookies
- login and open developer tools
- open application and you can edit from here
