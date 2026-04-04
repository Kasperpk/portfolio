Let's look at another algorithmic design or strategy to use. Not all problems can be expressed and solved using the greedy design and one alternative is the divide and conquer algorithmic paradigm which can be used to solve complex problems efficiently. The main idea is to break a problem into smaller subproblems, solve each subproblem independently, and then combine their solutions to solve the original problem. Th edivide and conquer algorithms is naturally recursive because it uses the same procedures to solve increasingly smaller subproblems. The general recipe for using this algorithmic design involves

1. **Divide:** Split the problem into two or more smaller subproblems.
2. **Conquer:** Solve each subproblem recursively. If the subproblem is small enough, solve it directly.
3. **Combine:** Merge the solutions of the subproblems to get the solution to the original problem.

Divide and conquer is widely used in computer science for designing efficient algorithms and is a key concept for mastering algorithmic problem-solving.

This approach can for example be applied to binary search algorithms, merge sort or quick sort algorithms. Below we will take a look at some of those problems which can be solved using this algorithmic paradigme. 

**Multiplying polynomials**
If we wan't to multiply large integers it might be useful to multiply polynomials and it turn out we can use the divide and conquer algorithm for this approach. One insight that helped solve this problem efficiently was made by a graduate student who realized that the original approach of dividing it into four multiplication subproblems could be reduced to three. I was introduced to this problem through the data structures and algorithms specialization course that i found online. If we have two polynomials $a$ and $b$ then multiplying them requires summing the pairwise products. For example consider $2x^3 + 4x^2 + 5x +10$ and $4x^3 + x^2 + 3x + 4$ multiplying these two polynomials means summing the pairs following pairs $2x^3 (4x^3 + x^2 + 3x + 4)$ + $4x^2 (4x^3+x^2+3x+4)$  + $5x(4x^3+x^2+3x+4)$ + $10(4x^3+x^2+3x+4)$. This is the distributive law that we use to multiply any two expressions. If we let  $2x^3 + 4x^2 + 5x$ be $a$ and $4x^3 + x^2 + 3x + 4$  be $b$ then we can write it as $a_1(b) + a_2(b) + a_3(b) + a_4(b)$ or more generally as $a_1(b)+ a_2(b) + ..a_n(b)$. To solve this using programming we can write the following algorithm

code exampel 6.1 algorithm to multiply polynomials
```
def multiply_polynomials(a,b,x):
    a = a.replace('x', x)
    b = b.replace('x', x)
    a_terms = [term.strip() for term in a.split('+')]
    b_terms = [term.strip() for term in b.split('+')]
    sums = 0
    for a_term in a_terms:
        for b_term in b_terms:
            sums = sums + (eval(a_term) * eval(b_term)) 

    return sums
```

Here i use a few built-in functions including .replace() so that i can take the polynomial string and replace all the x's with the value that needs to be passed in. 

**Sorting numbers using merge sort**
In programming we often encounter problems that are recursive in nature. That means we have to keep solving similar but often smaller subproblems. The merge sort algorithm applies exactly this idea to sorting an array of numbers using the genius algorithmic design idea called *divide-and-conquer*.   
To sort an array with the merge sort algorithm means we divide the problem by splitting the array in half, leaving us with two smaller subproblems. This is shown in the sketch in figure 1.1. The divide and conquer thinking is exceptionel when it comes to designing efficient algorithms. 
![[Sketches/merge sort|center]]
Figure 6.1 Merge sort algorithm
An important part of making such an algorithmic design is to have defined a base case for which the algorithm will stop recursively call itself. In this case it's when the division results in an array with one one element, because then it's already sorted.  When we analyze the running time of this algorithm we find that it is $O(n log(n))$ at worst, which is great improvement of the insertion algorithm which is $O(n^2)$ showcasing the important idea behind divide-and-conquer. 

We can use the idea of divide and conquer to solve a sorting problem and the merge sort algorithm is exactly that. It takes some input of integers and recursively break down the problem by dividing the array in half until it reaches the atomic units which we can then begin to merge back into a sorted array. As always we can begin with a sketch to better understand the problem at hand and how the proposed strategy of merge sort can help us. 

![[Sketches/Merge sort algorithm|center]]
Figure 6.2 Merge sort algorithm

From a drawing like this we may draw some pseudocode or control flow diagram which shows how the program will behave. Pseudocode is agnostic from the programming language we will use to implement the solution and therefore some specific details are omitted. In programmign we often have to initialize some variables and other data structures that can help us guide the process. For example in the lecture i am watching the pseudocode for the merge sort looks like the following

![[Merge sort pseudocode|center]]
Figure 6.3
Here we have some output list as well as two input list A and B. The pseudocode then shows how we could construct the final list that merges the two now sorted lists. We can analyze or estimate the running time based on the pseudocode by counting the number of operations that will be performed. 

