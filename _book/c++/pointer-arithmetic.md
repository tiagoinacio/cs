# Pointer arithmetic and array indexing

The C++ language allows you to perform integer addition or subtraction operations on pointers. If `ptr` points to an integer, `ptr + 1` is the address of the next integer in memory after `ptr`. `ptr - 1` is the address of the previous integer before `ptr`.

Note that `ptr + 1` does not return the memory address after `ptr`, but the memory address of the next object of the type that `ptr` points to. If `ptr` points to an integer (assuming 4 bytes), `ptr + 3` means 3 integers (12 bytes) after `ptr`. If `ptr` points to a `char`, which is always 1 byte, `ptr + 3` means 3 chars (3 bytes) after `ptr`.

When calculating the result of a pointer arithmetic expression, the compiler always multiplies the integer operand by the size of the object being pointed to. This is called scaling.

Reference: from [learncpp](http://www.learncpp.com/cpp-tutorial/6-8a-pointer-arithmetic-and-array-indexing/)