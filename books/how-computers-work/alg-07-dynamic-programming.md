The term *dynamic programming* originate back to the 1950s, when programming was "an esoteric activity practiced by so few people as to not even merit a name." (p. 165, algorithms). Programming meant planning back then and dynamic programming "was conceived to optimally plan multistage processes." A dag can represent such a process where each node denotes a state, the leftmost node is the starting point, and the edges leaving a state represent possible actions, leading to different states in the next unit of time.  

Dynamic programming is a powerful algorithmic paradigme that is able to be applied to a broad range of problems, typically optimization problems. Optimization problems typically have multiple possible solutions for which we want to select the optimal one. To solve a problem with dynamic programming involves 
1. Characterizing the structure of an optimal solution 
2. Recursively define the value of an optimal solution 
3. Compute the value of an optimal solution, typically in a bottom-up fashion
4. Construct an optimal solution from computed information
(p. 481, Cormen et al).  

Similarly the authors of algorithms describes how dynamic programming starts of by asking the question: *What are the subproblems?* (p. 165, algorithms). 

**Edit distance problem**
A well known problem in computer science is the edit distance. It's the minimum inserts, deleteds and edits needed to make to strings identical. The subproblem here is one that "should go part of the way toward solving the whole problem" (p. 165, algorithms). In the case of the two strings, exponential and polynomial.

![[Edit distance]]
A subproblem here could be E(i,j) where i refers to the i'th element of string number one and j refers to the j'th element of string number two For example looking at EXPONEN and POLYN entails the subproblem E(7,5). First let's consider the rightmost column x[i] and y[j]. There can only be three types of actions, either we insert value, substitute or delete. In this case they are aligned so the solution here is keep the alignment for a cost of 0. The order at which we solve the subproblems is not important as long as the subproblems E(i-1,j), E(i,j-1) and E(i-1,j-1) are handled before E(i,j). 

Finally the last thing that remains is the **base case**. The very smallest subproblem. In this scenario it is E(o,.) and E(.,0). The edit distance E(0,j) is the distance between the 0-length prefix of x, namely the empty string and the first j letters of y, clearly j. Similarly E(i,0) = i. 

The figures here show a) the table of subproblems and that E(i-1,j-1), E(i-1,j) and E(i,j-1) needs to be filled in before E(i,j). Then the matrix (b) that shows the values found by dynamic programming. 
![](Table%20of%20subproblems%20and%20values%20found%20by%20dynamic%20programming.png)
The pseudocode for the algorithm may be written as follows

```
for i = 0,1,2,...,m:
	E(i,0) = i
for j = 1,2,...,n:
	E(0,j) = j
for i = 1,2,...,m:
	for j = 1,2,..,n:
		E(i,j) = min{E(i-1,j) + 1,E(i,j -1) + 1, E(i-1,j-1) + diff(i,j)}
return E(m,n)
```

There is an **underlying dag** behind every dynamic program. Each node represent a subproblem, and each edge as a precedence constraint on the order in which the subproblems can be tackled. nodes between *u*<sub>1</sub> ... *u*<sub>k</sub> point to *u* means that subproblem *u* can first be solved once the answers to  u<sub>1</sub> ... u<sub>k</sub> are known. 

**The fibonacci problem recursive and dynamic solution**
The fibonacci problem is sort of the hello world of studying algorithms. It's an interesting problem that can be solved in many different ways and thus provides a good starting point for working with different algortihms. A *recursive* solution can be elegant, but for this problem can also cause some problems. The recursive tree below may shows that for calculating fib(5) the algorithm calculates the same values several times. The fib(2), fib(3), fib(1) and so on are recalculated several times leading to an inefficient solution that explodes exponentially as *n* grows.
![](Recursive%20tree%20for%20fibonacci%20number.png)
Dynamic programming deals with this problem by memoizing the values previously calculated. An array can be used to store the values for each level at the corresponding index in the array. This array is initialized to 0 for each index value. 

```
def fib(n, memo):
	if memo[n] != null:
		return memo[n]
	if n == 1 or n == 2:
		result = 1 # important to store result and not return directly
	else:
		result = fib(n-1) + fib(n-2)
	memo[n] = result # store the result in memo at index n. 
	
	return result
```

