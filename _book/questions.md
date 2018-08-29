
# Questions

## Code

### How to search for a key in a binary search tree iteratively?

```
/*
 * Do not forget that type T may not implement the comparison operators: < and >.
 */
TreeNode<T>* searchIteratively(const T& key) {
    TreeNode<T>* currentNode = root_;

    while (currentNode) {
        if (currentNode->key == key) {
            return currentNode;
        }

        if (key < currentNode) {
            currentNode = currentNode->left;
        } else {
            currentNode = currentNode->right;
        }
    }

    throw std::out_of_range("tree is empty");
}
```

### How to level-order traversal a tree recursively (breadth first)?

```
void breadthFirstTraversal() {
    auto queue = Queue<T>();

    queue.push_back(root_);

    while (!queue.isEmpty()) {
        auto node = queue.pop();

        if (node->left != nullptr) {
            queue.push_back(node->left);
        }
        if (node->right != nullptr) {
            queue.push_back(node->left);
        }
    }
}
```

### How to in-order traversal a tree recursively?


```
void inOrderTraversal(TreeNode<T>* node) {
    if (node != nullptr) {
        inOrderTraversal(node->right, vector);
        visit(node->value);
        inOrderTraversal(node->left, vector);
    }
}
```

### How to post-order traversal a tree recursively?

```
void postOrderTraversal(TreeNode<T>* node) {
    if (node != nullptr) {
        postOrderTraversal(node->right, vector);
        postOrderTraversal(node->left, vector);
        visit(node->value);
    }
}
```

### How to pre-order traversal a tree recursively?

```
void preOrderTraversalSearch(TreeNode<T>* node) {
    if (node != nullptr) {
        visit(node);
        preOrderTraversalSearch(node->left);
        preOrderTraversalSearch(node->right);
    }
}
```

### How to test a bit in C?

```
bit_fld & (1 << n)
```

### How to toggle a bit in C?

````
bit_fld ^= (1 << n)
```

### How to clear a bit in C?

```
bit_fld = bit_fld & ~(1 << n)
```

### How to set a bit in C?

```
bit_fld = bit_fld | (1 << n)

or the short version

bit_fld |= (1 << n)
```


### How many edits away are the string "spell" from "mine". One edit might be delete, insert or change a char.

```
Spell -> spill -> pill -> pile -> pine -> mine.

We could use a tree to solve this problem of Edit Distance: https://en.wikipedia.org/wiki/Edit_distance.

Building a tree to search a problem space.
```

### How to calculate decimal number from an IP address?

```
/*
 * IP addresses V4 have 4 bytes: 32 bits.
 */
int ip(int ip) const {
    return ip[1] * 2^24 + ip[2] * 2^16 + ip[3] * 2^8 + ip[4];
}
```

### Implement a Stack using a linked list with the following methods: isEmpty, push, pop, peek.

```
#ifndef DATA_STRUCTURES_STACK_LIST_H_INCLUDED
#define DATA_STRUCTURES_STACK_LIST_H_INCLUDED

#include <memory>
#include <stdexcept>

namespace datastructures {

template <typename T>
struct StackNode {
    T data;
    StackNode* next;
};

template <typename T>
class StackList {
 private:
    datastructures::StackNode<T> *top_;

 public:
    StackList() :
        top_(nullptr)
        {}

    bool isEmpty() const {
        return top_ == nullptr;
    }

    void push_back(const T &data) {
        datastructures::StackNode<T> *secondNode = top_;
        top_ = new datastructures::StackNode<T>();
        top_->data = data;
        top_->next = secondNode;
    }

    T peek() const throw {
        if (top_ == nullptr) {
            throw std::out_of_range("Stack is empty.");
        }
        return top_->data;
    }

    T pop() throw {
        if (top_ == nullptr) {
            throw std::out_of_range("Stack is empty.");
        }

        datastructures::StackNode<T> *previousHead = top_;
        T tmpData = top_->data;
        top_ = top_->next;
        delete previousHead;

        return tmpData;
    }
};
}
#endif
```

### Implement the pop function of a dynamic array. Resize if capacity is 25% or less the size. Return last element.

```
T& pop() {
    if (size_ == 0) {
      throw std::out_of_range("Nothing to pop");
    }

    // resize capacity to half if size is less then or equal to 25% of the capacity
    double difference = capacity_ / size_;
    if (difference <= 0.25) {
      resize(capacity_ / 2);
    }

    // remove last element
    size_--;

    // return previous last element (size_ is not zero based, starts at 1)
    return array_[size_];
}
```

### Implement a push_back method that appends a value to the end of a dynamic array

```
void push_back(const T &value) {
  if (size_ == capacity_) {
     resize(capacity_ * 2);
  }
  array_[size_] = value;
  size_++;
}
```

### Implement a constructor for a dynamic array

```
ArrayList<T>()
  :
  array_(new T[1]),
  size_(0),
  capacity_(1)
  {}
