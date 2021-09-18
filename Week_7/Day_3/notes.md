# W7D3 Notes

## Spread Operator
```javascript
const user = {
  name: 'Alice',
  age: 40,
  snacks: ['pretzels']
}

//spread operator
const copy = {
  ...user,

  snacks: [
    'Doritos',
    ...(user).snacks
  ]
};

console.log('user:', user); // user: { name: 'Alice', age: 40, snacks: ['pretzels'] }
console.log('copy:', copy); // copy: { name: 'Alice', age: 40, snacks: ['pretzels', 'Doritos'] }
```

## Array methods
- these do not change the original but create a new array. Use these from now on instead of .slice() etc. :
```javascript
const newArr = array.filter();
const newArr = array.slice();
const newArr = array.concat();
const newArr = array.map();
```

```javascript
const [numbers, setNumbers] = React.useState([1, 2, 3]);

// for set states, ALWAYS do a DEEP copy and create a new array by not altering the original
setNumbers((prevNumbers) => {
  const newState = [...prevNumbers, 4];

  //previous state is not affectedd
  console.log(prevNumbers); // [1, 2, 3]
  console.log(newState);    // [1, 2, 3, 4]

  return newState;
});

```

## Component Creation Steps
- Create a file with the component name
- Create & Export the component function
- Add the base HTML in the return statement of the component
- Create & Import a CSS/SCSS file holding the style of the component
- Write stories for Storybook to render components in isolation
- Refactor the hardcoded content to use props & state