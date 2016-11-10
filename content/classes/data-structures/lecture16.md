+++
date = "2016-10-31T22:36:00-04:00"
description = "Lecture 16 of COMS3134 at Columbia University"
draft = false
title = "Lecture 16: Midterm Test Review"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

## Problem 1: Induction Proof

Base case:

Is one node a perfect binary tree?  Yes.  1 node.  Is it odd?  Yes.

Assume this holds true for values k = 1 to N.

You need to add a full row of nodes at the bottom.  So we need to add twice
the number of elements, an even number.

So you'd have an odd number plus an even number; an 


## Problem 2

a. Binary search, searching a well balanced binary tree
b. ...
c. Popping from a stack, assigning to head in LinkedList
d. Towers of Hanoi and Fibonnaci recursively 


## Problem 3

Stack. Straightforward.


## Problem 4

Given postorder traversal or tree and inorder traversal, uniquely reconstruct
the tree.

  * Root has to be the `A`
  * Locate that node in the inorder traversal and realize that all nodes to the
    left are on the left side of the tree. Same for those on the right.
  * Look at the postorder for those on the left and you can find the root
  * Do the same for the right

## Problem 5

Pretty much 100% correct.  Didn't really need to check if both left and right
are null, can leave that out.


## Problem 6



## Problem 7