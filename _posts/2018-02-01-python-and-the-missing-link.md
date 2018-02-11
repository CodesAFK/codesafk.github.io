---
layout: post
title: Python and the Missing Links...
description: "How to linked list like a pyBoss"
modified: 2018-02-03
tags: [How To, Linked List, Data Structures]
categories: [Data Structures]
---

<h1>Finding The Missing Link With Python</h1>

Clever and misleading title is cleverly misleading.  We're not actually going to be talking about 'missing' links, so much as
we are going to be talking about Data Structures in general.  Honestly, some of the concepts we discuss here may be a bit too low 
level for python.  Why talk about it in python?  Well, there's a couple of reasons.  Firstly, python is great for readability.  Which, if 
you're keeping score, makes it a fantastic choice whilst learning/refreshing about data structures.  Secondly, I'm a python fanatic, and it's my blog.
  
Maybe you're on the market for that <a href="http://www.palantir.com/engineering-culture/" target="_blank"> Unicorn</a> company, 
or just some freak who learns for themselves... Either way:

<strong>Come on in and grab a seat</strong>.  We're going to be going going over the six major data structures and what makes them cool (and not so cool).

<h1>Linked Lists...  You mean like an array?</h1>

**No**  I don't.  Linked lists are often *compared* to arrays.  But they are fundamentally different.  By fundamentally different, what I 
mean to say, is that they are competitors.  What are the primary differences?  Arrays vary in detail a bit depending on what language your working in,
but just for context, here's some universal truths:

<h2>Arrays</h2>
<li>Are *static* -- Their sizes are declared when they're created.</li> 
<li>They are sequenced -- They require a sequence of memory to be initiated</li> 
<li>They're faster to search through -- You don't have to traverse an array *in order*</li> 

That's all fine and great, but what about linked lists?

<h2>Linked Lists</h2>
<li>Are *dynamic* -- Their sizes can be changed as needed.</li> 
<li>They are not sequenced -- As long as the reference is updated the linked list node can be moved to a different memory address</li> 
<li>They use less memory -- Because their size isn't fixed, linked lists use exactly as much memory as they need.</li> 
<li>They have a linear lookup time -- It takes longer to find a node because each node in a linked list must be traversed in order.</li> 

<h2>Which one is better?</h2>

Linked list is better.  Wait, I meant Array.  No, hold on...  Neither?  The true answer as with most things in life:

**It depends**

A lot of the argument for or against linked lists is going to depend on what you're using it for.  At the end of this data structure series,
I'll be sure and give you a cheatsheet.  Because who has time to think?  Robots.  Robots have time to think.  Speaking of robots, let's 
make a linked list in Python.

Starting with a Node Class:
{%highlight python%}
  class Node:
      def __init__(self,val):
          self.val = val
          self.next = None # when we initialize we aren't pointing at anything.  
{%endhighlight%} 

Now that we have the class, we can start cranking out those beautiful Nodes:

{%highlight python%}
  node1 = Node(345) 
  node2 = Node(589) 
  node3 = Node(644) 
  node1.next = node2 # 345->589
  node2.next = node3 # 589->644
  # the entire linked list now looks like: 345->589->644->None
 
{%endhighlight%} 

What's happening up there?  We're creating three Nodes.  One with the value of 345, one with 589, and finally one with 644.  
The values aren't relevant, we could set them to what we pleased.  What's important is that we're setting both the Node value, and later the ```.next``` 

The ```.next``` is the Node that the current node is pointing to.  That was confusing.  So...  We set ```node1.next``` to be equal to ```node2```
which means that now ```node1``` **points** to ```node2```.  Since we didn't specify where ```node3``` points, it points at nothing.  Which brings our 
conga line of nodes to an end.

Let's create a method to traverse the nodes we just created:

{%highlight python%}
  class Node:
           
      def traverse(self):
          node = self # start with the node that the method is called on
          while node != None:  #as long as the node exists
              print node.val # show us the value
              node = node.next # Keep it moving...
              
{%endhighlight%} 

Values can be traversed with this method.  But there's a problem.  There's no reverse in this car...  Let's see if there's a way to fix that:

{%highlight python%}
  class DoubleNode:
      def __init__(self, val):
          self.val = data
          self.next = None
          self.prev = None
              
{%endhighlight%} 

It may seem like a small change to our Node class, but it's a big one.  By allocating another pointer (prev) we've created a linked list that can be worked on 
forwards **and** backwards.  Also, we've made the delete function more efficient.

We've also made some not so good changes.  Namely that:

<li>We need more memory -- We have an extra pointer</li> 
<li>We have more work to do -- Two pointers now have to be maintained.</li> 

<h1>Imitation is the greatest form of flattery...</h1>

Let's get our practice on.  Here's some challenges for you:

1.  Traverse a linked list

2.  Remove duplicates from a linked list

3.  Get the nth to last element from a linked list

4.  Delete a node from a linked list

5.  Add two linked lists from left to right

6.  Add two linked lists from right to left

I'll post how I would solve these and the next installment of the series tomorrow.  These aren't my challenges.  You can thank

<a href="http://www.palantir.com/engineering-culture/" target="_blank">Cracking the Coding Interview</a>.

Because that's where I got them from.  

Stay frosty...  Just don't freeze.

~CodesAFK

  