```

### Implement a destructor for a dynamic array

```
~ArrayList<T>() {
  delete[] array_;
  size_ = 0;
  capacity_ = 0;
}
```

### Implement an assignment operator for dynamic array in C++

```
ArrayList<T>& operator=(const ArrayList<T> &rhs) {
  if (this != &rhs) {
    *this->array_ = *(rhs.array_);
    this->size_ = rhs.size_;
    this->capacity_ = rhs.capacity_;
  }
  return *this;
}
```

### Implement a copy constructor for dynamic array in C++

```
explicit ArrayList<T>(const ArrayList<T> &obj) {
  size_ = obj.size_;
  capacity_ = obj.capacity_;
  array_ = new T[capacity_];
  *array_ = *(obj.array_);
}
```

### Implement the resize function of a dynamic array in C++

```
void resize(int capacity) {
    // allocate new array with double capacity
    T *newArray = new T[capacity];

    // copy elements to new allocated array
    for (int i = 0; i < capacity; i++) {
      newArray[i] = array_[i];
    }

    // delete old array
    delete[] array_;

    // update array pointer
    array_ = newArray;
    capacity_ = capacity;
}
```

### Implement the get function of a dynamic array in C++.

```
T get(int index) {
  if (index < 0 || index > size_) {
    throw std::out_of_range("Index out of bounds");
  }
  return array_[index];
}
```

### Implement the insert function of a dynamic array in C++. The elements should be shifted to make room for the new value.

```
void insert(int index, const T &value) {
  if (index < 0 || index > size_ || index + 1 > capacity_) {
    throw std::out_of_range("Index out of bounds");
  }
  // shift elements to the right
  for (int i = size_; i > index; i--) {
    array_[i] = array_[i - 1];
  }
  // insert element at position index
  array_[index] = value;
  size_ = size_ + 1;
}
```
### Implement the remove function from a dynamic array

```
void remove(int index) {
    if (index < 0 || index > size_) {
      throw std::out_of_range("Index out of bounds");
    }
    for (int i = index; i < size_ - 1; i++) {
      array_[i] = array_[i + 1];
    }
    size_ = size_ - 1;
}
```

## General

### What is a jagged array?

It is a multi-dimensional array, where the arrays are of different sizes.

### What is the Big O of inserting or deleting a element in the end of an array?

It is done in constant-time: Big O(1). We don't need to shift each element. We just do pointer arithmetic.

### Can arrays store multiple types of objects?

No, array need to store the same type of object (to be consistent with the size of each element), in order to do pointing arithmetic, and maintain the constant-time access to read and write.

### What is the Big O of inserting or deleting a element in the middle of an array?

Linear time: Big O(n).

In the worst case, we need to shift each element into the previous or next position, depending if we are inserting or deleting an element.

### What is the Big O of writing and reading from an array?

Constant-time: Big O(1).

### What is Log2(8)?

How many times do we have to multiply 2 to have 8? 3 times. 2 x 2 x 2 = 8.

### In C++, if we have an array of integers, if we do array + 2, how many bytes will the compiler jump? (considering that an integer has a size of 4 bytes).

8 bytes (4 x 2). pointer arithmetic in C++ takes into account the size of the object.

### Which are the most common data elements from an array list?

```
T *array_;
int size_;
int capacity_;
```

### Analyse the access log and quickly answer queries: does anybody access the service from this IP during the last hour? How many times? How many IP's were used to access the service during the last hour?

Store in hash table

### Given the unbalanced string "()([]", what character is on top of the stack when the for loop is finished?

The stack will contain a single value: "(". The procedure will push the initial "(", and then pop it to match the ")". It will then push "(", and push the "[". And pop the "[" to match the "]". The char "(" will remain on the stack.

### What are sentinel nodes?

They are nodes used with linked lists and trees as a traversal path terminator. This type of node does not hold or reference any data managed by the data structure. Do not forget that on an empty doubly linked list, the previous and next pointers point to the node itself.


### Given f(n) = 10 log(n) + 5 (log(n))^3 + 7 n + 3 n^2 + 6 n^3, what is the Big O of f(n)?

A: f(n) = O(n^3).

If a function f(n) is a sum of functions, one of which grows faster than the others, then the faster growing one
determines the order of f(n).
