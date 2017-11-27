# Definition

Array is a contiguous area of memory either on the stack or on the heap, broken down into equal sized elements, and each of those elements is indexed by contigous integer.

It can be zero based indexed or one based indexed.

Constant-time acces to read and constant-time access to write O(1).

Every element needs to be the same size, so we can do pointer arithmetic and have O(1) to read and write.
If each element had a diferent size, we would need to go through each one and sum all together. This would represent a O(n) time.

To read get the memory address of an element in the array, given an index that we are interest in named `i`, and `first_index` as a 0 or 1 (depending if it is zero based array or not):

`array_address + element_size x (i - first_index)`

# Multi-dimensional arrays

How do we find the address of an element? There are a couple of alternatives.


## Row major

If the elements are stored by row (let's say that we have the first row, then the second row, etc.), we would need to:

* First, we need to skip the full rows that we are not interested in.
* Then, we need to skip the elements in the same row.

Like this:

`array_address + element_size x ((row - 1 x elements_per_row) + i - first_index)`.

## Row major

If the elements are stored by row (let's say that we have the first row elements, then the second row elements, etc.), we would need to:

* First, we need to skip the full rows that we are not interested in.
* Then, we need to skip the elements in the same row.

Like this:

`array_address + element_size x ((row - 1 x elements_per_row) + i - first_index)`.

(1, 1)
(1, 2)
(1, 3)
(1, 4)
(1, 5)
(1, 6)
(2, 1)
(2, 2)
...

## Column major

If the elements are stored by column (let's say that we have the first column elements, then the second column elements, etc.), we would need to:

* First, we need to skip the full columns that we are not interested in.
* Then, we need to skip the elements in the same column.

Like this:

`array_address + element_size x ((column - 1 x elements_per_column) + i - first_index)`.

(1, 1)
(2, 1)
(3, 1)
(1, 2)
(2, 2)
(3, 2)
(1, 3)
(2, 3)
...

# Times for common operations


|           |   Add   |   Remove  |
|-----------|---------|-----------|
| Beginning |   O(n)  |    O(n)   |
| End       |   O(1)  |    O(1)   |
| Middle    |   O(n)  |    O(n)   |

If we need to add or remove an element from the beginning or middle of an array, we would need to shift each element, so that is done in linear time, order N operation, because we need to pass through each element in the worst case scenario.

If we need to remove or add at the end, that is done in constant-time, order 1 operation.
