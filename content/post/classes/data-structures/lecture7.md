+++
date = "2016-09-28T22:36:00-04:00"
description = "Lecture 7 of COMS3134 at Columbia University"
draft = true
title = "Lecture 7: ArrayList, LinkedList, Stacks"
tags = [ "data structures"]
categories = [ "computer science" ]

+++

## Agenda

  * Cycling back to the ArrayListIterator to understand how nested classes
    function.
  * Also going through implementation of LinkedList.
  * Stacks and Queues.

## To Dos

  * Read Chapters 3 and 4.
  * And for me, go back to Big Java and at least skim those chapters as well.

---

## Array Lists

Going back to `MyArrayList` code.

`iterator()`: create a new instance of a class that implements `Iterator`

`ArrayListIterator` is a nested class; it's defined inside the `MyArrayList`
class. It's defined as private so that no one outside MyArrayList can
instantiate it, but `MyArrayList` can.

Purpose of an iterator is to step through a collection of any sort.

  * hasNext(): figure out if there's a next element
  * next(): move to next and return it
  * remove(): remove the element that we just moved past

Our iterator is *not* `static`.  There are two kinds of nested.

  * Non-`static` is tied to the particular instance of MyArrayList from whence it
    is generator.

The one thing we need to keep track of w/ an iterator is "Where are we?".

Private vars:

  * `current`: where we currently are; instantiated to zero.
  * `okToRemove`: whether we can implement the `remove` method. At the
    beginning it's not okay (since we'd remove n-1) so this is set to `false`

`size()` can be accessed on `MyArrayList` since `ArrayListIterator` is nested.
Would it work if the nested class was `static`?  I'm guessing no since it
wouldn't be tied to a specific instance but I should test it!

`curent++` will evaluate the value of `current` first and then increment it.

MyArrayList.this.remove(--current);

There's a method in the MyArrayList to actually remove an element which is
what we actually want to call.  

`MyArrayList.this` means the specific containing object.
`--current` means we remove the item before the current one.

Any Collection, which includes any List, would provide an Iterator.

An Inner Class is non-static nested class.

---

Back to Linked Lists.

MyLinkedList implementation (that will be sent out?) does a doubly linked list
with sentinal nodes.

Don't worry about `modCount`.

There's a class LinkedList and you can just instantiate to create.

Has two private Node objects: begin and end.

`Node` class is `static` and defined in MyLinkedList.
`Node` doesn't have access to MyLinkedList objects (since it's `static`).
`next` and `prev` pointers to other `Node`s.

`doClear()` creates end nodes and makes them point at each other.
Look at the code.

Also called when `beginMarker` and `endMarker` already exist by the `clear`
method.

Java garbage collection! Imagine if there's a count in memory of how many
references there are to an object.  The Java Virtual Machine reclaims the
memory of the objects that no one points to.  In other languages like C this
will give you a memory leak and you need to do it yourself.

So that's what happens when `clear()` is called.

`size()`
`isEmpty()`

`add()` Lots of them! Overloaded.
If no other info, add at the end of the list.
Another implementation takes index we want to insert something and the object
itself.

In a linked list, you don't just jump to a location, you have to iterate from
beginning to end.  So what we actually want, given an index, is the reference
to the `Node` that exists that many steps into the linked list.

  * `addBefore()`
  * `getNode()`
    * Interesting!
    * Depending on what index is, we start from beginning or end. Doesn't
      change Big Oh
    * Start at first element if start at beginning
    * Start at endMarker if we start at the end though since we're inserting
      before.

Also have a `set` method that also uses `getNode()`.

Remove methods.

  * Remove `Node` p.  Basically just bypass it by changing the references of
    the nodes before and after.  All you need is the reference to the node you
    want to remove and you can use its `next` and `prev` references!

Lastly has an `iterator()` method that returns an instance of the
`LinkedListIterator` class that's very similar to our `ArrayList` iterator.
Look at this code and understand it.

---

So what can we do with these things??

There are other data structures built on top of these.

The Stack.

  * You can only add/remove elements from the top of a Stack
  * Last in, first out. aka LIFO

ADT, Abstract Data Type of a Stack.
What methods does it need to have to behave like this?

Adding an element is referred to as `push`ing.
Removing an element (and returning it) is referred to `pop`ping.

`top` or `peek` gives you the last value without removing?

`isEmpty()`
`size()`

Lots of problems using just `push` and `pop`.

  * Reversing the order
  * Detecting palindromes: a word that's the same backwards and forwards
    * If you have an even number, the first half is the second half reversed
    * If odd, ignore middle character, 
    * `pop` off the second half and compare to each of the first

This is related to the Homework.  Something similar.
Need to implement a Stack.
Any List will work.

If singly linked list, push/pop from front, all O(1), otherwise if you do from
end, it's O(N).
With doubly linked list, it's O(1) from either end.

LinkedList has push / pop methods in java.util.  Basically just reimplement this
along with the other functions above.

---

Queues.

  * Similar to Stacks, but FIFO, first in, first out.
  * Adding from one end, Removing from the other.

