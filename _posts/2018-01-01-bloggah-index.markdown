---
layout: post
title: Bloggah Index and Initial Setup
description: "Settling the score between dynamically-typed and statically-typed languages."
modified: 2017-03-17
tags: [JavaScript, How To, Node, Express, SemanticUI]
categories: [How To Node | Bloggah |]
---

<h1>How To: The 'Bloggah'</h1>

**Index and Inital Setup**

Today we're going to start a Fullstack project called 'Bloggah'(In case you hadn't guessed that yet!)
I'm going to assume that you already have npm and mongod(for mongoDB) installed on your machine.  If not, you can find install directions relative 
to your machine <a href="https://nodejs.org/en/download/" target="_blank">here</a>(npm) and
<a href="https://nodejs.org/en/download/" target="_blank">here</a>(mongoDB).  Mongod needs to be running in a terminal instance
the entire time we're working on this or the database portion of our app will break (so basically, unless you want to display blank pages... install the dependencies.)
 <!--more-->

The stack:
  <ul>
    <li>MongoDB</li>
    <li>Node.js</li>
    <li>Express.js</li>
    <li>SemanticUI</li>
  </ul>
  
 First things first, open up your favorite IDE (or unfold your table napkin) so you can follow along.
 I'll be using WebStorm made by the fine folks over at <a href="https://www.jetbrains.com" target="_blank"> JetBrains</a>.
 
 I know, I know, it's a *gasp*** paid IDE**, but in my honest opinion, worth every penny.  And no, I'm not 
 sponsored by them.  I'm just a dirty little fanboy.  Anyway, like I said, pick any editor you feel comfortable with.  Except Eclipse.
 Don't be that guy.
 
 Alright, you've fired up the electric Internet machine and you're ready to roll.  What's first?  
 
 Open up your terminal and cd to where ever you keep your development stuffs.

 We're going to make the directory for our project(and cd into it):
 
 {%highlight bash%}
   havick@whiskey-jack]$ mkdir bloggah
   havick@whiskey-jack]$ cd bloggah
   havick@whiskey-jack bloggah]$  
 {%endhighlight%}
 
 My terminal might look different than yours.  I use a version of Arch Linux with KDE, because I have an elitist complex.
 
 Now that we're in our directory we'll use ```npm init``` to generate the package.json file for us.
 Answer or press Enter for each of the prompts, and enter 'y' at the end to confirm.  Anything that you aren't interested in 
 tracking/using, just leave it blank and pres enter.  When you're done, the confirmation should look like this:
 
 {%highlight bash%}
    
    About to write to /home/havick/Code/Websites/bloggah/package.json:
    
    {
      "name": "bloggah",
      "version": "1.0.0",
      "description": "Blog application built with SemanticUI, Node, and Express",
      "main": "app.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "repository": {
        "type": "git",
        "url": "GithubRepoGoesHereYo"
      },
      "keywords": [
        "Node.js",
        "CodesAFK",
        "Express.js",
        "SemanticUI",
        "Boston"
      ],
      "author": "Dave Mars (CodesAFK)",
      "license": "ISC",
      "bugs": {
        "url": "https://github.com/CodesAFK/bloggah/issues"
      },
      "homepage": "https://github.com/CodesAFK/bloggah#readme"
    }
    
    
    Is this ok? (yes) y

  {%endhighlight%}
  