The time complexity here is T(n) = O(n). 
Another approach is the *bottom-up* and here is the pseudocode. The good thing about the bottom_up approach is that the call stack is not reaching limit at high values of n. The memory usage here is O(n). 
```
def fib_bottom_up(n):
	if n == 1 or n == 2:
		return 1
	bottom_up = [0] * (n+1)
	bottom_up[1] = 1
	bottom_up[2] = 1
	for i from 3 to n:
		bottom_up[i] = bottom_up(i-1) + bottom_up(i-2)
	return bottom_up(n)
```

Compute the edit distance between two strings.
* Input. Two strings.
* Output. The minimum number of single-symbol insertions, deletions, and substitutions to transform one string into the other one.

Let's take an example. It's always good to visualize a problem before embarking on it. That is how to solve it. This DP table shows the cost at each state where at each there are two main scenarios. 
1) The characters of the string line up, the cost is 0 and here it is the minimum of the previous step
2) The characters do not line up. Here there are two possible options. It's possible to insert a value into one of the strings, delete a value or substitute a value at a cost of one.
![[Edit distance table DP]]
The *edit distance* between these two strings is shown in the last value in this DP table. It's 3. The algorithm for this problem is as follows. Here 
3) two variables are initialized. These are used to build the matrix using list comprehension. 
4) two for loops populate the matrix for the first row and first column which is equal to the index of that character in the string. 
5) A nested loop goes through every combination of i,j to calculate the edit distance. If the two characters align then the matrix cell for that is filled with the previous value, that is initialized at 0. If the two characters do not align then matrix cell is the minimum value of the neighboring cells corresponding to deletions if dp [i-1] [j] [j] is chosen. Looking above that corresponds to going horizontal, going vertical 

```
    n = len(s1)
    m = len(s2)
    dp = [[0] * (m + 1) for _ in range(n + 1)]
    
    for i in range(n+1):
        dp[i][0] = i

    for j in range(m+1):
        dp[0][j] = j
    
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(
                    dp[i-1][j], # deletion
                    dp[i][j-1], # insertion
                    dp[i-1][j-1] #substitution
                )
    return dp[n][m]
```

**Learnings**
Visualizing a problem and spending time contemplating it is really valueable and necessary. DP is really powerful tool and again by creating an array, here two dimensional matrix we can use this to build our solution. It requires insights and thinking just like the previous problem the primitive calculator. 

Consider a well known computer science problem of finding the highest common divisor between two numbers, something which is used for cryptogrophy. This is important for example for online transaction systems. There are many ways to make this solution. 

*A naive solution*
For example a naive one would do something like looping over every digit from 1 to the sum of the two numbers storing whenever the result of the iterator i/a and i/b are equal, thus being a common divisor. At the end of the loop if we overwrite the variable, the largest or greatest common divisor would be stored in that variable. It would take thousands of years to find the best answer for very large numbers as the algorithm has a runtime of (a+b) number of steps. 

*Euclidian approach*
Another approach is the one suggested here below. The insight here is that you can use something called the *lemma* which can mathematically be proven that gcd(a,b) = gcd(a', b) = gcd(b, a'), where a' is the remainder after integer dividing a with b.   
```
def euclidGCD(a,b):
    if b == 0:
        return a

    lemma = a % b

    return euclidGCD(b, lemma)

if __name__ == "__main__":
    a,b = map(int, input().split())
    result = euclidGCD(a,b)
```

**Understand the problem**
Compute the maximum length of a common subsequence of two sequences.
- Input: Two sequences.
- Output: The maximum length of a common subsequence.

![](Longest%20common%20subsequence%20of%20two%20sequences.png)
So this problem is about finding the longest possible subsquence that is common among the two. The subsequences should be in the same order but does not have to be contingiously. A few examples. Consider the sequences A and B.

A = [1, 3, 4, 1, 2, 1, 3]
B = [3, 4, 1, 2, 1, 3]

