# W4D3 Notes

## Folder format
- statics stay in public folder
- data in a different folder. ie json files
- requesting only data. But you can also access it by browser:
```javascript
app.get('/api/users', (req, res) => {

})
// instead of 
app.get('/users', (req, res) => {

})
```

## Starting the HTML
- always good to start with hard data and structure how it looks like 
```html
<body>
  <h2>
  <div class="post">
    <h1>title</h1>
    <h2>body</h2>
    <h3>author (userId)</h3>
  </div>

  <!-- check the server.js to see what the browser is expecting -->
  <form id="new-post-form">
    <label>Title</label>
    <input name="title" />
    <br/>

    <label>Body</label>
    <input name = "body" />
    <br/>

    <label>UserID
    <input name="userid" />
    <br/>

    <button type="submit">Create!!</button>
  </form>
  
  <!-- Step 1 to 8 in JS -->
  <div id ="posts-container"> </div>

  
</body>
```

## script.js
- Even though the script is src'd at the bottom of the HTML file, still use `$(document).ready(() => {})`
  - this is now shorted: `$(() => {})`
```javascript
$(() => {


  // --------------------------------------- STEP 6: Put the entire ajax inside a callback
  const fetchPosts = () => {
  // --------------------------------------- STEP 1: create AJAX
    $.ajax({ // THERE'S A SHORTHAND METHOD. GOOGLE AJAX SHORTHAND
      url: '/api/posts',
      method: 'GET',
      dataType: 'json',
      success: (posts) => {
        console.log(posts); // you'll be able to see the output in the devTools console. You'll see the JSON information (datatype)
        
        // const post = posts[0]; // first data in the JSON
        // const $post = createPost(post); // callback the post with ajax
        
        // // ------------------------------ STEP 3: hook it with HTML
        // const $postsContainer = $('#posts-container'); // hook with HTML
        // $postsContainer.append($post); //show it to the browser

        // --------------------------------- STEP 5: comment out all above
        createposts(posts);
      },
      error: (err) => {
        console.err(err);
      }
    });
  }

  // --------------------------------------- STEP 8: ?????
  fetchPosts();

  // PROTIP: IIFE (immediately invoked function expression) but not in this
  (() => {})()

  // --------------------------------------- STEP 7. Hook a button from HTML to run the above ajax
  $('#fetch-posts').on('click', fetchPosts); // not fetchPosts() because it's not a callback

  // --------------------------------------- STEP 2. pass the data (HTML) and make it functional. Refer to HTML Div section
  const createPost = (post) => {
    // start from bottom to top (children to parent)
    const $title = $('<h2>').text(`Title: ${post.title}`); 
    const $body = $('<h2>').text(`Body: ${post.body}`);
    const $author = $('<h3>').text(`Author: ${post.userId}`);

    const $post = $('<div>').addClss('post'); // div parent 

    $post.append($title).append($body).append($author); // add children to the parent (title, body, author TO div)
    $post.prepend($title, $body, $author); // This is the best practice. NEED prepend to show new on top
    
    return $post;
  };

  // --------------------------------------- STEP 4. create POSTS not POST (multiple)
  const creratePosts = (posts) => { // this is what we receive from the data (multiple)
    const $postsContainer = $('#posts-container'); // C&P from STEP 3. post by post
  
    // ------------------------------------- STEP 8. empty before iterating not to keep on adding on the data (duplicating div > children in this example)
    $postsContainer.empty();
    for (const post of posts) { 
      const $post = createPost(post); // create individual post of posts
      $postsContainer.append($post)
    }
  };

  // --------------------------------------- STEP 9. grab from HTML (new post)
  const $form = $('#new-post-form');
  $form.on('submit', function (event) { // when a form is submitted, CALLBACK!
    event.preventDefault(); // this will not refresh the page
    console.log('the form is submitted');
    const serializedData = $(this).serialize(); // this = submit on form
    console.log(serializedData) // this will give out the urlencoded data

    $.post('/api/posts', serializedData, (response) => { // shorthand ajax. from Google
    console.log(response); // this test should show all the responses
    fetchPosts(); // THIS ELIMINATES NEED TO REFRESH PAGE. REFER TOP FOR THIS CALLBACK
    })
  });

});
```


