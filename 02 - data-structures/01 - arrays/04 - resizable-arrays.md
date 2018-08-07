# Resizable arrays

It's common in many languages that when a basic array is created it cannot be resized. What many languages to in the background is create a new array, with more memory, to fit in the new elements. This is an order N operation.

> The idea is to store a pointer to a dynamically allocated array, and replace it with a newly-allocated array as needed.

Dynamic array is an abstract data type with the following operations (at a minimum):

* Get(i): returns element at location `i` in constant-time O(1).
* Set(i, val): sets element `i` to `val` in constant-time O(1).
* PushBack(i):  adds `val` to the end of the array in linear time O(n).
* Remove(i): removes element at location `i` in linear time O(n).
* Size(): the number of elements in the array in constant-time O(1).

## Implementation

Store:

| variable  | description                               |
|-----------|-------------------------------------------|
| arr       | dynamically-allocated array               |
| capacity  | size of the dynamically-allocated array   |
| size      | number of elements currently in the array |

Example by duplicating the capacity:

Start with capacity of 2, and size 0.

PushBack(a) -> size: 1, capacity: 2.
PushBack(b) -> size: 2, capacity: 2.
PushBack(c) -> allocate a new dynamically allocated array with capacity 4 and size 3
PushBack(d) -> size: 4, capacity: 4
PushBack(e) -> allocate a new dynamically allocated array with capacity 8 and size 4

| Get(i)                                  |
|-----------------------------------------|
| `if i < 0 or i ≥ size:`                 |
| &nbsp;&nbsp;`Error: index out of range` |
| `return arr[i]`                         |

<br />

| Set(i, val)                             |
|-----------------------------------------|
| `if i < 0 or i ≥ size:`                 |
| &nbsp;&nbsp;`Error: index out of range` |
| `arr[i] = val`                          |

<br />

| PushBack(val)                           |
|-----------------------------------------|
| `if size = capacity:`                   |
| &nbsp;&nbsp;`allocate new_arr[2 x capacity]` |
| &nbsp;&nbsp;`for i from 0 to size - 1:` |
| &nbsp;&nbsp;&nbsp;&nbsp;`new_arr[i] <- arr[i]` |
| &nbsp;&nbsp;`free arr` |
| &nbsp;&nbsp;`arr <- new_arr; capacity <- 2 x capacity` |
| `arr[size] <- val` |
| `size <- size + 1` |

<br />

| Remove(i)                             |
|-----------------------------------------|
| `if i < 0 or i ≥ size:`                 |
| &nbsp;&nbsp;`Error: index out of range` |
| `for j from i to size - 2:` |
| &nbsp;&nbsp;`arr[j] <- arr[j + 1]` |
| `size <- size - 1` |

<br />

| Size()                             |
|-----------------------------------------|
| `return size`                 |

## Summary:

Unlike static arrays, dynamic arrays **can be resized**.

**Appending** a new element to a dynamic array is often constant time, but **can take O(n)**.

Some space is wasted, at the most **half of the space is wasted**.

Resize can also be done to shrink the array.