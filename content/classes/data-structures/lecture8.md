+++
date = "2016-10-03T22:36:00-04:00"
description = "Lecture 8 of COMS3134 at Columbia University"
draft = false
title = "Lecture 8: Stacks"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

## Agenda

### Stacks (continued)

  * LIFO: Last In, First Out
  * `pop` and `push` methods are central

A Java `List` is a doubly-linked list.  So for implementing a Stack, we don't
care which side we add / remove from.  If it was a singly-linked list, we'd
want to choose the front so we keep *O(1)* and not *O(N)*.

Stacks can also be implemented with a simple `Array`.

Popping an empty stack is sometimes referred to underflow.

Can you overflow a linked-list based stack?
Not really.  Only if you actually run out of computer memory.

But if you use an array, you do need to worry about overflow.

---

*example on board*

A seven element array.  For first `push`, `push` it to location zero.
Now if we want to `push` another 6, where do we `push`?

We need an instance variable that stores the index of the first free element of
the array.  So in this case, `top = 1`.

Every time you `push`, you go to index top gives you, place the value,
increment `top` by one.

If `top >= Array.length` we know that the array is full.  So `top` needs to be
less than the length in order to add an element.

If we want to `pop` an element, we decrement `top` and return the value at that
location.  We should probably use `--top` as below.

```java
// Simplified implementation
pop() {
    return a[--top];
}
```

We don't actually have to remove the element since we'll just overwrite it in
the future since `top` points at that position.  We can get away with this
although it could be problematic because it would prevent that memory from
being garbage collected.  Also, if we printed the Array or did some operation
with it, we'd need to make sure to not print past `top - 1`.

Aside from me: I think it's better to remove it.. Maybe check to see what they
do in `LinkedList`.

---

### Queues (continued)

  * FIFO.  First in, first out.  Line at the grocery store.

Two main methods:

  1. `enqueue`: adding someone to the line
  2. `dequeue`: removing someone from the line

Goal is to provide the fastest way to provide these methods in these data
structures. Multiple ways to do them but how can we do them most efficiently?

In implementing a queue in these data structures, can they be *O(1)*?:

  * Doubly-linked list: can be *O(1)* for both methods
  * Singly-linked list: not really, *O(1)* and *O(N)* for the two methods

Can also use an `Array`, and again you need to beware of overflowing.

---

*Whiteboard Example: Implementing a Queue Using an Array*

Array of length ten.

So how many instance variables do we need?

If one, let's say `tail`, doesn't work great since we can only track one side
of the queue so we'd have to move everything over if we `dequeue`d an
element.  It'd be O(N) because of that.

If two variables: `head` and `tail`, we can track both ends and we don't have
to move anything around.

When `tail` becomes the length of the array, we've run out of space.  Before
increasing the size of the array and copying over, we should try to use the
same Array and just "wrap around".  We can do this by adding one to `tail` and
taking the `mod` by the length of the `Array`.

This is when a separate `size` variable becomes useful.  It would track the
current number of elements so you can better make the decision of whether to
wrap around or increase the size of the array.

---

### Stack Algorithms

One good use of stacks is to reverse strings; e.g. check for palindromes.  
e.g. *yo banana boy*, *race car*, *taco cat*

Sample algorithm for determining if `race car` is a palindrome:

  1. For each character in the string, `push` into stack
  2. If you have an odd number of characters, ignore the middle character; if
    even, you don't ignore
  3. Skip whitespace
  4. After the midpoint, `pop` from the stack and compare to that character
  5. If ever it doesn't match, you return false
  6. When you get to the end, you should check to make sure the string is empty
    but this shouldn't happen (the string or the stack?)
  7. If you pop an empty stack something is wrong as well

Another example...

RPN Calculator: put the operands first followed by the operator (e.g. 5 3 +).
Parentheses aren't needed because order of operations is explicit.

`5 3 + 2 *` would equal `(5 + 3) * 2`

Let's try to write an algorithm to do this.  
`apply`: takes three arguments, two operands and an operator.

  1. Start out with a stack.
  2. Move through the input token by token.
  3. Is the token an operator or operand?
  4. If it's an operand, `push` onto the stack.
  5. If it's an operator, we `pop` the stack twice.
  6. The first number popped is the second operand
  7. The second number popped is the first operand
  8. Pop the stack one more time, if the stack is not empty, you have an error
  9. Other errors?  If there is only one number and then an operand, the second
    `pop` won't work.

```java
op2 = pop();
op1 = pop();
result = apply(op1, op2, +);
push(result); // Push result back onto stack and keep going
```

Details of this [algorithm can be found here](https://en.wikipedia.org/wiki/Reverse_Polish_notation#Postfix_algorithm).

`2 5 3 + *` should be calculated `(5 + 3) * 2`

RPN is called Postfix expression.
The way we usually do things is called Infix expressions.


  3. A token is either a number or an operator.
  4. How should we distinguish between them?
  5. We can use `split` to turn string into an array.
  6. We can also use String Tokenizer which acts like an Iterator.  They take in a
     string and has two methods: `hasNextToken` and `nextToken`.


