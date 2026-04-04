In everyday life we often try to sort things out. We sort our notes, our books, things, people. It's also viewed as one of the fundamental problems in computing as many applications of computer science needs to sort. Understanding sorting is typically at the start of some computer science curricilum as it's one of the first steps to mastering programming and computer science in general. There has been developed several sorting algorithms the first one we will look at being the insertion sort algorithm. 

code example 4.1 insertion sort algorithm
```
def insertion_sort(n, numbers):  
  
    for i in range(1, n):  
        key = numbers[i]  
        j = i-1  
        while j >= 0 and numbers[j] > key:  
            numbers[j+1] = numbers[j]  
            j=j-1  
        numbers[j+1] = key  
    return numbers
```

Insertion sort introduces a _for loop_, one of the most common control structures in programming. The insertion sort loops over every number in the array and store the value in some variable here $key$. It begins from the next to first number and checks if the previous number is greater, if so it swaps the numbers around and continue to check until it finds a smaller number or reach the begining of the array. At that point in inserts the current $key$ variable. This procedure looks much like how people would sort a hand of cards (Cormen et al, p 46). If we analyze the running time then in the worst case scenario the sort order is exactly reverse. That means for every number we have to go through the entire array and we end up with a $O(n^2)$ running time. 

Selection sort is another well known sorting algorithm and it works by finding the index of the minimum value in the array and inserts it at the start of the array which is constantly moved forward one iteration at the time. This algorithm has a running time that is similar to insertion sort because it uses the same nested looping. In total the running time is made up of 
1. The running time for the calls to finding the index of the minimum value
2. The running time for swapping the element
3. The running time for the loop over all items

The first two parts are linearly bounded and take a constant time to perform for each element. Similarly the third part is linear because we have to loop over positions in the array. 

There are other sorting algorithms some of which achieve quite good performance on larger input sizes where insertion sort can struggle in worst cases. The merge sort algorithm, which i will introduce in the coming chapter achieves the asymptotic performance of $O(n \space log \space n)$. Heapsort and quicksort are two additional algorithms which also are good alternatives. 

**Using heaps to sort things**
In line with Cormen et al presentation of sorting algorithms i will introduce the heap sort algorithm which uses a particular data structure called a *heap*. A heap is a data structure that can be viewed as a binary tree and looking at it conceptually the data stored in a heap might be visualized as follows, here a max heap where the root node of the tree is the highest number in the array. 
![](Binary%20max%20heap.png)
Figure 4.1 max heap sketch

In memory it would be a contingious string of elements as shown here below. 
```
42 | 29 | 18 | 14 | 7 | 18 | 7 | 11 | 12 | 7
```
In the max heap as shown here the property has to hold that the child nodes are not greater than the parent nodes. In a min-heap the organization is reversed so that the child nodes are greater than or equal to the parent. The heap allow us to perform operations like the following here:

* size(): returns the size of the heap meaning the number of elements
* heapify(): ensures that the heap maintains the heap property
* heapsort(): sorts an array in place in O(n log n) time

In addition it can be used to implement a priority queue, something which will be shown later. The heapify algorithm is the one that brings the heap into the right order and it does so by comparing the child elements with the parent and recursively call the algorithm on this subtree. As an exercise Cormen et al asks to illustrate the operation of MAX HEAPIFY(A, 3) on the array A = 〈27, 17, 3, 16, 13, 10, 1, 5, 7, 12, 4, 8, 9, 0〉.  Here in figure 4.2 we can see how it starts from index *i* = 3, then compares against the left and right child, find that 10 is greater than 3 and swaps the elements. It then continues to do that until the structure is again upheld. 

![[01 Computer engineering and architecture/sketches/max heapify procedure|center]]
Figure 4.2 example of heapify procedure

It works by **pushing a node down the heap** until the heap property is satisfied. If the value at the root is **smaller than every node below it**, it will move **all the way to a leaf**. The length of that path equals the **height of the heap**. For a heap with $n$ nodes: $\text{height} = \lfloor \log_2 n\rfloor$ 

So the algorithm may take **at least logarithmic time** at the worst case. As mentioned the heap can also be a min-heap which means each parent should be smaller than it's children. The pseudocode for the min heapify can be seen here below. 

code example 4.2 min heapify pseudocode
```
MIN-HEAPIFY(A, i)

	l = LEFT(i)
	r = RIGHT(i)
	smallest = i
	if l ≤ heap-size[A] and A[l] < A[i]
	    smallest = l
	else
	    smallest = i
	if r ≤ heap-size[A] and A[r] < A[smallest]
	    smallest = r
	if smallest ≠ i
	    exchange A[i] with A[smallest]
	    MIN-HEAPIFY(A, smallest)
```

The running time will also be $O(log \space n)$ as such they are asymptotically identical. Another question that Cormen poses is "what is the effect of calling MAX-HEAPIFY(A, i) when the element A[i] is larger than its children?". The answer here is that nothing will happen as the procedure only checks from the current node and down. If i>A.heap_size/2i > A.heap\_size/2i>A.heap_size/2, node i is a **leaf** and has no children. Therefore `MAX-HEAPIFY` performs no swaps and terminates immediately, taking **Θ(1)** time. 

Cormen et al remarks that some compilers might be generating inefficient code for recursive structures and therefore we might think of an algorithm that uses a loop structure. 

```
MAX-HEAPIFY(A, i)

while TRUE

    l = LEFT(i)
    r = RIGHT(i)
    if l ≤ heap-size[A] and A[l] > A[i]
        largest = l
    else
        largest = i
    if r ≤ heap-size[A] and A[r] > A[largest]
        largest = r
    if largest == i
        return
    exchange A[i] with A[largest]
    i = largest
```

The heapsort algorithm itself uses the heap structure and if the array is not already in this structure it would begin by building heap from the array. Then it continously pop of the root element becuase we know that this must be the largest element in a max heap and every time it has popped that element it calls the max_heapify() procedure with the remaining elements. Consider the array A = ⟨6, 13, 2, 25, 7, 17, 20, 9, 4⟩. If we represent that as a binary tree to begin with we have the following tree where the left child is 2i and the right child is 2i+1. It's easy to see that this does not satisfy the max heap condition because several child nodes are greater than the node above them. 

![](binary%20tree.png)
If we look at how the build heap algorithm will start from original array and turn it into one that satisfy the max heap property. It starts and index n/2 and compares that to the nodes below it. If one or both of them are greater, then swap the elements picking the greatest of them. Then it compares against the next subtree and if it's a leaf node then it moves to the next node in this case at index n/2 -1 and so on until it reaches the very first element of the array. 
![[Sketches/max heapify|center]]
Now we can begin to sort the numbers using the heap sort algorithm. We swap out the element at index 1 which is 25 with the element that is the last in the array here at index 9 which is 4. We then call max heapify again on the array such that 4 now trickles down and the maximum number again is lifted to the root node. Given that we first need an algorithm to build a max heap from an array of numbers we should focus on having pseudocode for that algorithm.

```
def build_heap(array)
	start_index = 2/n
	for index in range(start_index, 0, -1):
		while array[start_index] < array[start_index]*2 and start_index*2<=len(array):
			array[start_index], array[start_index]*2 = array[start_index]*2, array[start_index]
			start_index = start_index*2
	
	return array
	
```






