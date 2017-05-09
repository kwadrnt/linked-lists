<!--
Creator: WDI Team
Last edited by: Brianna
Location: SF
-->

![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Linked Lists

### Why is this important?
<!-- framing the "why" in big-picture/real world examples -->
*This workshop is important because:*

- Data Structures are popular interview topics.  
- Linked lists are a foundational data structure - understanding them will make it easier to understand stacks, queues, trees, graphs, and hash maps.  
- The concept of a "pointer" - which stores a memory location, is common in lower-level programming languages.


### What are the objectives?
<!-- specific/measurable goal for students to achieve -->
*After this workshop, developers will be able to:*

- Describe the low-level structure of arrays and linked lists.  
- Manipulate linked lists.


### Interview question

What's the difference between a JavaScript array and a linked list?

## What are linked lists?

![linked list image from wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/640px-Singly-linked-list.svg.png)

Linked lists store sequential (ordered) data in a series of "nodes".  Each node in a linked list contains some value and a reference or "pointer" to the next node.

Every linked list has a head, which is just the first node in the list.  A linked list itself is actually just storing the head node.

The very last node of a linked list, called the tail, has a null next node because nothing comes after it.  Most singly linked lists don't store a reference directly to the tail, but it can make some operations smoother.

<img src="https://cloud.githubusercontent.com/assets/3254910/14589131/8456511c-048f-11e6-9ba3-1069f09591cd.jpg" width="300px" alt="wiggle snake toy">


## Singly Linked Lists and Arrays

#### So... linked lists are like arrays?

A little! But not 100%.  Let's step back and take a closer look at arrays. Their true nature may surprise you!

Arrays store data in one continuous block of computer memory.  The computer sets aside just enough memory when the array is created. You can think of your computer's memory as a giant city full of identical buildings. Using an array is like renting out a bunch of adjacent buildings.


![cartoon city skyline](https://cloud.githubusercontent.com/assets/3254910/14589266/b990b3a6-0492-11e6-922e-46cf0517fa64.png)


This makes it really convenient to find all the data in an array. Your computer knows where each piece of data is stored because it knows where your array's territory starts and how big each building is.  Your computer can move from one location in the array to the next about as easily as you stroll down the street.

On the other hand, your computer needs to know from the start exactly how many buildings you need -- how big the array will be. And, if you ever need more space, your computer has to find a new continuous row of empty buildings big enough for you - a new block of free memory that can fit the entire array.

**But wait! You've never had to worry about array size...**

Totally! In lower level computer programming languages like C, you *would* have to. JavaScript and Ruby handle array sizing and resizing for you efficiently. That's one of the reasons we love higher level programming languages.

But! in interviews it's good to know what's happening in the background, because that's the biggest difference between arrays and linked lists.

#### Array / Linked List Tradeoff

Creating a linked list is a bit like renting buildings all around the city, wherever it's convenient.   From there on, you just add a new building whenever you need one, wherever you can find one available. With linked lists, each building is a "node" in the list.  



<img height="350px" alt="academy of arts university map" src="https://cloud.githubusercontent.com/assets/3254910/14611060/52180c84-0545-11e6-9323-d33706d377e5.png">


In our analogy, you delegate a lot! You would know the address of the headquarters (the head or first node of the linked list). In a singly linked list, every node stores a pointer that gives the memory address of the next node. This is like letting each building manager keep track of just their address and the address of the *next* building you own.  In a doubly linked list, each node has pointers to the *next* and the *previous* node.

### Pros and Cons

**Linked lists don't need to be resized with one giant block of memory;** they can grow with pointers to other parts of the computer's memory.  You don't have to find continuous free space.

**It's easier to insert into the middle of a linked list**, because with an array you'd need to move every element after the insertion point over by one. It's easier with linked lists, as you'll see in the challenges.

On the other hand...

**You can't quickly access a particular node in a linked list, like you can with array indices.** You have to start with the head and move sequentially.

**Linked lists take up a bit more space** because in addition to storing the actual data, you have to store the pointers.  (You have to hire building managers to keep track of where the next address is!)

**It can take more time to access a full linked list,** because the data living in different places can't just be read as a continuous chunk.  You have to travel around the city to visit all of your buildings.

### Check for Understanding

1. What is the "big o" time complexity of inserting a node into a linked list after a given node?

    <details><summary>click for some info</summary>
    If we know exactly which node we're inserting after, we can just change a few nodes' `next` values.  This is O(1).

    However, if we didn't know which node to insert after, we might have to search for it based on some given data. In this case, it could take us O(n) just to find the right place before we can change around those few `next`s.  This is O(n).
    </details>

2. What is the "big o" time complexity of inserting a new value into an array at a given index?

    <details><summary>click for some info</summary>
    It depends!

    In the worst cases where we're inserting near the start of an array, we'd need to move O(n) items down a slot, increasing each of their indices by 1, to make room for the new item. This is assuming the array had enough space reserved in memory to accommodate that item.

    If we have to resize, that's O(n) to move each value to a new location.

    To combat this issue, though, arrays are implemented so that they only resize infrequently and they overestimate the new size they'll need (when addng one element to a 8-item array, the computer will acutally find space for a 16-item array).  This helps out in the case of adding an item to the end of the array (appending). The amortized cost (the average cost over many appends) is O(1).  
    </details>

See [bigocheatsheet.com](http://bigocheatsheet.com/).

### Real-world Uses

* **file systems** Files are often stored in chunks, but when files grow large they may not fit in their original chunk. You can think of a file as a series of nodes with chunks of data and links to the next section of the file. (They're often actually implemented with a more complex related data structure called a B-tree.)

* **implementing stacks and queues** Linked lists are a natural choice for these data structures, which need fast access to beginning or end of a list.

### Starter Code
Take a look at the starter code for the node object type and the singly linked list object type.  

Each node stores `data` and the `next` node.   The linked list stores its `head`, which is a  `Node`.   

Take 5 minutes to make 2 observations each about `Node`, `List`, and the `List.prototype` code (JS) or `node.rb` and `singly_linked_list.rb` (Ruby). Generate at least one question about this code.

### Whiteboarding

1. On the whiteboard, draw a diagram and write pseudocode for `insertAt(data)` (JS) or `insert_at_end data` (Ruby). When you've confirmed your pseudocode works for some sample input, try translating it into code on the whiteboard.

1. On the whiteboard, draw a diagram and write pseudocode for `delete(data)` (JS) or `delete data` (Ruby). If you were working in a pair with one marker, switch who's "driving." When you've confirmed your pseudocode works for some sample input, try translating it into code on the whiteboard.

### Base Coding Challenges

If you haven't yet, clone this repo.  Fill in the method stubs from `singly-linked-list-starter.js` or `singly_linked_list.rb` to your heart's content!  Methods like `delete` and `middle_node` are reasonable interview questions.


### Stretch Challenges

These stretch challenges are harder interview questions. A hint for both: use two pointers to track two locations in the list.

1. Write a method to find the nth-from-last node of a linked list. Can you do this while only looping through the list once?


1. Cycles in linked lists (repeated nodes) can make them stop working for a lot of applications.  Write a method to detect whether a linked list has a cycle in it.

### Closing Thoughts

1. What is the difference between arrays and linked lists?

1. How do you loop through a linked list?

1. What is a pointer?

### Further Reading

The article below goes step by step on creating a linked list and inserting items into it, in JavaScript.  It might spoil some of today's solutions, but you can use this as a guide when dealing with linked lists and their properties:

<a href="http://code.tutsplus.com/articles/data-structures-with-javascript-singly-linked-list-and-doubly-linked-list--cms-23392" target="_blank">JavaScript Linked List Guide</a>
