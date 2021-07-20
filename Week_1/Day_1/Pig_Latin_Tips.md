# Pig Latin tips




```javascript
//---------- help from Andrew
const args = process.argv;
const argsNew = args.slice(2);

const pigLatin = function(array) {
  let result = '';

  for (let i = 0; i < array.length; i++) {
    result += array[i].slice(1);
    result += array[i][0] + "ay ";
  }
  return result;
}
console.log(pigLatin(argsNew));

//--------- Solene's code
const args = process.argv.slice(2);
  
const pigLatin = args => {
  let newSentence = '';

  for (let arg of args) {
    arg += arg[0];
    newSentence += arg.slice(1) + 'ay ';
  }
  console.log(newSentence);
};

pigLatin(args); 

//--------- Tim's code
const args = process.argv.slice(2);
let output = "";
for (let e of args) {
  let firstLetter = e[0]
  output += e.substring(1) + firstLetter + "ay ";
};
console.log(output);
```
