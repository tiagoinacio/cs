# Doubly-Linked List

Bi-directional pointers, to the next node and previous node.

The Linked-List contains a key, next pointer a previous pointer to go forward or go backwards.

PopBack is now order 1, constant-time.

## PushBack(key)

```
node <- new node
node.key <- key
node.next <- nil
if tail = nil
    head <- tail <- node
    node.prev = nil
else:
    tail.next = node
    node.prev = tail
    tail = node
```

## PopBack()

```
if head = nil:
    ERROR: emtpy list
if head = tail:
    head <- tail <- nil
else:
    tail <- tail.prev
    tail.next <- nil
```

## AddAfter(node, key)

```
node2 <- new node
node2.key <- key
node2.next <- node
node2.prev <- node.prev
node.prev <- node2
if node2.prev != nil:
    node2.prev.next <- node2
if head = node:
    head <- node2
```

## Operations Time

<img src="./assets/doubly-linked-list.png" width="300px" />

 Reference: [Coursera](https://www.coursera.org/learn/data-structures/lecture/kHhgK/singly-linked-lists)
