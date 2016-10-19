+++
date = "2016-10-12T22:36:00-04:00"
description = "Lecture 11 of COMS3134 at Columbia University"
draft = false
title = "Lecture 11: Trees, Continued"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

Root node is usually operator.

### Post-Order Traversal

  * Gives us Postfix expressions


### In-Order Traversal

  * Do the left
  * Print out the result
  * Do the right


Using a tree to evaluate expressions.

What should we store the operators and operands as?  And how do we tell them
apart?

Some rules (I think):

  * A leaf has to be an operand
  * An inner node has to be an operator
  * Another?


## Implementing a Tree for Expressions: Expression Trees

```java
class ExprNode {
    char operator;
    int operand;
    ExprNode left;
    ExprNode right;
}
```

You could also do a string and then try to parse it and see if it's a number or
not.  Need to be careful of negative numbers.

We're making the decision to just have two instance vars, one of each type.
Then we can have logic to determine which value to look at (and where to store
a value as well).

Programming problem #1 on Homework 3.

  1. Construct tree
  2. Postfix expr
  3. Prefix expr
  4. Infix expr
  5. Evaluate the tree

```java
void postFix(ExprNode t) {
    // Print out the left, then the right, then the node itself.

    // base case. tree is empty.
    if (t == null) {
        return;
    }
    postFix(t.left);  // If these are leafs, it will be our base case and just return
    postFix(t.right);

    // Now we want to print out. Need to determine if it's a operator or
    // an operand.
    if (t.left != null) {
        System.out.println(t.operator);
    } else {
        System.outprintln(t.operand);
    }
}
```

What if we want to change this to prefix?  Basically just move the `if`/`else`
statements to before the recursive call.

What about the infix?  You can't just put the `if`/`else` in the middle of the
left and right postFix calls.  Order of operations is important!

Print parentheses pre and post the `postFix(t.left)` call.

### How do we evaluate the tree?

  1. Evaluate the left side
  2. Evaluate the right side
  3. Do the expression

So evaluating a tree is actually just a flavor of postfix.


## Creating Expression Trees

**Input:** postfix expression from a user  
**Output:** an expression tree object

We use stacks of nodes!

`3 4 * 5 +`

  * encase 3 into a node and `push` to stack
  * encase 4 into a node and `push` to stack
  * oooh we've come to an operator; create a node around the operator and then
    `pop` the stack twice.
    * First `pop` goes to the right reference
    * Second `pop` goes to the left reference
  * Now push the root of the tree we just created back onto the stack (root 
    of the tree is the `*` with `3` and `4` hanging off of it as children)
  * 5 because a node (`ExprNode`)
  * The `+`, encase it, `pop` the stack twice again.
      * 5 goes to the right
      * `ExprNode` (with `3` and `4` with it) on the left
  * `push` back to the stack
  * End of expression! Soo...
  * `pop` the stack! And get a reference to the root `ExprNode` of the tree


## Code.

There's a distinction between the `ExprTree` class and the `ExprNode` class.
The job of the `ExprTree` is to encapsulate `ExprNode`.  The instance variable
will be the root of the tree.

Constructor for `ExprTree` class would take in a postfix expression and build
up the tree.

`ExprTree.java`
```java
public class ExprTree {

    private ExprNode root;

    public ExprTree(String postFix) {
        // run through stack-based algorithm to build the expression tree
        // remember, you're pushing `ExprNode`s
        // When done, pop the stack and make that the root.
    }

    // Evaluate the expression tree.  Public version of the function since the
    // user doesn't know anything about the root node.
    public eval() {
        return eval(root);
    }

    private int eval(ExprNode t) {
        // do your traversal to evaluate the tree rooted at t and return it
    }

    static private class ExprNode {
        int operand;
        char operator;
        ExprNode left;
        ExprNode right;
    }
}
``` 


## Binary Search Tree

### Rules

  * Every single node in the left subtree must be smaller than the root node
  * Every single node in the right subtree must be larger than the root node
  * This must be true at every node

A perfect binary search tree has perfect balance.

At each node, ask if smaller or larger, move to left or right accordingly and
keep going (recursion).  Keep going until you find the value or you reach a
`null` link.

We're making the assumption that there are no repeat values.

So what methods should we have for the ADT for a Binary Search Tree?

  1. `contains`
  2. `add`: just like `contains`, go through looking for it, if you find it,
     just return; if you don't, replace your value with a `null` link.
  3. `remove`

PBST means height is about `O(log N)` so both `contains` and `add` run that
fast.  But not for non-perfect BSTs.

### Example

`5, 4, 3, 2, 1`

Basically you end up building a `LinkedList` so searching could actually be
`O(N)`.

If tree is very well balanced, then it's `O(log N)`, but if it's not, then it's
`O(N)`.  Basically, you have to assume `O(N)` is the worst case unless you
KNOW its well balanced.

But there are such things as self-balancing trees, e.g. ABL trees.  For these
we can guarantee `O(log N)`.

Finding `min` and `max` is pretty easy, just keep going left or right,
respectively.  Same order as searching.

Btw, an in-order traversal of a BST will give us a **sorted list**!
