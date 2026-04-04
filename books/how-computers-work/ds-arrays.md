Arrays represent contingious areas of memory and have constant read and write access to any element in the array. This is because the address can be calculated by compilers and interprenters using the formula:
$$
addresIndexI = baseAdress + ElementSize * (I - firstIndex)
$$
Multi-dimensional arrays can be constructed and be accessed using row or column major. 

![[Multi-dimensional array]]
The operations on the array and the runtimes are 

| Operation             | Runtime |
| --------------------- | ------- |
| read/write            | O(1)    |
| add to end            | O(1)    |
| add to beginning      | O(n)    |
| remove from beginning | O(n)    |
| remove from end       | O(1)    |
| Add middle            | O(n)    |
| Remove middle         | O(n)    |

#flashcards 
What is the data structure array efficient at?:: It's efficient at reading and writing from any position in the contigious area of memory.
<!--SR:!2026-01-19,64,310-->
What operations cost more working with arrays?:: The operation of add and removing operations from the beginning and middle because this requires us to move the entire set of elements in memory.
<!--SR:!2025-12-23,37,290-->