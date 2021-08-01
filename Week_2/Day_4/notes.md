# W2D4 Notes

## PROMISE

- Example callback

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const answers = [];

rl.question('What do you think of Node.js? ', (answer) => {
  answers.push(answer);
  rl.question('What\'s your name? ', (answer) => {
    answers.push(answer);

    rl.close();
    const node = answers[0];
    const name = answers[1];
    console.log();
    console.log('Your profile is ready!!');
    console.log(`My name is ${name} and I think Node is ${node}!!`);
  });
});
```

- above callback can be a promise like below:
```javascript
const rlp = readline.createInterface
const readline = require('readline-promise').default;

const rlp = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const answers = [];

rlp.questionAsync('What do you think of Node.js? ')
  .then((answer) => {
    answers.push(answer);
    return rlp.questionAsync('What\'s your name? ');
  })
  .then((answer) => {
    answers.push(answer);
//    return rlp.questionAsync('Which sport is your absolute favourite? ');
    throw "error!";
  })
  .then((answer) => {
    answers.push(answer);
    rlp.close();
    const node = answers[0];
    const name = answers[1];

    console.log();
    console.log('Your profile is ready!!');
    console.log(`My name is ${name} and I think Node is ${node}!!`);
  })
  .catch((err)=>{
    console.log(err);
  });
```

- another example with explanation: 
```javascript
promise // promise is an object
    .then((data) => { // then is a function
        console.log('resolved!!:', data); // data is that is returned by that promise
        return 'another thing'; // 'another thing' is a string. Turns out if you return a primitive (if not a promise), promise infrastructure will wrap up so that the .then can change to further promise syntax. You don't need to return promise because you can continue on with the next .then clause. 
    })
    .then((data) => {
        console.log("monkeyfuzz:", data);
    });
```

- Promise.all() = wait for all the array to complete (wait until all of them are fulfilled)
- Promise.race() = fastest will print out

ex) 
```javascript
const one = returnPromise('one', 1500);
const two = returnPromise('two', 4000);
const three = returnPromise('three', 2000);
const four = returnPromise('four', 3000);

Promise.all(promises)
    .then((data) => {
        console.log('succes:', data);
    })
    .catch((err) => {
        console.log('something was rejeced!:', err);
    })
```

## JSON compared to a string

```javascript
const jsonString = '{"a":1, "b":2, "foo":"bar"}'; 
const obj = JSON.parse(jsonString);

delete jsonString['foo'];
delete obj.foo;

console.log(jsonString); // will print as a string 
console.log(obj); // will transform the produced value and its properties and return the value
console.log(JSON.stringify(obj)); // this will serialize it back to a string
```
