# W4D1 Notes

## Tweeter Project
- Tweeter page:
  1. feeds 
  2. message you can tweet 
  3. word count 
  4. no refresh when posting

## HTML
- responsible for contents in a webpage
- ref. MDN HTML elements reference 
  - there's all the semantic tags 
- You can have multiple siblings, but you can only have ONE PARENT
```html
<aside>
  <h2>
  <section>
    <p>
    <p>
  </section>
  </h2>
<aside>
```
  - aside is parent to `h2` and `section`. `h2` and `section` are siblings 

## CSS
- responsible for styling a webpage
- using in-html `<style>`
```html
  h1 {
    font-size: 46px;
    color: green; 
  }
  section {
    background-color: blueviolet; 
  }
  .pet-title {
    color: coral;
    font-size: 24px;
  }
  <!--to specify even more-->
  h2.pet-title {
    color: black;
  }
  #special-dog {
    border: 3px solid #ff432f;
    border-radius: 3px; 
  }
```
- from the chrome devtools, you can test it out from the styles tab and if you like, simply copy and paste
- if you want to specifically change one of the h2, simply add a class="pet-title"
  - dot is for class. # is for id

## ids 
- ID is unique per page 

## specificity
- inline > id > class > elements
- ref: polypane.app/css-specificity-calculator

## border calculation
- guyroutledge.github.io/box-model/

## CSS filing 
- it's best to have a separate CSS file to have a styles file 
- from the html page, link it by: 
- because each browser have different formatting, google copy and paste CSS reset 
```html
<link rel="stylesheet" href="reset.css"/>
<link rel="stylesheet" href="styles.css"/>
```

