+++
date = "2016-09-21T22:49:15-04:00"
description = "Lecture 5 of COMS3134 at Columbia University"
draft = false
title = "Lecture 5: Iterators and Interfaces"
tags = [ "data structures"]
categories = [ "computer science" ]

+++

A list is a type of collection.

A collection is 

Iterator is another class that attaches to a particular Collection used to go
through the Collection, item by item.

Can have multiple iterators attached to a collection moving at different
speeds, different locations.

java.util.Iterator is an "interface" provides methods.

Iterator method is a factory method and its job is to construct a class. It's
job is to create some Iterator object that iterates across the collection and
returns something.

An iterator is its own object of type Iterator.

This is all in chapter 3 of the book..

Iterators have 3 methods:

  1. Boolean: hasNext (if true, move on to next, if false, end of list)
  2. AnyType next(): returns current element (telling where we aer),
     advances to next
  3. void remove(): remove the item? or the iterator? think the latter.
  
while hasNext() == True:
  next()

List interface extends Collection.  So all methods included in List.

So the List interface adds additional methods to take advantage of ordered
space.

ListIterator is same as Iterator but can move forward/backward since lists have
an order (Collections do not)


Some mumbo jumbo about generics and objects and using int vs Integer???

Advanced for loop expects an iterable / iterator. (a.iterator())
It creates an iterator and uses it to go through.
Understand how to make something work in an advanced for loop.

Iterator is generic so defaults to object.  Need to cast it like
java.util.Iterator<Integer>

---

When we create an ArrayList, we need to preallocate the size (let's say 10
elements) and keep track of the first empty location.  So on instantiation,
it's location zero.  We don't know how long it's going to be.

Adding elements at end of list is O(1) operation until you fill up the list
(the preallocated size) and then it's O(n) to copy it to the new array.

So how big do we make it when we need a larger list?  Wasteful to just make it
11 since it's quite possible to make it 12 later.

Randomly, they multiply by 1.5.  Or 2.

Removing elements also O(1). So is changing a specific element.

What if you want to insert an element in the middle or beginning?  You have to
copy everything and move it over.  So O(n).  n is how many things you're
moving?

---

On Canvas there is a download of all the code in the textbook.

Difference between extends and implements?
implements Iterator..

theSize is how many items are filled up.
Length of theItems is how long the arraylist is.

ensureCapacity().

When creating the array, you construct an array of objects and then cast it to
generics.  The compiler doesn't know how to create an array of generics.

--

By starting at the end with add() you don't have to move anything (or iterate
through anything) if you're adding to the end.

ArrayListIterator() is not provided by java, need to implement ourselves.
