# W4D2 Notes

## Window
- each browser tab have window API that we can interact with 
  - `window.`
  - `window.history` : tap history 
  - `window.navigator`: 
  - `navigator.geolocation.getCurrentPosition((data) => console.log(data))`: this is to find out how we get the user location
  - `navigator.getBattery()`
  - `window.document`: represents the DOM 

## DOM 
- HTML is read by the browser and turned into the DOM
- DOM is a "tree" data structure

## Logging through browser
- console.dir()
  - `console.dir(document)`: discloses the object 

## Grabbing elements from browser using Javascript 
- document.getElementById('main-list')
  - we bet back from the html
  - then we can set a variable and add onto it
    - ul = document.getElementById('main-list')
    - const node = document.createElement("li");
    - const textnode = document. createTextNode("Water");
    - node.appendChild(textnode);
      - this will add Water as a child in an `<li>` format

## JQuery
- always download from: cdnjs.com/libraries/jquery
  - instead of downloading locally, simply copy and paste the url 
- `$ === jQuery` 
- Difference: 

```javascript
document.getElementById("main-list").appendChild(li);
id = "myList"

// this can be used by jQuery 
const $mainList = $('#main-list') // grab from ID 
$mainList.addClass('danger'); // grabs from the class 

setTimeout(() => {
  $mainList.removeClass('danger'); // deletes a class after 3 seconds
}, 3000);
```
- give back DOM node wrapped up with jQuery elements 
- add $ infront of the variable name as it indirectly tells that it's using jQuery

## DOM Events
- there's TONs of DOM events. checkout MDN 
- Adding Event Handling:: 
```javascript
const $h1 = $('h1'); // grab h1 direct descendent of body 
$h1.on('click', () => { // takes two arguments asynch
  console.log('hey the h1 got clicked on')
} ); 

$mainList.on('mousemove', (event) = {
  console.log(event); // this is wrapped up with all the jQuery. Thus we can be more specific 
})

const $searchTermInput = $('#input-field'); // grabbing the ID from HTML
$searchTermInput.on('keypress', (event) => { // whenever user presses a key, callback fires
  console.log(event) 
  console.log(event.target.value) // this will specify jQuery object. It'll only show the value
})

```
- with jQuery, we can grab everything we need. No need for forms to be submitted 
- try these for $.on: 
  - keypress
  - keydown
  - keyup
  - change

## Document Ready
- document ready is a special event that occurs when the document is fully loaded 
```javascript
// MAKE SURE ALL INFO ARE TABBED IN 
$(document).ready(() => { // if Document is ready, callback
  const $h1 = $('h1'); // grab h1 direct descendent of body 
  $h1.on('click', () => { // takes two arguments asynch
    console.log('hey the h1 got clicked on')
  } ); 

  $mainList.on('mousemove', (event) = {
    console.log(event); // this is wrapped up with all the jQuery. Thus we can be more specific 
  })

  const $searchTermInput = $('#input-field'); // grabbing the ID from HTML
  $searchTermInput.on('keypress', (event) => { // whenever user presses a key, callback fires
    console.log(event) 
    console.log(event.target.value) // this will specify jQuery object. It'll only show the value
  })  
})
```
- You can put all functions inside document.ready. Then, everything will load first then start calling the callbacks.
- Recommendation: 
  - Put the jQuery in the head
  - put script src at the bottom 
    - since we'll be working as a team, put all scripts inside document.ready. In case, other DEV does not put the script at the bottom. 


## Dynamic form
```javascript

const $newItemInput = $('#input-field'); // pull out from the ID 
const $button = $('#add-new-item');

$button.on('click', () => {
  // step 1: get the value from the input field 
  const newVal = $newItemInput.val(); // retrieving 

  // const $newLi = $('li'); // this SEARCH
  const $newLi = $('<li>'); // this CREATES 
  $newLi.text(newVal); // this will ADD text in the node 

  // we can CHAIN jQuesry. This is preferrable. You can continue chaining 
  const $newLi = $('<li>').text(newVal);

  // Simpler way
  const $newLi = $(`<li>${newVal}</li>`);

  // not limited to one. You can just ADD directly 
  const $funStuff = $(`
    <div> 
      <form action = "" method = "GET">
        <label></label>
        <input />
      </form>
    </div>
  `);

  $('body').append($funStuff);


  // ******* THIS WILL APPEND & ADD DYNAMICALLY *******
  $mainList.append($newLi);

  // clears the input field and mouse focus inside the box automatically
  $newItemInput.val('')
  $newItemInput.focus();
  $newItemInput.val('').focus(); // ONELINE

})

```