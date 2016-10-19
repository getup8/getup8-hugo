+++
date = "2016-10-17T22:36:00-04:00"
description = "Lecture 12 of COMS3134 at Columbia University"
draft = false
title = "Lecture 12: Trees, Continued"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

Material covered through next lecture (on Wednesday) will be on Midterm.

This week's resitation sessions will be midterm review.

Next Monday will be Midterm review.  Do not miss this.

---

## BinarySearchTree Class

Look up and understand this code, it's provided in the book PDF.

`Comparable<? super AnyType>`says it has to be comparable to itself or any
superclass of itself.

He says it's gratuitous having two Constructors since when you insert, you
replace the null reference with a single leaf node.

### `public boolean contains(AnyType x)` Method

Returns `contains(x, root)`.  The true `contains` method has to take in the
root.  This one does not and is not recursive, it actually calls the `private`
recursive method with `root`.

We see this `public` / `private` pairing a lot in this.


### Insert Method

`public boolean contains(AnyType x)`

The method takes in a node we want to insert.  If it's already in the tree,
we don't do anything.  If it's not, we add it in, and make sure the rules of
the tree are upheld.

```java
public void insert(AnyType x) {
    // We assign to root here just in case the tree is empty.
    // So the recursive `insert` that this calls returns the "new"
    // root of the tree
    root = insert(x, root);
}
```

The `private` method is recursive and similar to `contains` in its logic.


### Find Min and Find Max

We basically just search left (right) until we find a left `null` reference and
return that node with the `null` pointer.

These are tail recursions; when you make a recursive call as the very last line
of your method.  You're effectively iterating across the dataset.  These can
very easily be replace with `while` loops.

In the text, `findMax` is written iteratively as a while loop instead of as a
recursion.


### Height Method

Find the longer of the left and right subtrees (recursively) and add one (the
root).


### Print Tree

Standard in-order traversal. Will print the data in sorted order.


### Remove

Leaf nodes are simple.  Just drop them.

What if we delete the root?

  * Replace with the smallest thing on the right hand side.
  * Or the largest thing on the left hand side.

So the steps are:

  1. Find the largest on the left side using `findMax`
  2. Replace root with it
  3. Recursively remove it

`public` method very similar to `insert` method.  
`private` method starts out with base case similar to others (null tree).

Pretty simple if the node just has a single child.  If it has two, it's kinda
hard.

Look over the code and understand this.  Fading in class fast.


### Lazy Deletion

Add a field to the TreeNode class `valid`.  If it's `true`, the node is marked
to exist.  If it's `false`, the node is marked to not exist.  So in lazy
deletion, you just do a `contains` check and if it finds it, you just flip
the value to `false`.

All the other methods need to be adjusted to take account of this though and
check whether nodes are `valid` or not.

`findMax` and `findMin` actually become quite tough.


## AVL Trees

Binary search trees with an added condition: the height of the left subtree
cannot differ from the height of the right subtree by more than one.  If at
any time, an insertion or deletion is made that disrupts this balance, you need
to perform a single or double rotation to fix it.





