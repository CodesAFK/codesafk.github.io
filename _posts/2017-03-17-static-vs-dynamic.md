---
layout: post
title: Pick Your Poison
description: "Settling the score between dynamically-typed and statically-typed languages."
modified: 2017-03-17
tags: [Java, JavaScript, General Theory]
categories: [Theory]

---

### Is your poison Static or Dynamic? 
  


Often times this comes down to a personal preference, and as with most personal preferences,
the debate can become quite heated.  First let’s discuss the differences.
(In most of these I’ll be using Javascript for the Dynamic crew, and Java as the Static crew.)

{%highlight javascript%}
  var x = 2;
  x = “hello”;
  x = 3.2567894;

  console.log(x);
  
=> 3.2567894

{%endhighlight%}

The above snippet is in Javascript (which is a dynamically typed language). 
Our variable x, is able to change types at will.  The reason that this is
legal and fair is because Javascript, and most dynamic languages, are interpreted rather
than compiled.  In common terms, you’re allowing Javascript to decide what type of variable x is.  

Take a similar snippet from Java (which is statically typed):

{%highlight java%}

String myString = “Hello”;

int x = 45;

myString = 3; //  error: incompatible types: String cannot be ... 

{%endhighlight%} 

In Java, we get a compiler error, because myString has already been declared as an int(eger).  
In statically typed languages, the ```type``` of a variable must be known at compile time.  

Which one is better?  The answer is, as it usually is in the development community…  It depends.  It’s a very
opinionated subject, often coming down to personal preferences.  

## Benefits of dynamically typed languages:


1.  **More concise**- There’s a lot of repetitive code involved in static typed languages (type declarations, typecasting logic, and the like.  Which makes it a little easier to write, but more importantly it makes code easier to read.

2.  **Hacking**- It’s easier to change.  Using techniques like monkey patching or duck typing can get you those results faster.  Be careful with double-edged swords though, as it can also confuse you.

3.  **Interactive**- Dynamically typed languages offer rapid prototyping and real time debugging.

4.  **Polymorphism**- Because of the dynamic nature of ummm…  Dynamically typed languages, they encourage polymorphism  which helps out with code reuse and increases productivity.

## Benefits of statically typed languages:

1.  **Better Design**- Statically typed forces you to think about the type of your data upfront which, in theory, leads to a better overall design.

2.  **Compile time protection**-  Static typing catches many errors at compile time. This is a huge advantage, and is arguably the best thing about statically typed languages overall.

3.  **Discourages hacks** - you have to keep type **discipline** in your code, which is likely to be an advantage for long term maintainability.


So which is better? 

#### **Statically Typed for the win!**

I think that Dynamically typed languages are more productive in the short term, without a doubt.  However, unless your test suite and your discipline is on point, maintenance becomes an issue.  Which is why I am a follower of the Static Religion.  It allows for greater productivity in the long run.  

Then again, I’m just some guy on the Internet.  

~CodesAFK~