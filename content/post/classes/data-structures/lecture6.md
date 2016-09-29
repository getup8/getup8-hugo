+++
date = "2016-09-26T22:49:10-04:00"
description = "Lecture 6 of COMS3134 at Columbia University"
draft = false
title = "Lecture 6: Linked Lists"
tags = [ "data structures"]
categories = [ "computer science" ]

+++

ArrayList
Issues if we add to end if we're out of room or if we try to add in the beginning (or middle). O(N).

## LinkedList

A few types of linked lists: singly and doubly linked.

Singly linked list:

  * Each piece of data we insert is placed in a `Node` object
  * `Node` class defines two instance variables
    1. The data
    2. Object reference to another node: `next`
  * Don't have prescribed locations in memory where each element is. You have
    to start at the beginning and work your way to it using the `next`
    references.
  * `next` reference in last element of the list just points to `null`

Linked list class has a `head` reference to the first element of the list.  So
to get the third element, you have to keep a counter and start at the first and
go to the third using `next`.

What if we want to access the nth element?  What's Big-Oh cost?  *O(N)*.
What about for an array? *O(const)* or *O(1)*.

Linked lists suck!  At least for *get* operations.  They're more expensive.


```java
class Node<AnyType> {
    AnyType data;
    Node<AnyType> next;
}
```

```java
class LinkedList<AnyType> {
    Node<AnyType> head;
    int size;

    // Getter
    AnyType get(int i) {
        // Initially point to beginning of list
        Node<AnyType> t = head;
        int count = 0;
        if (i >= size) {
            // throw exception..
        }
        while(count < i) {
            count++;
            // You'll get a null pointer exception here if `i` is greater than
            // the number of nodes in the list
            t = t.next;
        }
        return t.data;
    }
}
```

So what would the cost be to insert a new value at the beginning of the list?
Order 1. *O(1)*.

  1. Create a new node
  2. Put data into it
  3. Set `next` equal to `head`
  4. Make `head` refer to it

What about if you want to insert at the end?  You need to iterate all the way
to the end since you only have a reference to `head`.  So it's O(N).

What about the middle?  O(N) still.  But once I have the reference to the node
I want to insert after already, it's easy and O(1).  Remember that.  So if
you're already moving across the list, and you decide you want to insert
something, it's easy and cheap.

Another benefit: We don't need to specify how large this list is going to be.

This is a building block for other data structures.

## Doubly Linked Lists

You have a head and a tail.  You add a `previous` pointer.  So you can move in
both directions, forwards or backwards.

Iterator interface.  ListIterator interface adds an extra bit that allows you
to move forward or backward; it exploits the doubly linked list.

Uses "sentinal nodes".  The head data has no data.  The first piece of data is
actually at head.next().  The tail also doesn't have any data.  The last node
is tail.previous().

Nodes now have three fields:

  1. data
  2. previous
  3. next

An empty doubly linked list:
null -> head -> tail -> null

If we're going to insert data, we'd insert after head or before tail.

  1. Create a node, populated with data
  2. `previous` points to `head`
  3. `next` points to `head.next` (instead of `tail`)
  4. `head.next.previous` (or `tail.previous`) points to it
  5. `head.next` points to it

You can actually implement both types with sentinal nodes (singly and doubly).

Next class:
ArrayList code.
Doubly LinkedList code.
