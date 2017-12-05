# Stack

The stack data structure is precisely what it sounds like: a stack of data. In certain types of problems, it can be favorable to store data in a stack rather than in an array.
A stack uses LIFO (last-in first-out) ordering. That is, as in a stack of dinner plates, the most recent item added to the stack is the  rst item to be removed.

It uses the following operations:

Unlike an array, a stack does not offer constant-time access to the ith item. However, it does allow constant­ time adds and removes, as it doesn't require shifting elements around.
Abstract data type with the following operations:

* Push(key): adds key to collection

* Peek(): returns most recently-added key

* Pop(): removes and returns most recently-added key

* isEmpty(): Return true if and only if the stack is empty.

One case where stacks are often useful is in certain recursive algorithms. Sometimes you need to push temporary data onto a stack as you recurse, but then remove them as you backtrack (for example, because the recursive check failed). A stack offers an intuitive way to do this.

A stack can also be used to implement a recursive algorithm iteratively.