The merge sort algorithm uses at most $6n log_2 n + 6n$ operations according to the claim in the lecture. We can make a proof of that statement using a recursive tree. Sarting from the top of the tree we have two childs every time we split up the original array and that we have to do $log_2 (n+1)$ times. At each level there are $2^j$ subproblems that is at level 3 there are $2^3 = 8$ sub problems and so on. The size of the problem shrinks at each level as fewer and fewer items are in the arrays until we get to the base case. More particularly it shrinks at each level to be $\frac n {2^j}$, so that at the level three the size of the problems is 1, as there is only a single element to sort. 

![[Sketches/Merge sort analysis|center]]
Figure 6.4

**The quick sort algorithm**
Another sorting algorithm is the quick sort algorithm. This is an algorithm where a **pivot** is chosen. Each element of the array is compared to the pivot and put into one of two subarrays. Then we have a subproblem, which again can be solved choosing a pivot making a recursive call with the subarrays. The quicksort can't really be solved using the *greedy* algorithm paradigme so again we consider the divide and conquer paradigme. 

Much like merge sort divides and conquers the problem by partitioning (rearranging) the array into two sub arrays $A[p:q-1]$ and $A[q+1:r]$ where each element on the low side is less than the chosen pivot $q$ and vice versa. Figure 6.5 shows the sketch of the how the array A is halfed around the pivot 6 such that all elements in the left half is less than or equal to 6 and in the right half all elements are greater than 6.  
![[Quick sort sketch|center]]
Figure 6.5. Quick sort with pivot 6

Calling the quicksort recursively then accomplishes what we want to do. The pseudocode from Cormen et al for the quick sort is as follows

```
Quicksort(A,p,r)

if p < r
	// Partition the subarray around the pivot, which ends up in A[q]
	q = Partition(A,p,r)
	Quicksort(A, p,q-1) // recursively sort the low side
	Quicksort(A,q+1,r) // recursively sort the high side
```

It's the partiton algorithm that is the key part of the quicksort procedure and it's the one that rearranges the subarray $A[p:r]$ in place, returning the index of the dividing point (pivot). If we look closer at the partition algorithm it's job is to rearrange the array and recursive subarrays and return $q$ which is the index that splits the array in half. If we take an example of an array $A$ defined as $A = ⟨13, 19, 9, 5, 12, 8, 7, 4, 21, 2, 6, 11⟩$ the partition algorithm will then take the input array, then $p$ and $r$. To begin with $p$ is the first element so 1 and the $r$ is the pivot with the value $11$. The following sketch shows how pointers again are very useful in proceeding the program by keeping track of the current index that is the highest in the low side and the current element we compare with. 

![[Sketches/Quicksort algorithm|center]]
Figure 6.6 Quick sort procedure sketch

By looking at the sketch above we can see that the algorithm will go through every element and compare it to the pivot which is the bulk of the procedure. This takes $O(n)$ time and every call to quicksort produces two recursive calls and the depth of the recursion tree is $O(log \space n)$ when the pivot is balanced. What it means for the pivot to be balanced can be noticed in the sketch figure 6.6. Because the pivot is balanced (not the minimum or maximum value in the array) some elements are never compared such as 5 and 19 because of the pivot 11 these two numbers land in their subarray without being compared. If instead the pivot was always chosen as the minimum or maximum element then the quicksort algorithm would instead have a running time of $O(n^2)$. We can understand this because if we choose for example 21 as the pivot above we will not have partitioned the array any better than before, the only thing we have now sorted out is that 21 is the maximum element and this suffices to the same running time as selection or insertion sort which sorts values one value at the time. The brilliance of this algorithm comes from understanding that we can divide and conquer by making smaller subproblems and when the pivot is balanced the expected running time is $O(n log n)$ making it prefered for many practical purposes. Therefore in practice three elements, the first, last and middle are sorted and the middle one is picked as pivot to make sure it's not one of the extremes. 

Here is my python implementation of the quick sort algorithm. It is made of the partition procedure which does the bulk of the work, while the quick_sort simply calls the partition and then two recursive calls thereafter. 
```
def partition(array, low, high):  
    pivot = array[high]  
    current_index_in_low_array = low-1  
    for index in range(low, high):  
  
        if array[index] <= pivot:  
            current_index_in_low_array += 1  
            array[current_index_in_low_array], array[index] = array[index], array[current_index_in_low_array]  
  
    array[current_index_in_low_array+1], array[high] = array[high], array[current_index_in_low_array+1]  
   
    return current_index_in_low_array + 1
```

```
def quick_sort(array, low=0, high=None):  
    if high is None:  
        high = len(array) - 1  
    if low < high:  
        pivot_index = partition(array, low, high)  
        quick_sort(array, low, pivot_index-1)  
        quick_sort(array, pivot_index+1, high)  
    return array
```



