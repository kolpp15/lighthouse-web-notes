# process.argv tips

Using `process.argv` & `.slice` to reverse a string in a command line args.


```javascript
const args = process.argv;

args.slice(2).forEach(function(reverseMe) {
  let reversed = '';

  for (let i = reverseMe.length - 1; i >= 0; i--) {
    reversed += reverseMe[i];
  }
  console.log(reversed);
});
```
