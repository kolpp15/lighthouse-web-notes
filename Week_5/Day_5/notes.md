# W5D5 Notes

## Pick a Project
- Wiki Map
- Decision Maker
- Buy/Sell

## Check the requirements 

## User Stories
- describe how and why a user will interact with our app
- `As a ___, I can ___, because ____`
  - As a logged in user, I can put pins on a map, because I want to share places of interest with my friends 
  - As a non-logged in user, I cannot edit pins on a map, because they don't belong to me
  - As a user, I can favourite a blog post, because I want to read it later AND the heart icon turns red
- Create about a dozen 

## Identify the nouns 
- nouns will be our resources. It'll be a table 
- nouns === tables
- Get reviewed from a mentor

## Routes (middleman) - routes.md
- name out the resource to ex) menu-tems, maps, item ...

- Browse: GET   /resource
- Read:   GET   /resource/:id
- Edit:   POST  /resource/:id
- Add:    POST  /resource
- Delete: POST  /resource/:id/delete

- IF AJAX:
  - Browse: GET        /resource
  - Read:   GET        /resource/:id
  - Edit:   PUT/PATCH  /resource/:id
  - Add:    POST       /resource
  - Delete: POST       /resource/:id/delete

## WIREFRAMES/MOCKUPS
- General layout 
- minimal, modern
- balsamiq, moqups, draw.io, pen/paper
- Steal the design

## Planning folder 
- create a .md file and share with the member

## Features
- If not going to demo, don't build it

## Git Merge
- branch merge to master: updating into the main
- master merge to branch: pulling other's updates to mine
- If there's a conflict, for example working together in a single file, 
- 2 options:
  1. merge locally, then push
  2. merge in the cloud, then pull
- general flow:
  1. checkout branch
  2. work on branch
  3. commit frequently
  - General flow
  4. checkout master 
  5. pull the latest master (to be up to date)
  6. merge my branch into master
  7. push to github
  - IF there's a master update while working: 
  4. checkout master
  5. pull master
  6. checkout my branch
  7. merge master into my branch 

## MVP
- Minimum Viable Product
- Minimum Viable Demo (5 min)

## User Login/registeration
- DON'T DO THIS
- Do this: 
```javascript
// ex) localhost:3000/login/7
app.get('/login/:id', (req, res) => {
  // session cookies
  res.cookie('user_id', req.params.id);
  //cookie parse
  res.cookie('user_id', req.params.user_id);

  res.redirect('/');
})
```

## Tech Stack
- Front End: HTML/CSS/JS/jQuery/SCSS
- Back End: node/express/postgres

## SPA (Single Page App) vs. multi-page

## Splitting up the work
1. Vertical - each team member is working on a diff part of the stack
2. Horizontal - each team member is working on the same layer 
3. Pair programming 

* how familiar and comfortable: HTML, CSS, JS
* Make it work first with minimum features. Add on as stretches
* Setup meeting times
* vertical or horizontal work  