**ProTip**: 
  
  I always change index.js to app.js, because it makes me feel special.
  
  Now that ```npm init``` has worked it's magic, let's get to work.
  
  Back in terminal, type the following:
  
  {%highlight bash%}
     havick@whiskey-jack bloggah]$ npm install express mongoose body-parser ejs --save  
   {%endhighlight%}
 
 We'll use express for our backend/routing.  Mongoose is a tool we're going to use to communicate
 with our MongoDB inside of our app.js file.  Body-parser is another tool we're going to
 use to retrieve data from our forms.  Finally, ejs is what we're going to use so we can name our views with the
 extension ejs.  Ejs stands for 'embedded javaScript' and it essentially allows us to use Javascript inside our html files.
 
 From terminal or from your IDE go ahead and create the app.js file.  For this application it needs to be in the root of 
 our base directory (bloggah).
 
 Inside app.js, we're going to declare our var(s) that we just installed with npm like this:
 
 {%highlight javascript%}
    var express    = require('express'),
        bodyParser = require('body-parser'),
        mongoose   = require('mongoose'),
        app        = express();
    const server   = 1337; //the localhost port we're using
  {%endhighlight%}
 
 In the above snippet, we're declaring express, body-parser, and mongoose as themselves (by requiring them), finally we
 declare and define express as a function through ```app = express()```.  There are other ways to accomplish the same, but
 I prefer this way, because it increases readability.  Now about that database.
 
 {%highlight javascript%}
    //app.js
    ...
    mongoose.connect("mongodb://localhost/bloggah");
 {%endhighlight%}
 
 This connects mongoose to our database.  If the db 'bloggah' doesn't exist, mongoose will dynamically create it when we 
 fire up the application via ```node app.js``` from our app directory (blogah).  Now let's set up our view engine with:
 
 {%highlight javascript%}
     //app.js
     ...
     app.set("view engine", "ejs");
   {%endhighlight%}
 This is so our application knows to parse and execute the Javascript we're about to have all up in our html.  
 
 Let's go ahead and setup what we want express to use, and give the instructions on how we want to start the server.
 
 {%highlight javascript%}
     //app.js
     ...
     app.use(express.static("public"));  //This will let us load our own CSS
     app.use(bodyParser.urlencoded({extended:true})); //This is so we can use body-parser
     
     
     
     // ============================
     //     START SERVER          ==
     // ============================
     
     app.listen(server, function(){
       console.log("Started Server on " + server);
     });
   {%endhighlight%}
   
   The ```app.listen(...)``` should be placed at the end of your file.  In other words, everything we do from here on out
   will be above that line.  Our last setup (before we start building the index route) is the schema for our db.  Before 
   my inbox blows up with hate and discontent... I know that mongoDB is a non-relational database and as such, doesn't 'need'
   a schema.  The problem is, yes it does.  We may not have to follow it exactly, but it helps if we have a few things that we
   know all posts will have.  This will also let us set up a Post model.  Add the following to our growing app.js:
   
   {%highlight javascript%}
        //app.js
        ...
        
        var postSchema = mongoose.Schema({
          title: String,
          body:  String,
          image: String,
          created: {type: Date, default: Date.now}
        });

        var Post = mongoose.model("posts", postSchema);
      {%endhighlight%}
   Here we're saying that all posts will have a title, a body, and an image of type String.  We're also setting a created 
   column with a default value of "right now".  **Pro-Tip:** We could also set a default value for the image associated with
   the post, in case we ever forgot to include one.
   
   Before we start with the routes, go ahead and create a view directory inside the root directory of our application.  
   Inside that folder, create a file named 'index.ejs'.  Open the file, and place the following:
   
    {%highlight javascript%}
        //index.ejs
        <% posts.forEach(function(post){ %>
          <h2><%= post.title %></h2>
            <img src="<%= post.image %>" alt="" height="175px" width="auto">
          <p><%= post.created %></p>
          <p><%= post.body %></p>
        <% }); %>
        
    {%endhighlight%}
    
     
   Looks a bit weird, I'll admit.  But that's okay.  It should make more sense here in just a second.  Back in app.js put the
   following:
   
   {%highlight javascript%}
           //app.js
           ...
           
           Post.create(
               {
                title:"What do you know, it works!!",
                body: "Lots of good stuff here...  Lorem Ipsum is dead!!",
                image: "https://static.pexels.com/photos/261579/pexels-photo-261579.jpeg"
               }, function(err, newlyCreated){
                   if(err){
                       console.log(err)
                   } else {
                       console.log("created new post: " + newlyCreated);
                   }
               });
           // ============================
           //         GET Routes        ==
           // ============================
           
           //redirect from the root to the index page
           
           app.get("/", function(req, res){
               res.redirect("/posts")
           });
           
           //find ALL posts, and send them to the index page as 'posts'
           app.get("/posts", function(req, res){
               Post.find({}, function(err, posts){
                 if(err){
                     console.log(err);
                 }  else {
                     res.render("index", {posts:posts});
                 }
               });
           
           });

           
   {%endhighlight%}
  
  We're placing that just below our post model (created with ```var Post = mongoose.model("posts", postSchema);```)
  But before the ```app.listen(...)```.
  
  The first block is creating a new post via the create function, just pass in the arguments as an object.  **Pro-Tip:** If
  you don't comment out this section after the first time you reset your server, this function will fire every time it starts the application.
  Which means you'll have quite a bit of duplicate data.
  
  Earlier when we created the index.ejs page, you may have noticed ```<%= javascript goes here %>```
  That's the magic of ejs.  It tells the view engine that it should interpret the information between the <%= %>,
  as javascript.  If you're trying to display information, the wrap should look like <%= post.title %>.  Otherwise
  if you're writing application logic like <% posts.forEach(...) %>, you omit the '='.  Each line of Javascript must be
  wrapped in <%%> or <%=%>, otherwise the application will just think you don't know how to HTML and silently judge you for 
  that.
  
  Alright friends...  
  
  Our app.js file should now look like:
  {%highlight javascript%}
             //app.js
             var express    = require('express'),
                 bodyParser = require('body-parser'),
                 mongoose   = require('mongoose'),
                 app        = express();
             const server = 1337;
             
             mongoose.connect("mongodb://localhost/bloggah");
             app.set("view engine", "ejs");
             app.use(express.static("public"));
             app.use(bodyParser.urlencoded({extended:true}));
             
             // ============================
             //     SCHEMA                ==
             // ============================
             
             var postSchema = mongoose.Schema({
                title: String,
                body:  String,
                image: String,
                created: {type: Date, default: Date.now}
             });
             
             var Post = mongoose.model("posts", postSchema);
             
             Post.create(
                 {
                  title:"What do you know, it works!!",
                  body: "Lots of good stuff here...  Lorem Ipsum is dead!!",
                  image: "https://static.pexels.com/photos/261579/pexels-photo-261579.jpeg"
                 }, function(err, newlyCreated){
                     if(err){
                         console.log(err)
                     } else {
                         console.log("created new post: " + newlyCreated);
                     }
                 });
             // ============================
             //         GET Routes        ==
             // ============================
             app.get("/", function(req, res){
                 res.redirect("/posts")
             });
             
             app.get("/posts", function(req, res){
                 Post.find({}, function(err, posts){
                   if(err){
                       console.log(err);
                   }  else {
                       res.render("index", {posts:posts});
                   }
                 });
             
             });
             
             // ============================
             //     START SERVER          ==
             // ============================
             
             app.listen(server, function(){
               console.log("Started Server on " + server);
             });
             
     {%endhighlight%}
  Remember to comment out the ```Post.create(...)``` after firing up the server the first time, nobody like repeated content.
  Nobody likes repeated content.
  
  That starts our little masterpiece.  Tomorrow, I'll post about some simple layouts that we'll do to make our app look a
  little less terrible.  We'll also add some functionality.  
  
  We'll also be doing a fair bit of refactoring throughout this tutorial, and at the end we should have a Fullstack, fancy-pants,
  not-so-terrible-ui Node application.
  
  We got this.
  
  ~CodesAFK