# Day 3 Notes

## Objects
- to return keys of objects: 
```javascript
//Sample 1
const person = {
  firstName: 'Brian',
  lastName: 'Sohn',
  age: 77,
  isTall: false,
  '1': 1,
  '2': 2
}

for (const key in person) {
  // console.log('key in person is:', key)
  console.log('key:', key, 'value', person[key])
}
``` 
```javascript
//Sample 2
const planetMoons = {
  mercury: 0,
  venus: 0,
  earth: 1,
  mars: 2,
  jupiter: 67,
  saturn: 62,
  uranus: 27,
  neptune: 14
};

for (let planet in planetMoons) {
  let numberOfMoons = planetMoons[planet];
  console.log(`Planet: ${planet}, # of Moons: ${numberOfMoons}`);
}
```
```javascript
//Sample 3
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(`${property}: ${object[property]}`);
}
```

- object keys are strings so when using square brackets, always use "". ex) 
```javascript
const person = { firstName: "Brian" };
const firstName = person["firstName"];
```
- to change object value, do this: 
```javascript
const person = { firstName: "Khurram" };
person["firstName"] = "Brian";

console.log(person["firstName"]);
```

- Example of two ways of specifying the same value in an object literal: using a literal string for the value, or using a variable: 
```javascript
const spam = "spam";

const person = {
  name: "Paul",
  address: {
    street: "310 W 95th",
    city: "New York",
    zipCode: 10027
  },
  phoneNumbers: 7783230852,
  dislikes: {
    food: spam,
    email: "spam"
  }
};

console.log(person.dislikes.email);
```

- Inspecting an object's keys by using Object.keys(...): 
```javascript
const spam = "spam";

const person = {
  name: "Paul",
  address: {
    street: "310 W 95th",
    city: "New York",
    zipCode: 10027
  },
  phoneNumbers: 7783230852,
  dislikes: {
    food: spam,
    email: "spam"
  }
};

console.log(Object.keys(person.address.city));
// returns an array of index numbers 
```

## Loop

```javascript  
for (const value of creatures) {
  console.log('the crreature is', value)
}
// is the same as 

for (let i = 0; i < creatures.length; i++) {
  console.log('the creature is', creatures[i])
}
```

### Instructor Github
https://github.com/jcbain/ 
