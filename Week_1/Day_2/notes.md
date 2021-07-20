# Day 2 Notes

## Fundamental Fridays
- Programming Tests
- Computer Science Topics 
- Research, Reflect & Write
<br/><br/>

## Weekly Details
- Check the curriculum slides on Compass 
<br/><br/>

## VS Code
- download Prettier ESLint
<br/><br/>

## Git
- start with main/master
- good to create a branch so that the main won't be affected
- once done and finalized, merge branch to main 
- (checkout to main before merging)
- finally, push on github
<br/><br/>

## Code example (command line)
Write a node program that takes in an unlimited number of command line arguments, goes through each and prints out the sum of them. If any argument is not a whole number, skip it. Do support negative numbers though. If any argument is not a number, output an error message. We need at least 2 arguments.
1. first write steps on comments: separate main steps and edge cases (edge cases can be done later)
<br/><br/>

2. always console log throughout the steps
```javascript
const args = process.argv; 
console.log("args:", args);
```
<br/>

3. test out slice() and splice()
```javascript
const args = process.argv.slice(2);
console.log("args:", args);
```
<br/>

4. Decide which we'll use to go through each:
- forEach
- c-style loop (better for index)
- for of (better for non-index)
```javascript 
// create an accumulator
let total = 0; 

for (let num of args) {

  const nb = Number(num);
  
  // total = total + num
  total += nb; 
  console.log("nb:", nb, "type:", typeof nb, "total:", total);
}
```
- can use Number() or parseInt() to extract numbers. 
  - parseInt() will extract a number (ex. 5hello = 5)
<br/><br/>

5. Edge cases: (1) need at least 2 arguments, (2) skip if not a whole number (3) if not a number, output an error message

```javascript
const args = process.argv.slice(2);

if (args.length < 2) {
  console.log('please enter at least 2 command-line arguments');
  process.exit(); // return or process.exit
}

let total = 0; 

for (let num of args) {

  const nb = Number(num);

  if (isNaN(nb)) {
    console.log("Please enter only numbers");
    // return or process.exit();
    process.exit();
  }

  if (Number.isInteger(nb)) {
    total += nb; 
    // console.log("nb:", nb, "type:", typeof nb, "total:", total); => this is used to test out
  }
}

console.log("Total:", total);
```
<br/>

6. Finally, wrap everything in a function so we can (1) reuse (2) it's more readible by naming it
```javascript
// takes in an unlimited number of command line arguments
const args = process.argv.slice(2);
// console.log("args:", args);
// edge case: We need at least 2 arguments. if not output an error message
if (args.length < 2) {
  console.log('please enter at least 2 command-line arguments');
  // return or process.exit();
  process.exit();
}

// return an array of converted values to number
const convertToNums = function (nums) {
  const output = [];

  for (let num of nums) {
    output.push(Number(num));
  }

  return output;
};

// Single Responsibility principle => each function should achieve a single goal

const sum = function (nums) {
  // create an accumulator
  let total = 0;

  // map => loop + transformation to each element in the array

  for (let num of nums) {

    // edge case: If any argument is not a whole number, skip it.
    // edge case: If any argument is not a number, output an error message.
    if (isNaN(num)) {
      console.log('Please enter only numbers');
      // return or process.exit();
      process.exit();
    }

    if (Number.isInteger(num)) {
      // add them up
      // total <= total + num;
      total += num;
      // console.log('num:', num, 'type:', typeof num, 'total:', total);
    }
  }

  return total;
};

const result = sum(convertToNums(args));
console.log('result:', result);
```
