---
layout: post
title: Bloggah Adding Views
description: "Adding Views to our Bloggah application"
modified: 2017-03-17
tags: [JavaScript, How To, Node, Express, SemanticUI]
categories: [How To Node | Bloggah |]
---

<h1>A room with a view...</h1>

Welcome back friends to our third installment of the 'Bloggah' application.  Last time we added our header and footer
partials and SemanticUI <a href="https://codesafk.github.io/how%20to%20node%20%7C%20bloggah%20%7C/bloggah-add-simple-layout/">here</a>.
Now it's time to start knocking out our views.

From terminal because we're pros:

{%highlight bash%}
  havick@whiskey-jack bloggah]$ mkdir views  
  havick@whiskey-jack bloggah]$ touch views/new.ejs 
  havick@whiskey-jack bloggah]$ touch views/edit.ejs 
  havick@whiskey-jack bloggah]$ touch views/show.ejs 
  havick@whiskey-jack bloggah]$ touch views/about.ejs 
{%endhighlight%} 

As always, note the ```.ejs``` extension on the view files.

Now that we have the pages made, let's open up app.js and start defining some routes...

Just below the ```app.get('/')``` and ```app.get('/posts')``` routes, place the following for ```new``` route:
{%highlight javascript%}
  //app.js
  
  //NEW POST ROUTE
  
  app.get('/posts/new', function(req, res){
      res.send("You've hit the new post route!");
  });
  
{%endhighlight%} 

Don't worry, we'll change what it does soon.  Even though we're making a simple blog application, it's much easier
to fix errors if you take small steps.  Now, fire up that server with ```node app.js``` from your command line.

When you first visit your local host, you should see the index page with our one post that we created last time.
Find your way up to the address bar and edit the url to end with ```/posts/new```.  You should see a single line at
the top of the page that says "You've hit the new post route!"  If you see that, then we're good!  Common errors that 
you'll find here are ```Cannot get /posts/new```.  Normally this is due to how we set the route up.  If you have this
error, make sure you entered the route in ```app.js``` correctly.  Of specific importance is the bit between the 
parenthesis.  

We don't want our users to see that disgusting ```res.send``` message, that's not going to win friends and influence people.
We want them to see our new post form.  Back to app.js, and change that res.send to:

{%highlight javascript%}
  //app.js
  
  //NEW POST ROUTE
  
  app.get('/posts/new', function(req, res){
      res.render("new");
  });
  
{%endhighlight%}

Open up ```views/new.ejs``` and put an ugly h1 element at the top that says something to the effect of "New Post".
Restart the server, because we changed app.js, and edit the url again to visit the ```posts/new``` route.  Now you 
should see the page with the h1 element that you created a second ago.  Nice.

A lonely h1 element isn't going to get it done.  Let's add a form.  In views/new.ejs:

  {%highlight html%}
    <% include ./partials/header %>
    
    <div class="main ui segment container center">
        <div class="ui huge header">New Post</div>
        <form class="ui form" action="/posts" method="POST">
            <div class="field">
                <label for="Title">
                    <input type="text" name="post[title]" placeholder="Title" required>
                </label>
            </div>
    
            <div class="field">
                <label for="Image">
                    <input type="text" name="post[image]" placeholder="Image Url" required>
                </label>
            </div>
    
            <div class="field">
                <label for="Post">
                    <textarea name="post[body]" placeholder="Post goes here..." required>
    
                    </textarea>
                </label>
                <input type="submit" class="ui green big basic button">
            </div>
    
    
    
    
        </form>
    </div>
    
    <% include ./partials/footer %>
    
  {%endhighlight%} 

Much better.  Although our form looks okay, it doesn't do anything.  Let's fix that next.  Open up app.js again and
let's get that ```POST``` route going.

{%highlight javascript%}
  //app.js
  
 // CREATE POST
  
  app.post('/posts', function(req, res){
      res.send("Hit that post route yo!");
  });
  
{%endhighlight%}

Just like before, restart the server.  Visit ```/posts/new``` and submit the form.  You should see our clever,
totally not outdated, message.  Now let's figure out exactly what we're doing.  

What do we want to do when we submit the form?  Create a post.  Got it.  Let's run back over to app.js and see if that's possible.

{%highlight javascript%}
  //app.js
  
 // CREATE POST
  
  app.post('/posts', function(req, res){
     Post.create(req.body.post, function(err, newPost){
             if(err){
                 console.log(err);
                 res.render("new");
             } else {
                 res.redirect("/posts")
             }
         });
     });
  
{%endhighlight%}

For now, we'll redirect to the ```/posts``` route, later we'll change that to the show page.  Speaking of the show
page...  Open that up and let's lay that out.

{%highlight html%}
  //views/show.ejs
 <% include ./partials/header %>
 
 <div class="main ui segment container">
     <div class="ui huge header"><%= post.title %></div>
     <div class="ui attached ">
         <div class="item">
             <img class="ui centered rounded image" src="<%= post.image %>">
             <div class="content">
                 <%= post.created.toDateString() %>
             </div>
             <div class="description postContent">
                 <%- post.body %>
             </div>
         </div>
     </div>
 </div>
 
 <% include ./partials/footer %>
  
{%endhighlight%}

Not so terrible.  This will be the page that we see when we want to view an entire post.  But that isn't going to 
do us a lot of good right now.  Why?  Because there isn't a route for that.  Let's solve that problem now.
Back in ```app.js```

{%highlight javascript%}
  //app.js
  
 // CREATE POST
  
  //  SHOW ROUTE
  
  app.get("/posts/:id", function(req, res){
      Post.findById(req.params.id, function(err, foundPost){
          if(err){
              console.log(err);
              res.redirect("/posts");
          } else {
              res.render("show", {post:foundPost});
          }
      });
  });

  
{%endhighlight%}

In the above snippet, there's a lot going on.  We're finding the post we want to show via a built in method from 
mongoose called ```.findById(req.params.id)```.  The request that's sent to our get request contains the post id,
and we're sending that to the method as an argument.  If it finds the post, it's going to render the show page
with the foundPost as an object.  This is what allows us to reference the attributes of the post (i.e. author) in the 
show page.  Sweet!

You should be proud, we're definitely getting it done.  In our next installment we'll setup our edit and delete routes.
Then we'll fix the secret security flaw we have right now.  

I believe in you.

~CodesAFK
