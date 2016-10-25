+++
date = "2016-10-19T22:36:00-04:00"
description = "Lecture 12 of COMS3134 at Columbia University"
draft = false
title = "Lecture 13: AVL Trees"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

## Random Stuff

Only difference between AVL and Binary Search Tree code are the methods to take
care of the tree balancing. 

For the second programming problem, you just have to make some minor changes;
basically just using it as a type of collection.

Only thing we haven't learned is rotation for AVL inserts.  Have a problem on
this in the homework and will have one on the exam.


## AVL Trees

A self-balancing Binary Search Tree with a height constraint.  At a given node,
the height of the left subtree cannot differ from the right subtree by more
than one.  This has to be true for every node in the tree.

This bounds the height of the tree at *log(N)* so all operations, including
`remove()` are *O(log N)*.

### Tree Height

  * Height of a tree with only the root node is zero
    * Left subtree is `null` and so is right subtree
    * These `null` "nodes" have a height of -1
  * Tree with a root node and one left node
    * Height of left node is 0
    * Height of right node (which is `null`) is -1
    * So it's a valid AVL Tree
  * Tree with a root node and a left node which has a left node
    * Imbalance occurs at the root, which has a left node with height of 1 and
      a right node (`null`) of height -1

Tree with root and three on left and two on right the imbalance occurs on the
first left node.  I don't really understand this.  Review.

Ahh, I think when we say "height" we're talking about the height of the
subtrees to the left and the right, not the height of the node itself.

Imbalances will occur on `insert()` calls.  You need to check the height of the
nodes and then balance if the rules are broken. (??)

### Single Rotation

**Case 1: "zig zig"**
```
  4
 2
1

becomes

  2
 1 4
```
**Case 2: "zig zag"**
```
  4
 2
  3
```
A single rotation doesn't really work here. If you "pull the two up", there's
no room for the 4.

So instead, we perform a double rotation.

### Double Rotation

You have to do two steps.  In the above example, the 3 is what we want to
become the root.  To do this, we do a sequence of two rotations.

  1. Rotate the 2 and the 3
  2. Do the single rotation, pulling the 3 up.

**Case 2: "zig zag"**

```
  4
 2
  3

  4
 3
2

  3
 2 4
```

**Case 3: "zag zig"**
```
  2
   4
  3
```
This is just a mirror of Case 2 so do the same thing.

**Case 4: "zag zag"**
```
  2
   4
    5
```
This is a mirror of Case 1.


## Little Triangles and Big Triangles

We're talking about subtrees as little and big triangles.  I think a small
triangle means height of *h* and a big triangle means a height of *h + 1*.

Rebalancing large trees is actually the same as the trivial examples above.

When a new node gets inserted into a subtree, there are two scenarios:

  1. The height of the subtree doesn't change
  2. The height of the subtree increases by one (and you might have an
     imbalance)

The "zig zag" rebalance (double rotation) is a bit tricky.  Basically the root
of the big triangle (that has the imbalance) needs to be come the new root of
the entire tree.


## Example

3, 1, 7, 2, 6, 8, 4, 5

Insert these numbers into an AVL tree.  We finally get an imbalance on the last
entry of 5.  We get the imbalance at the 6 node which has a right subtree
height of -1 and a left subtree height of 1.

I think this is a double rotation since it's a "zig zag" but it looks like a
simple switch of two nodes..

There's a website that allows you to check the validity of an AVL tree and see
the operations that occur with each insertion.


## Exam

Only thing he hasn't done is implementation of the AVL rebalancing methods.

Exam through 4.4

