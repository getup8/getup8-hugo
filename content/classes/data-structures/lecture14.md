+++
date = "2016-10-24T22:36:00-04:00"
description = "Lecture 12 of COMS3134 at Columbia University"
draft = false
title = "Lecture 14: Midterm Review"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

## Midterm Review

  * 8 questions
  * Straightforward
  * Touch on every topic
  * A little bit on the long side; budget time well and if you're stuck, move
    on to the next
  * Closed book / notes / calculator
  * Pen or pencil, just not red
  * Short answer problems, Big Oh
  * Crank through algorithms on paper: AVL inserts on paper
  * Write two or three Java methods, one of which will be a recursion on a tree
  * Induction proof is the first question

## From the Book

  * 1-4.4 and 4.6

### Chapter 1

  * Chapter 1.  Induction proofs.  Don't really need to know all the math.
    Fibonacci.  Binary trees.  Prove a property of a binary tree.
  * Proof by counter example. Homework 3.
  * Recursion. Base cases, design rules and be able to write methods
    recursively.
  * 1.4 and 1.5.  Don't need to focus on this.  Just be able to use generics
    and interfaces as we have in homeworks.  There will be generic methods.
  * 1.6 Function objects

### Chapter 2

  * Pretty much whole thing
  * 2.4 examples don't really have to worry about but otherwise, all of it

### Chapter 3

  * The whole thing.
  * Josephus problem about how to use a queue.  Don't worry about that.  But
    know where queues, enqueue, dequeue, etc.
  * Implementation with LinkedList and ArrayList (MyLinkedList out of Weiss),
    know how to add and remove items

### Chapter 4

  * 4.3.5 Ignore
  * Otherwise, everything up through 4.4 and then 4.6 as well

---

## Detailed Topics

  * Tower of Hanoi.  Remember the basic problem and how we solved it
    recursively.  Will not have to implement but need to understand it.  What
    is the Big Oh notation of that?  2^(n-1) or 2^N
  * Abstract Data Type vs Data Structure.  ADT doesn't define how they're
    performed.  Data Structure is the specifics and implementation.  Stack vs
    ArrayStack.  Interfaces are kinda ADTs.  Just signatures, not
    implementation.
  * Generics.  Interfaces.  Iterators across a collection; using it with an
    enhance for loop.  Comparable. Inner Class.  Who can access them and who
    can't.  Binary Nodes for example.
  * Big Oh notation for asymptotic runtime.  Typical growth functions and have
    a sense of ordering.
  * Costs of algorithms WILL be on the exam.  Big Oh is an upper bound.  But we
    need the tightest bound possible.
  * Binary Search Trees are O(N) for worst case.  So be careful of balanced vs
    not.  If it's perfectly balanced, then O(log N).
  * List ADT.  Typical List operations.
  * ArrayList.  Costs of operations on ArrayLists.  How they're implemented.
    Default size that auto grows.
  * LinkedList.  Runtimes for all methods.  Singly vs Doubly.  For add/removes,
    depends on where we are; O(N) or O(1).  Implementation.
  * Stacks/Queues.  Stack ADT and operations.  Queue and operations.  Costs of
    those.  All ideally O(1).
  * Lots of implementations of Stacks from class and homework.
  * Queues. LinkedList implementation.  Don't need to worry about circular
    array implementation.
  * Trees and terminology.  Parent, child, leaf, path, node, depth, height.
    Height of leaf is zero.  Height of null link is -1.
  * Trees.  First child and next sibling vs link to all children.
  * Full binary trees: every node is a leaf or two children.  Remember all of
    these.  Complete binary tree is not necessarily full.  Filled from left to
    right.  Perfect binary tree is full, final row filled up.
  * In-order, pre-order and post-order traversal of a tree and be able to
    perform them and use them for other stuff.

### Post Order

Recursively call the left
Recursively call the right
Call the current node (root)

```
    A
 B     C
D E   F
   G
```

`DGEBFCA`

### Pre Order

Current node first (root)
Go left
Go right

`ABDEGCF`

### In Order

`DBEGAFC`


## Topics Continued

  * Expression trees.  Operators and operands.  Interior nodes are operators
    and leaves are operands.  You can do postfix by post order, etc.  In-order
    traversal you have to modify a bit to include parentheses.
  * Stack based algorithm to build the tree.  Push/pop, etc.  Know that.
  * Know rules of Binary Search Tree.  In-order traversal will get us the
    elements in sorted order.  You should know when a tree is BST ordered.
    Know contains, findMin, findMax and remove.  Know about lazy deletion.
    Know how to do the remove.
  * Should know how to perform BST / AVL operations.  He'll give a list of
    numbers and we'll have to construct a tree.
  * AVL trees.  Constrain height so that operations are in O(log N).  Doesn't
    have to be perfectly balanced but all AVL trees are Binary Search Trees.
    Always needs to be a BST, even during rotation.  Left subtreees height
    must not differ from right subtree's height by more than one at every
    node.  Know how to spot these and how to fix them using rotations.
  * You'll have to draw an AVL tree given a list of numbers.  And you'll have
    to write down all the intermediate steps, including the rotations and
    show where the imbalances are, etc.
  * Iterable.  Implements Iterator, has some method, returns an iterator.
  * Throwing exceptions. Prob not but maybe.
  * No File IO operations.

## Example AVL Tree Creation

`50, 20, 10, 30, 40, 25`

```
  50
20

  *50
 20
10

# Single rotation.

  20
 10  50
    30 

  20
10  50*
   30
     40

# Double rotation.

  20
 10  50
    40
   30

  20
10  40
   30 50

   20*
10    40
    30  50
  25

# Again a double rotation.

   20
10    30
    25  40
  20

# THIS IS WRONG FIX THIS.

   20
10    25
    20  30
         40
```

## Induction Proof

  1. Show that the base case holds true
  2. Make an assumption that the property holds true from the base case up to
     an arbitrary N.
  3. Show that it's true for N + 1
  4. Draw a diagram and show what happens when you add one more
  5. A little math to prove what we need to prove

Total number of nodes.  Total height of tree.  Etc.
