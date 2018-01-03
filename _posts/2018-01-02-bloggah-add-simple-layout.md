---
layout: post
title: Bloggah Layout I
description: "Settling the score between dynamically-typed and statically-typed languages."
modified: 2017-03-17
tags: [JavaScript, How To, Node, Express, SemanticUI]
categories: [How To Node | Bloggah |]
---
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.13/components/button.min.css" />
<h1>Adding Semantic</h1>

We started our Bloggah app <a href="https://codesafk.github.io/how%20to%20node%20%7C%20bloggah%20%7C/bloggah-index/" target="_blank">here</a>

And today it's time to move on to bigger and better things.  Before we define any more routes, we need to
make our app a little more...  *aesthetically pleasing*.  Enter:

<h2>SemanticUI</h2>

I realize a lot of people are committed to Bootstrap, and hey, I love Bootstrap as much as the next guy.  But, SemanticUI solves one of
the only problems I have with Bootstrap.  *Semantics* (See what they did there?  Brilliant).  Using Bootstrap defaults we'd style
a button like:

{%highlight html%}
   <button type="button" class="btn btn-dark">Dark</button>
 {%endhighlight%}
 
 Which would give us something like: 
 
 <button type="button" class="btn btn-dark">Dark</button>
 
 Notice the awkward syntax?  It's not that it isn't there, it's just that we're so used to using it.  ```btn btn-dark ```
 
 {%highlight html%}
    <button class="ui secondary button">Dark</button>
  {%endhighlight%}
  
  See?  Easier, human readable format.  Isn't that what this is all about?  Otherwise we'd all just code on a single line.
  Anyway, the above snippet give us:

 <button class="ui secondary button">
   Dark
 </button>
 
 Like I said, I love bootstrap.  I'm just falling in love with SemanticUI and if I fall to hard, I may not be able to come back home.
 But that's between me and Twitter, let's get to this layout.
 
 Open up app.js and add the following:
 
 {%highlight javascript%}
     //app.js
     
     app.set("view engine", "ejs");  //Should already be here...
     ...
     app.use(express.static("public"));  //This is what we're adding
   {%endhighlight%}
 
 That's going to allow us to use a public folder to link our own css.  Speaking of the public folder, we're going to need to create one of those.
 Either right-click the file tree and create a folder called ```public``` inside your root directory (bloggah) or do it **pro-style**
 from the terminal with ```mkdir public```
 
 Nice job.
 
 Now create another folder named stylesheets inside the public directory, and inside of that create an ```app.css``` file.  Terminal pros:
 
 {%highlight bash%}
     mkdir public/stylesheets
     touch public/stylesheets/app.css //tab-complete for the win!
    {%endhighlight%}
    
 We'll come back to the stylesheet in a few.  Inside your views directory create another directory called ```partials```.  Inside this 
 new folder create two files:
 
 {%highlight bash%}
      mkdir views/partials
      touch views/partials/header.ejs
      touch views/partials/footer.ejs
 {%endhighlight%}
 
 ***Note the ```ejs``` file extension***.
 
 Open up the header and place the following:
 
 {%highlight html%}
 //header.ejs
       <html>
         <head>
             <title>Bloggah</title>
             <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.13/semantic.min.css" />
             <link rel="stylesheet" href="/stylesheets/app.css"/>
         </head>
         <div class="ui fixed inverted menu">
             <div class="ui container">
                 <div class="header item">
                     <i class="code icon"></i>Bloggah
                 </div>
                 <a href="/" class="item">Home</a>
                 <a href="/posts/new" class="item">New Post</a>
                 <a href="/about" class="item">About</a>
             </div>
         </div>
       <body>
  {%endhighlight%}  
  
  Now the footer.ejs:
  
  {%highlight html%}
   //footer.ejs
         <script src="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.13/semantic.min.js"></script>
         </body>
     </html>
    {%endhighlight%}  
  
  Annnnnd.... Let's take a quick little jog over to our index.ejs file:
  {%highlight html%}
   //index.ejs
       <% include ./partials/header %>
            //content
        <% include ./partials/footer %>     
    {%endhighlight%}  
  
  
  We're loading the partials, because it will help keep everything neat later, so we don't have to repeat so much code.
  
  We'll add the ```<% include ./partials/footer %>``` and ```<% include ./partials/header %>``` to every ejs file from here
  on out.  Which technically is repeating ourselves, but not as bad.  This way, if we need to change something in the header file,
  we only do it **once**.  And that's important, because there's coffee to buy and arenas to run.
  
  One last thing about SemanticUI vs Bootstrap.  If you only want the a certain element, there's a cdn for that.  So you don't have to load the entire 
  library if you don't need it.  Lighter files, faster world.  
  
  We're killing this!  (You're doing awesome!)
  
  <h3>{CodesAFK}</h3>      

      