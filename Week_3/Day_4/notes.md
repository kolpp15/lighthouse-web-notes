# W3D4 Notes

## Hashing
- Salt: added in texts
- Password: abcd
- After hashing: salt + password
- encrypt can decrypt BUT hash can't be dehashed
  - however, you can compare with the original password if it's true/false

```javascript
const bcrypt = require('bcrypt');
const plaintextPassword = 'abcd';

//hashing using asynch callback
bcrypt.genSalt(10, function(err, salt) {
  bcrypt.hash(plaintextPassword, salt, function(err, hash) {
    console.log('hash: ', hash); // testing
  })
})

//hashing using promises
bcrypt.genSalt(10)
  .then((salt) => {
    return bcrypt.hash(plaintextPassword, salt);
  })
  .then((hash) => {
    console.log('hash', hash); // testing
  });

//Now comparing with the result
const hash = '$2b$08$DjNw.rPWr4V' //this will true
const hash2 = '$2b$08$DjNw.rPWr4BB' // this will false

bcrypt.compare(('abcd', hash)
  .then(result) => {
    console.log('do the passwords match?', result);
  });

```

## Continue from yesterday's code
```javascript

const cookieSession = require('cookie-session');
const bcrypt = require('bcrypt');

// Middlewares will always run whereas routes are specific
app.use(express.urlencoded( { extended: false}));
app.use(express.static('public')); // this will read CSS files

app.use(cookieSession({
  name: 'cookiemonster',
  keys: ['my secret key', 'yet another secret key'] // having extra layers of array is for extra security
}));


//array of objects
const user = {
  brian: {
    username: 'brian',
    password: 'abc'
  }
};

app.post('/login/', (req, res) => {
  const testUsername = req.body.username;
  const testPassword = req.body.password;
  
  const user = users[testUsername];
  if (!user) {
    return res.status(401).send('No user with that username found');
  }

  bcrypt.compare(testPassword, user.password) // user.password saved as a hashed PW. Thus, we need to bcrypt.compare().
    .then((result) => {
      if (result) {
        // res.cookie('username', user.username); THIS WAS THE BEFORE COOKIE EXTENSION
        req.session.username = user.username; // first .username becomes an object of the req.session. This will change the cookie name for security issue. (CHECK INSPECT)
        res.redirect('/protected'); // if match, redirect to /protected
      } else {
        return res.status(401).send('Password incorrect');
      }
    })
})

app.post('/register', (req, res) => {
  const testUsername = req.body.username; // body is from the FORM. these are typed in by the users.
  const testPassword = req.body.password;

  bcrypt.genSalt(10)
    .then((salt) => {         // salt is just a variable name because it's a callback. It can be anything
      return bcrypt.hash(password, salt);
    })
    .then((hash) => {
      users[testUsername] = { // inside the [] will be the property(key) of the object
        username: testUsername,
        password: hash
      };
      console.log("users :", users); // this will show the hashed PW
      res.redirect('/login');
    });
});

app.get('/protected', (req, res) => {
  // const username = req.cookies.username; 
  const username = req.session.username;

  if (!username) {
    return res.redirect('/login');
  }

  const user = users[username];
  if (!user) {
    return res.redirect('/register');
  }

  console.log('users:', users);
  res.render('protected', { user });
});

// YESTERDAY's codes below: 

// app.post('/register-submit', (req, res) => {
//   const newUser = {
//     username: req.body.username,
//     password: req.body.password
//   }
//   users.push(newUser); // this will push to the users array
//   console.log('users:', user); // this is a test log if newUser has been added. This will print when new user registers
//   res.render('/homepage');
// });

// app.post('/login', (req, res) => {
//   for (user of users) {
//     if (user.username === req.body.username && user.password === req.body.password) {
//       res.cookie('user', user.username); // second paramenter: value of the user who logged in
//       const templateVars = {
//         user: req.body.username,
//         password: req.body.password
//       };
      
//       res.render('profile', templateVars); // this will render the profile.ejs
//       return; // we want to return because if a person successfully logs in, we want to return. 
//     }
//   }
//   res.render('homepage'); // if loop checks all and there's no user, take back to homepage
//   return;
// });

// app.get('/profile', (req, res) => {
//   console.log('req.cookies:', req.cookies); // we need a cookieParser extension to use this.

//   for (user of users) {
//     if (user.username === req.cookies.user) { // if the username matches the cookie username
//       const templateVars = {
//         user: req.cookies.user,
//         password: user.password
//       };
//       res.render('profile', templateVars);
//       return;
//     }
//   }
//   res.redirect('homepage'); // if for loop can't find a user
// });

// app.get('/logout', (req, res) => {
//   res.render('logout');
// })

// // from GET, if user clicks logout button, it'll POST and follow the below POST code
// app.post('/logout', (req, res) => {
//   res.clearCookie('user');
//   res.redirect('homepage');
// }

```

## REST
- HTML can ONLY process 2 verbs: GET & POST

## Sessions terminology
- Session cookies: cookies that expire after a browser is closed
- Session: encrypted cookies
- user session: 
  - login/logout features
  - event of a user using an application

