+++
date = "2016-11-09T22:36:00-04:00"
description = "Lecture 18 of COMS3134 at Columbia University"
title = "Lecture 18: Hash Tables and Heaps?"
tags = [ "data structures"]
categories = [ "computer science" ]
hidden = true
+++

## Hashing in Java Standard Library

In the `Object` class, there's a function called `hashCode()`, which applies
a hash function to that object.  So when one inserts a Java object into some
built-in hash table (`HashMap` or `HashSet`), they use that function or the
overrides of that function.

The `.equals()` method actually works via `hashCode()`.  So if two objects have
the same hash code, that function will return true.

Reversible vs. Non-reversible.  Non-reversible is good for security but doesn't
concern us too much.

`String` evaluates to the ASCII code of the character(s).

Integers and doubles and such will hash to the underlying number.

When you do `System.out.print(Object)` that's the hash code that gets printed
out.

---

Let's say we're inserting new values into a hash table (Integers).

Hash table itself will be an array where we'll store the values we're
inserting.  We don't want this array to be that large so we don't want to
create an array that could store any integer (based on its value).

Operation:

`integer % tableSize`

You should pick prime numbers as the size.  You tend to get better spread with
locations if you do that.  There are certain types of hash tables where this is
actually *critical* for inserts to even happen.

Often, for convenience and ease, we just assign a table size of 10 though.

---

## An Example of a Hash Table

Given an array of size 10 (so a hash table with size 10).

  * Insert 0.  Goes to location 0.
  * Insert 81.  Goes to location 1.  (`81 % 10 = 1`)
  * Insert 1.  Try to go to 1 but we have a *collision*.

Two types of collisions we have to worry about:

  1. If underlying hash function gives us the same hash code
  2. When the insertion position is already filled

Different ways of dealing with this.

## Separate Chaining Methods

With separate chaining, we can have a separate structure, like a `LinkedList`
stored at each location in the array instead of a single value.

So how efficient is this?

  * Inserting is *O(1)* since inserting into a `LinkedList` is *O(1)*, as is the
    hash function.
  * Searching via a `contains()` call could actually be *O(N)* if the hash
    function is terrible or the table is much too small.  We could instead
    implement a balanced (e.g. AVL) binary tree and the search would be
    *O(log N)* but then this would ruin our insertion time.

There's a property of a hash table called the load factor.  It's the ratio of
the number of elements in the table to the table size.

`loadFactor (lambda) = # of inserted elements / hash table size`

If we ensure the load factor of the hash table is no greater than 1, then we're
pretty good to go.

But that assumes:

  1. The hash function is good
  2. The table size is prime
  3. Something else maybe

When that load factor gets too large, we want to **rehash** the table.

  1. Grow the size of the table (usually double it)
  2. Rehash all the elements (with the new hash function modulo) and insert
     into the new table.  This is *O(N)*.

So inserts into a hash table have the danger of causing a rehash.  There's this
idea of amortized cost though when we look at the cost of this rehash on
average across all inserts so it's not *that* expensive.  But it doesn't
dismiss the fact that *one* insert is *O(N)* when the rehashing occurs.

NOTE TO SELF.  See if I can get the 1004 class notes to learn some of the
basics of computing.

---

## Open Addressing

Only one element can be at any given location in the hash table.  An example
of this is **Linear Probing**.

So the load factor of these tables is never more than one.

So what happens with a collision?  We need to find a new place for it since we
can't just add to a list.  We need a deterministic way of inserting it so we
can go back and find it when we search.

### Probing

Gives us a series of locations that we should try to insert/search in. These
series are defined like:

`h0(x), h1(x), h2(x)...`

So the *ith* position can be calculated like:

`hi = (hash(x) + f(i)) % tableSize`

### Linear Probing

We have a linear function, usually just `f(i) = i` that we use to probe. This
just means we go to the next position in the array until we find an open space.

**Primary Clustering** is an issue with this method.  You end up getting large
clusters of the array that are filled and it slows down the operations a lot.
You need to make sure:

  1. The load factor is less than 0.5 (rehash if it goes above this)
  2. You don't try to insert on a primary cluster

So this isn't a great choice.  We want to spread things out more and avoid any
clustering.

If you remove an item completely and make a location empty, that breaks the
contains check because we might stop searching at the empty position.  This is
bad.  We have to do "lazy" deletion here, basically by leaving the value here
and storing with a var whether its there or not (e.g. `isActive`).

When you do a rehash though, you can discard all of these.

### Quadratic Probing

Next class.