The sequence 3,4,1,2,1,3 exists in both sequences which is quite obvious and therefore the longest common subsequence is of length 6. 

A = [7, 5, 3, 2, 6, 9, 4]
B = [1, 7, 9]

Here the longest subsequence is (7,9), (3,4) or (2,9). 

It makes sense to start from the two first elements in the sequences and comparing them. This gives us two subproblems. If they are equal we can compare the remaining elements and add 1, or if not equal the longest common subsequence could be in either of the two cases shown in the bottom.

![[LCS]]
In dynamic programming like this with two sequences we can create a table as a matrix that can provide intuition for the solution. Here first we compare 7 with 7. There is a match, that means we can move on to the first subproblem which corresponds to going diagonal. Then we compare the subsequence 2,3,4 and 5,2,4. Comparing 2 and 5 does not match gives us two subproblems and we return the max between comparing the subsequences 2,3,4 and 2,4 meaning going down. This gives us a diagonal move again because 2 equals 2. This give sus the subproblem 4 and 3,4. Since 4 and 3 don't match we compare the max of going vertical and horizontal. Since comparing 3,4 with an empty string returns 0 and comparing 4,4 returns one we go right. At this point we have found the solution and as we back track we can sum up the longest common subsequence to be 3. 
![[DP table]]
#keyinsight 
Finding the right subproblems takes creativity and experimentation. 



**Recurrence relation and base case**
The recurrence relation is the mathematical expression of the problem’s structure. The problem is solved by referring to _smaller versions_ of the same problem. That’s the essence of dynamic programming.

So, if `MinCoins(m)` is the minimum number of coins needed to make `m`, then:

$$
MinCoins(m)=1+min⁡(MinCoins(m−1),MinCoins(m−3),MinCoins(m−4))
$$
This says:

> To make `m`, take the _minimum_ of the solutions to `m-1`, `m-3`, and `m-4`, then add 1 (because you're using one more coin, either of 1, 3, or 4).

The base case for the problem is 
$$
MinCoins(0)=0
$$
> Making zero value needs zero coins.

**The DP table**
Dynamic programming is typically done either **top-down with memoization** or **bottom-up with a table**. We want to understand how the solution emerges from the table.

| money | MinCoins(money) |
| ----- | --------------- |
| 0     | 0               |
| 1     | 1               |
| 2     | 2               |
| 3     | 1               |
| 4     | 1               |
| 5     | 2               |
| 6     | 2               |
| 7     | 2               |
| 8     | 2               |
| 9     | 3               |
| 10    | 4               |
To solve `MinCoins(m)`, consider using each coin `c` from the available denominations. For each `c`, solve `MinCoins(m - c)`, and take the **minimum** across all valid coins. Then add 1 (for the coin you just used). The base case is `MinCoins(0) = 0`. The recursion tree here shows that this problem have overlapping subproblems, why dynamic programming can be effective for solving it. 
![[Recurrence tree DP|center]]

| money | MinCoins(money) | Explanation                        |
| ----- | --------------- | ---------------------------------- |
| 0     | 0               | base case                          |
| 1     | 1               | minCoins(1)                        |
| 2     | 2               | sum of two minCoins(1) subproblems |
| 3     | 1               | minCoins(3)                        |
| 4     | 1               | minCoins(4)                        |
| 5     | 2               | minCoins(4) + minCoins(1)          |
| 6     | 2               | minCoins(3) + minCoins(3)          |
| 7     | 2               | minCoins(4) + minCoins(3)          |
| 8     | 2               | minCoins(4) + minCoins(4)          |
| 9     | 3               | minCoins(3) + minCoins(6)          |
| 10    | 3               | minCoins(4) + minCoins(6)          |
1. Write a function signature in pseudocode for computing the minimum number of coins:
```
	function MinCoins(amount, denominations):
		dp_array = [amount + 1] * (amount + 1) # setting up DP array
		dp_array[0] = 0
		for a in range(1, amount + 1)
			for c in coins:
				if a - c >= 0:
					dp[a] = min(dp[a], 1 + dp[a-c])
		return dp[amount] if dp[amount] != amount + 1 else return -1
```
    