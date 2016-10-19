+++
date = "2016-10-10T22:36:00-04:00"
description = "Lecture 10 of COMS3134 at Columbia University"
draft = false
title = "Lecture 10: Trees"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

Starting this lecture at 6:40 btw. 30 minutes of nothingness before.

## Trees

  * Trees are a bunch of nodes
  * Need to have references to child nodes
  * Very likely going to iterate across children, not necessarily jump to a
    specific one.
  * You could do this with a LinkedList but there's an easier way
  * To iterate through children, go to `firstChild` and then iterate through
    using `nextSibling`

```java
class TreeNode<T> {
    T data;
    TreeNode<T> nextSibling;  // Similar to LinkedList
    TreeNode<T> firstChild;  // Another LinkedList type structure to children
}
```

Pre-order traversal: evaluate the node first, then evaluate the children.
Post-order: evaluate the children first, then the node.

## Tree Traversal

A pre-order tree traversal via `listAll`

```java
// Pseudo code
private void listAll(int depth) {
    printName(depth);  // Print name of object
    if(isDirectory()) {
        for each file c in this directory (for each child) {
            c.listAll(depth + 1);
        }
    }
}

public void listAll() {
    listAll(0);  // Initial call for root node calls actual recursive method
}
```

## Tree Types

  * Full Binary Tree
    * ?
  * Complete Binary Tree
    * Last row is filled up from left to right but not all the way
  * Perfect Binary Tree
    * A complete binary tree with the last row all filled up

Need to think about the number of nodes in a tree given the height..

A perfect binary tree has `2^(h + 1) - 1` nodes.

Btw, know what "proof by induction" means.

### Proof by Induction

#### Base Case

  * 2^(0 + 1) - 1 = 1
  * 2^(1 + 1) - 1 = 3

Assume for perfect trees of height `1` through `k` this holds.

So now we need to prove that this works for a tree of height `k + 1`.

A tree of height `k` will have `2^(k + 1) - 1` nodes.

Now copy that tree and we have two identical trees.

Now add a root node and point to the root nodes of those two initial trees.

So now we just need to add up the nodes.

`2 * (2^(k + 1) - 1) + 1`
`2^((k + 1) + 1) - 2 + 1`
`2^((k + 1) + 1) - 1`

## QUESTION ONE ON THE MIDTERM WILL ESSENTIALLY BE THIS BUT ON ANOTHER
   CHARACTERISTIC OF THE BINARY TREE


## Expression Tree

Tree will be represented by a full binary tree.  In a binary tree, there is
something on the "left" and something on the "right" so there is some implicit
order.

Operators are interior nodes.  Operands are leaf nodes.

Example:

3 + (2 * 5)

  +
3   *
  2   5

Does the root node of an expression tree have to be an operand?  Nope.

Interior nodes must be operators.

Leaf nodes must be operands?

Look at the ExpressionNode class...

```java
public class ExprNode {
    Op data;  // either operator or operand
    ExprNode left;
    ExprNode right;
}
```




