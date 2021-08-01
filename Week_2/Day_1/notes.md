# W2D1 Notes

## Export and test file

Exporting file (hello-world.js):
```javascript
// implement a function called sayHello that takes the name of the saluted and returns 
const sayHello = (name) => {
    let output = '';
    output = `Hello, ${name}`;
    return output;
};

const sayGoodbye = (name) => {
    let output = '';
    output = `Goodbye, ${name}`;
    return output;
};

//console.log(sayHello('Production Development Environment!')); //optional 

// make the functions exportable
module.exports = {
    monkeyFuzz: sayHello,
    goodBye = sayGoodbye
}

// can also directly export: 
// module.exports = sayHello 
```

Test file (test-hello-world.js): 
```javascript
const assert = require('assert'); // npm node
const functions = require('./hello-world');
// DIRECT EXPORT: const sayHello = require('./hello-world'); 

const returnValue = functions.monkeyFuzz('little friend.');
console.log('returnValue:', returnValue);
assert.equal(returnValue, 'Hello, little friend.');
```
- same directory: ./
- one up directory: ../

## Mocha test runner

- mocha test file (hello-world.test.js)
```javascript
const functions = require('../hello-world');
// const assert = require('assert'); //assert is a node assertion library. If we use Chai, we need to require chai assertion library
const assert = require('chai').assert 

//first is a string, second is a callback function
describe('test the hello and goodbye communication functions', () => { 
    
    it('should test sayHello', () => {
        const returnVal = functions.monkeyFuzz('Monkey!');
        assert.equal(returnVal, 'Hello, Monkey!');
    });

    it('should test sayGoodbye', () => {
        const returnVal = functions.sayGoodbye('Donkey!');
        assert.equal(returnVal, 'Goodbye, Donkey!');
    });

});
```
- To run mocha, have to specify the direcory in the command line
- adding .test in the file name will automatically pickup all the test files in the test directory (ex. hello-world.tes.js)

## Technical Interview #1
1. Define falsy and truthy in javascript
2. Difference between == and === in javascript
3. fix or improve in a given sample code: 
    - use === instead of ==
    - use {} after the if statement
    - use for...of statement
4. Comments:
    - Logic building takes time. It's more important than learning the language. Takes about 6-9 months 