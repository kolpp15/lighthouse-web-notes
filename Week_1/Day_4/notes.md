# Day 4 Notes

## Execution
- it's best practice to always print out the labels when testing: 
```javascript
console.log('sayHello:', sayHello);
```
- tip: all functions have .toString():
```javascript
console.log('sayHello:', sayHello.toString());

console.log('console.log:', console.log.toString());
```

## Callback
- a function that gets passed to another function to be invoked by that second function:
  - runMe runs through sayHello function

```javascript
const runMe = function(callback) {
  callback('Elise');
};

const sayHello = function(name) {
  console.log(`hello there ${name}`);
}

runme('George'); //this will not work because it's a string
runMe(sayHello);
```
```javascript
const runMyFunction = function(callback) {
  // console.log(callback.toString());
  callback('Elise');
}

const sayHello = function(name) {
  console.log('Hello, ', name);
}

runMyFunction(

  function(name) {
    console.log(`bonjour! ${name}`);
  }
);
```
Best Practice:
- Step 1: 
```javascript
runMyfunction();
```
- Step 2: 
```javascript
runMyFunction(function(){});
```
- Step 3: 
```javascript
runMyFunction(function(){
  console.log();
});
```
- Step 4: 
```javascript
runMyFunction(function(name){
  console.log('Hola Amiga! ', name);
});
```

## Arrow function
```javascript
const runMyFunction = function (callback) {
  callback('Elise');
};

runMyFunction( arg1 => console.log(arg1) );
```

```javascript
// const sayHello = function(name) {
//   return `hello there ${name}`;
// };

const sayHello = name => `hello there ${name}`;

const result = sayHello('Tommy!');
console.log('Result:', result);
```

## Looping
```javascript
const animalNoises = ['a', 'b', 'c', 'd']

const forEach = (arr, action) => {
  console.log('this is our version:');
  for (const element of arr) {
    action(element);
  }
};

animalNoises.forEach((animalNoise) => {
  console.log(`the animal says "${animalNoise}"`);
});

forEach(animalNoises, animalNoise => console.log(`the animal says "${animalNoise}"`));

```

## Mapping
```javascript
const animalNoises = ['a', 'b', 'c', 'd']

const ourMap = (arr, callback) => {
  for (const elemeent of arr) {
    const returnVal = callback(element);
    output.push(returnVal);
  }
  return output;
};

const mappedArray = ourMap(animalNoises, (animalNoise) => {
  return `only the best animal say ${animalNoise}`;
});

// execution:
// step 1: console.log('animalNoises:', animalNoises);
// step 2: console.log('mappedArray:', mappedArray);
```
can also call buy because it's single line:
```javascript
const mappedArray = ourMap(animalNoises, animalNoise => `only the best animals say ${animalNoise}`);
```

there's also a builtin feature:
```javascript
const builtInMap = animalNoises.map( animalNoise => `the animal says ${animalNoise}` );
console.log('builtInMap:', builtInMap)
```

## array.filter() 

```javascript
array.filter((item) => {
  if (item % 2) {
    return true;
  }
});
```

## Arrow Functions compared: 

- Before: 
```javascript
const dragonEvents = [
  { type: 'attack', value: 12, target: 'player-dorkman'},
  { type: 'yawn', value: 40},
  { type: 'eat', target: 'horse'},
  { type: 'attack', value: 23, target: 'player-fluffykins'},
  { type: 'attack', value: 12, target: 'player-dorkman'},  
]

const totalDamageOnDorkman = dragonEvents
  .filter(function (event) {
    return event.type === 'attack'
  })
  .filter(function (event) {
    return event.target === 'player-dorkman'
  })
  .map(function(event) {
    return event.value
  })
  .reduce(function(prev, value) {
    return (prev || 0) + value
  })

  console.log('totalDamageOnDorkman\n', totalDamageOnDorkman);
  ```
- After:
```javascript
const dragonEvents = [
  { type: 'attack', value: 12, target: 'player-dorkman'},
  { type: 'yawn', value: 40},
  { type: 'eat', target: 'horse'},
  { type: 'attack', value: 23, target: 'player-fluffykins'},
  { type: 'attack', value: 12, target: 'player-dorkman'},  
]

const reduceTotal = (prev, value) => (prev || 0) + value
const totalDamageOnDorkman = dragonEvents
  .filter(event => event.type === 'attack')
  .filter(event => event.target === 'player-dorkman')
  .map(event => event.value)
  .reduce(reduceTotal)

  console.log('totalDamageOnDorkman\n', totalDamageOnDorkman);
```

