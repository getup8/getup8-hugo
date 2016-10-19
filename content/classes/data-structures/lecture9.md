+++
date = "2016-10-05T22:36:00-04:00"
description = "Lecture 9 of COMS3134 at Columbia University"
draft = false
title = "Lecture 9: Stacks, Queues, Trees"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

## Stacks and Postfix / Infix Expression (continued)

Postfix and Infix expressions.

If we have an infix expression, we scan through each token and when we
encounter an operator, we don't have all of the operands.  So we `push` that
operator onto the stack (as long as it's empty).  If it's not empty and there
are other operators, we need to figure out order of operations.

So we look at the top of the stack and check if it has a lower precedence of
the one we're processing, we `push` on to the stack.  If it's higher, we `pop`
it off and do the operation and keep checking until the stack is empty or we
find an operator of lower precedence.

---

*Example 1*

`a * b - c + d`

Steps:

* a
* stack = [*]
* b
* stack = [-, *]
* c
* `pop(-)`
* stack = [+, *]
* <run out of tokens]
* `pop(+)`
* `pop(*)`

`a b * c - d +`

What about parentheses?  You `push` open parentheses onto the stack.
Eventually you reach the end of the parentheses; when you do, you keep `pop`ing
the stack until you get the open parentheses.  Then you `pop` it out and get
rid of both parentheses and keep going.

---

*Example 2*

`a + b * c + (d * e + f) * g`

Steps:

* a
* [+]
* b
* [*, +]
* c
* `pop(*)`
* `pop(+)`
* [+]
* [(, +]
* d
* [*, (, +]
* e
* `pop(*)`
* [+, (, +]
* f
* `pop(+)`
* `pop(()`
* g
* [*, +]
* `pop(*)`
* `pop(+)`

`a b c * + d e * f + g * +`

Stacks are used in programs (all programs?) and are very present in how
recursion works.  Each level of the recursion pushes the step onto the stack
until we return and we start popping them all off.

---

## Queues and the Josephus Game

You have `n` items in a circle, in a specific order.

Then you have a second value `k`.

You count from the first to the `k`th person.  That person is then out.  Then
you count the next `k`th and that person is out and you keep going.  You wrap
back around in a circle to the beginning and keep going until there's only one
person left and that's the winner.

Can you figure out which position wins given `N` and `k`?  Tough to do I guess.

Let's simulate it instead.  Using a Queue.

*Example 3*

`n = 12` and `k = 3`

3, 6, 9, 12, 4, 8, 1, 7, 2, 11, 5.  10 is the winner.

So in a queue, add them all in order.  As you process, `dequeue` and then
`enqueue` it to the end of the list until the `k`th element, you `dequeue`
but don't `enqueue`.

### Implementing a Queue

We would use a list.  We want to add at one end and remove at the other.

In the `LinkedList` API in Java, the `add` method adds to the end of the list
by default.  There's also a `remove` method that takes no input and by default,
removes the first element.  So these directly map to a `Queue`.

Java actually has a `Queue` interface.  In the homework, we implement `MyQueue`
which is slightly different (simplified I believe).

`LinkedList` actually implements `Queue`.  So it uses `enqueue` and `dequeue`.

```java
import java.util.LinkedList;
import java.util.Queue;

public class Josephus {
  public static void main(String[] args) {
    int n = 12;
    int k = 3;
    // Queue is an interface so we can use it as type
    // LinkedList implements Queue so this works
    // We constrain ourselves to the Queue interface which is a subset
    // of LinkedList
    Queue<Integer> q = new LinkedList<Integer>;
    
    // Initialize our Queue full of peeps
    for (int i = 1; i <= n; i++) {
      q.add(i);
    }
    
    // Keep going until there's only one person left
    while(q.size > 1) {
      for (int i = 0; i < k - 1) {
        q.add(q.remove());
      }
      // We're now at the kth element so remove it
      q.remove()
    }
  }
}
```

---

## Trees

We're going to go up to AVL trees, which is through 4.4 (check that though).

Trees have a root node and zero or more sub-nodes hanging off the root node.
Each of these sub-nodes are in turn trees.

Trees are like Graphs but are not cyclical (you only in one direction). Maybe
read about Graphs.

Linked lists are actually Trees (kinda) with only one path to follow.

The sub-nodes are called children and the root is the parent.  Nodes with no
children are called leaf nodes.  Nodes with children are called interior /
inner nodes.

### Height of a Node

The length of a path is the number of edges we traverse (the connectors between
nodes).  The height of a node is the length of the longest path to a leaf.

### Depth of a Node

Depth of a node is the length of the unique path to the root.  Depth of the
root is zero.  Each level of a tree is basically increasing the depth by one.
