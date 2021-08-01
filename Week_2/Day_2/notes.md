# W2D2 Notes

## For..in (in an array)
- for..in in an object will give the keys
- for..in in an array will give the index value of the array
    - array is also an object

## Asynchronous 
- Synchronous will always run first and then asynchronous
```javascript
console.log('(1)')

setTimeout(() => {
    console.log('(2)')
}, 2000)

setTimeout(() => {
    console.log('(3)')
}, 1000)

console.log('(4)')

// this will run 1, 4, 3, 2
```
- Asyncronous will return first if it's inside the syncronous 
```javascript
const higherOrderFunction = (callback) => {
    const data = {
        userName: "Mulder"
    }

    console.log('1')
    setTimeout(() => {
        data.userName = "Scully"
        callback(data);
    }, 700)
    console.log('2')
}

// console.log('3');
higherOrderFunction((something) => console.log('my data', something));
// console.log('5');
// will return 3 1 2 5 4
```

## Set Interval

- setInterval() will keep on going without stopping 

```javascript 
let iterator = 0; 

setInterval(() => {
    iterator++;
    console.log('hi there', iterator);
}, 1000)
```
- clearing interval: 
```javascript
let iterator = 0; 

const returnValue = setInterval(() => {
    iterator++;
    console.log('hi there', iterator);

    if(iterator >= 10) {
        clearInterval(returnValue);
    }
}, 250)

console.log('handle', returnValue);
```

## node file systems
node file systems are built-in

- fs.readFileSync

```javascript
const fs = require('fs');

// sync readfile
const date = fs.readFileSync('./index.html', {encoding: 'utf-8'}) // this is linked to the index html file located in the same directory. fs.readFileSync will read out the index html file. utf-8 is the encoding language

console.log('sync', data);
```

- readFile is asynchronous 
```javascript
// third parameter in readFile is when there's an error. refer to (err, data)
fs. readFile('./index.html', {encoding: 'utf-8'}, (err, data) => {
    if (err) {
        return console.log(err) 
    }
    console.log('async', data);
});

console.log('hi there');
```

## print out in a single line
- instead of using console.log, use process.stdout.write

## sample process.stdin and process.stout 
```javascript
const stdin = process.stdin;
// don't worry about these next two lines of setup work.
stdin.setRawMode(true);
stdin.setEncoding('utf8');

////////////
// Event Handling for User Input
////////////

// on any input from stdin (standard input), output a "." to stdout
process.stdin.on('data', (key) => {
  if (key === '\u0003') {
    process.exit();
  }
  process.stdout.write('.');
});

console.log('after callback');
```

## Transmission Control Protocol (TCP)
- provides a standard that allows machines to speak to each other

## Definition
- Network: connection between two or more computers to communicate
- How to connect network:
    - ex 1: wireless router 
- Local Area Network (LAN): my home have 3 laptops, 1 printer. this is a LAN
    - neighbor has a different LAN
- Network Intervace Card (NIC): computers have NIC that acts as mouth and ears like human talk and hear
- Wide Area network (WAN): officce campus have different buildings. there's a bigger routers connecting each building
- MAC Address: 
    - ex) John knows that it's Mary when talking over the phone cuz of her voice
    - instead of names, computers have a unique MAC address
    - 48bits(6bytes) long: ex) 00:00:AB:13:5A:2C or 0000.AB13.5A2C 
- communicating: if there's A, B, C computers, when A sends message to B, C can listen but B replys (like 3 ppl in the room)
    - when C wants to send a message to A, if C detects that A is sending a message to B, it detects collision. 