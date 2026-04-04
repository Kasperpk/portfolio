## Enter the fibonacci problem
Let me perhaps start with an problem that any computer science student often is introduced to, namely the problem of calculating the sum of an Fibonacci sequence for some integer *n*. The problem is quite abstract but expose one to important tactics and means of which to think algorithmically. The Fibonacci sequence is a numerical sequence where each term is defined as the sum of the two preceding terms. In other words, for some integer _n_,

$$
F(n)=F(n−1)+F(n−2)
$$
Although this problem is on the number theoretically and mathematical side, it does have real-world origins. In fact, the sequence was first introduced by Leonardo of Pisa, also known as Fibonacci, in the 13th century to model the growth of a population of rabbits under idealized conditions. Since then, the Fibonacci sequence has appeared in many areas of mathematics, computer science, and even nature. What's fitting about this problem is that it can be tackled using different strategies, but also shows that the choice of strategy can have major implications, something that future problems with certainty also have. First of all let's understand the problem. The Fibonacci sequence is for all positive integers and the three first numbers in the sequence are 0,1,1, because the sequence does not go below 0. The fourth element in the sequence is the sum of the two previous in the sequence so 1 + 1 = 2. The fifth number in the fibonacci sequence is  then 1 + 2 = 3 and so on. The sequence quite quickly grows an already for tenth element it is 55 and 144 at the twelfth element. The question is how can we make use of our high-level language to solve such problem?

code example 1.25 recursive solution for Fibonacci sequence
```
python

def fibonacci(n):
	if n < 2:
		return n
	
	return fibonacci(n-1) + fibonacci(n-2)
```

Code example 1.5 shows an solution, one that uses recursive calls to the same function. Python has no problem with this as it can save the frame of the caller on the stack and if you run this algorithm, it will work just fine at least for reasonably low values of *n*. The issue is that once *n* exceeds something like 1000 the stack can no longer hold all the recursive calls and the interpreter throws an error after running for several seconds. What's the problem here? The problem with this recursive solution is that every time *n* grows then we have to make another two recursive calls. For example for something like *n* = 5, the recursive tree in figure 5.3 can be drawn. Already at 5, we see several calls to the same function. fib(2) is called at least three times. That's how we designed this algorithm. We call fib(5), which calls fib(4) and fib(3), fib(4) calls fib(3) and fib(2) and fib(3) calls fib(2) and fib(1) and so on. The recurrence relation for this naive solution can be written as T(n) = T(n-1) + T(n-2) + O(1). 
![](Recursive%20tree%20for%20fibonacci%20number.png|center)
Figure 5.3 call tree for recursive algorithm for Fibonacci sequence 

What else could we do to solve this problem? The answer is a bright idea found in *dynamic programming*. Dynamic programming is a algorithm paradigm which is useful for many general problems such as those using recursion. While some other paradigms like the *greedy* and *divide-and-conquer* works well for some particular problems, dynamic program does well on several occasions. The idea is to use something called *memoization.* There is no reason to calculate the same result twice, it would be much more efficient to store the results and then return that. The code example 1.26 shows the solution using dynamic programming. Running this code, shows that it now takes a split second to solve something like Fibonacci(1000). 

code example 1.26 recursive solution for Fibonacci sequence with memoization
```
python

def fibonacci(n, memo=None):
    if memo is None:
        memo = {}
                
    if n < 2:
        return n
    if n in memo:
        return memo[n]
    
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]
```

Having several swings at the same problems is very typically when it comes to programming where the first or ten first are not optimized to the extend possible. There is an even more sophisticated algorithm to solve the fibonacci sequence problem. This requires some thinkering and a brilliant idea. Code example 1.27 

code exmaple 1.27 a more efficient algorithm for finding fibonacci numbers
```
def fibonacci(n):  
    if n <= 1:  
        return n  
  
    prev, curr = 0, 1  
    for i in range(1, n):  
        prev, curr = curr, prev + curr  
  
    return curr
```
What this algorithm does is that it stores two variables prev, curr initialized to 0 and 1. Then it loops from 1 to $n$ setting updating prev and curr. Let's consider $n=5$. On the first iteration it sets $prev=1$ and $curr=0+1$. The next iteration at $i=2$ it sets $prev=1$ again and $curr = 1+1=2$ . Iteration where $i=3$, prev is updated to $prev=2$ and $curr=1+2=3$. Iteration four is setting $prev=3$ and $curr=2+3=5$ and this is the final iteration in the loop as as a range in python stops at the number $n$ excluding it. 
## Greatests common divisor algorithm
Another classical computer science problem is that of finding the greatest common divisor between two numbers say 5 and 15. Again we have several alternatives and we could simply use trial and error and it's not necessarily a need to use technology. For the numbers 5 and 15 we find that 5 is the largest common divisor between the two numbers since both numbers can be divided by 5, which is quite straight forward. The pair of numbers say 6 and 20 would instead have the greatest common divisor of 2. We would like an algorithm that can find this number for any two numbers such as 323010 and 392423 where trail and error no longer is viable. Instead of using trial and error we can write a naive solution by going from 1 to the sum of the two numbers and if that number divides both numbers without any remainder then that number is written as the current highest solution. That naive algorithm might look like this one below. 

code example 1.28 naive greates common divisor algorithm
```
def greatest_common_divisor(a,b):  
    max = 0  
    for d in range(1, a+b):  
        if a%d == 0 and b%d == 0:  
            max = d  
    return max
```
Are there any problems with this algorithm? This algorithm is O(a+b) and have linear magnitude we may write *O(n)*. 

Fortunately there have been some great ideas that helped solved this problem. There is a key lemma which comes from mathematics and number theory. The Greek mathematicians including Euclid were well known for their mathematical inventions among them the euclid algorithm for finding the greatest common divisor. Euclid kept track of something we might call a prime, the remainder of dividing a and b. For example take the two numbers 38 and 8. We integer divide 38 with 8, which is yields 4 with a remainder of 6. Now store 6 as a prime. We then run the same integer division but swapping the original b to a's place and putting in a prime for b, so we divide 8 with 6. This now yields 2 as you can put 6 into 8 one time and then there is 2 remaining. Now a prime is 2 and 6 is the b now swapped to a's place. We run the algorithm again with 6 and 2 which yields 0 since you can divide 2 with 6 three times and you will have no remainder. Once a prime reaches 0 the algortihm stops and we have found the solution as the previous a prime, in this case 2.  The python code for this algorithm now looks completely different as shown in code block  below

code example 1.29 euclids greatest common divisor algorithm
```
def greatest_common_divisor_euclid(a,b):  
    if b == 0:  
        return a  
    a_prime = a%b  
    return greatest_common_divisor_euclid(b, a_prime)
```

To see what difference this makes on runtime i printed out some statements using the time library in python. 

code example 1.30 code to measure runtime of algorithm
```
start_time = time.time()
print(greatest_common_divisor_euclid(43243244,23432423))  
print("It took %s seconds to complete the greatest_common_divisor_euclid function" % (time.time() - start_time)) 
 
start_time = time.time()
print(greatest_common_divisor(43243244,23432423))  
print("It took %s seconds to complete the greatest_common_divisor function" % (time.time() - start_time))
```
What this print output shows is that it took only microseconds to run the euclid algorithm version while the naive algorithm used 1,59 seconds. 

code example 1.31 console output of running the code from example 1.29
```
It took 4.0531158447265625e-06 seconds to complete the greatest_common_divisor_euclid function

It took 3.814697265625e-06 seconds to complete the greatest_common_divisor_euclid function

It took 1.5945367813110352 seconds to complete the greatest_common_divisor function
```
The reason for this is that at each step the euclids algorithm reduces the size of the numbers by a factor of 2 and takes about *log(ab)* steps which is much of an improvement over the linear time complexity of the naive algorithm. 

## Multiple roads to travel and Big-O notation
These two examples show that there are generally many ways to reach a certain solution. This is true for very many problems in life and other domains as well. What the two examples above also show is that finding improved algorithms has major implications for the runtimes and since computers do not have infinite computing power and memory finding the best one is an important task. The typical scenario is that the first solution we may come up with rarely is the optimal one, but this is still progress. It's often somewhat naive and do not take advantage of possible optimizations. For example in the fibonacci problem the naive recursive solution without dynamic programming quickly filled up the stack and so only for very small numbers of *n* it would work properly. The dynamic programming algorithm instead could solve for even very large *n*'s very fast. The solution could be improved even more with the brilliant insights about the pattern of the fibonacci sequence. The concept of choosing among multiple alternative ways of doing things to reach the best outcome is just as relevant for problems outside programming. For example in primary school we learn algortihms for arithmetic operations. Here we learn to stack numbers and the steps we need to compute addition, subtraction and so on. These algorithms are *correct* as they will always return the right answer if the steps are followed correctly. Sometimes we might just take a guess instead or use some mental tactics, particularly when the problems are trivial. This approach may not be a correct algorithm however even a wrong algorithm can be the best one in certain applications. That's why we have to consider the context in which we develop solutions because sometimes speed can be more important than consistency. 

For computational problems the running time depends on the number of steps that the computer has to perform. We may count them, for example in Cormen et al they count the number of steps that the insertion sort algorithm for which we will see a solution in the next chapter. The authors consider the number of steps in the best-case aswell as in the worst-case scenario. In the best case the input array is already sorted and so at each evaluation of the for loop the while loop is skipped and in that case the algorithm is growing linearly with input sizes something like *an + b* where *a* and *b* are some constants which runs on each loop, initializing some variables. 

The worst-case scenario is where the input array is completely reverse of being sorted. In this case at each iteration the numbers has to be moved all the way down the array. The runtime now becomes quadratic something like $an^2 + bn + c$. In this analysis we have left out some details which can influence runtime such as the programming language of choice and the hardware which runs the code. This is typically considered noise when computer scientists evaluate efficiency of algorithms. Computer scientist typically consider what the worst-case scenario is in terms of what they call time and space complexity, refering to counting the number of operations and memory used as $n$ grows large. They use *asymptotic* notation which  ignores constants and focus on the terms that dominate as input sizes grow. For example we can write O(n<sup>2</sup>) instead of 3n<sup>2</sup> + 5n + 2, because the squared term will dominate the runtime as *n* grows. The graphs in figure 5.4 and 5.5 shows the importance that the first term of the growth function. As *n* grows large enough n<sup>2</sup> begins to dominate and the remaining terms becomes insignificant. It's clear that if the squared term is less compared to the constant terms it will take a longer while before it starts to dominate the runtime, but eventually it will and therefore we still say this algortihm is runtime O(n<sup>2</sup>) 

![[Asymptotic growth of squared function]]
Figure 5.4 run-time comparison of linear runtime versus squared 

![[Asymptotic growth of squared function larger constant]]
Figure 5.5 run-time comparison of linear runtime versus squared 

The *O* is also called Big-O notation and it describes an upper bound on the running time something that is very important to have in mind when designing an algorithm. Alongside Big-O notation, there is Big-Omega which defines the lower bound for the algorithm and Big-Theta which is a tight bound. This is the mathematical ornament that is the measuring stick that  tells us how the cost of our solution scales as the input grows. An algorithm that performs well for ten elements may fail spectacularly for ten million. Big-O forces us to ask: _How does the work grow?_

For engineers, this perspective is practical. When we analyze a loop or a recursive call, we are not chasing symbols—we are estimating future cost. If a piece of code performs linear work inside a loop that itself runs linearly many times, we should immediately suspect quadratic growth. Big-O gives us the vocabulary to express that suspicion precisely.

In serious algorithmic work—especially in academic research—intuition is not enough. The runtime must be proven. A proof turns a performance claim into a guarantee. One common technique for recursive algorithms is the **substitution method**.

The substitution method follows a disciplined pattern:

1. **Form a hypothesis** about the growth rate (for example $O(n^2)$
2. **Assume** the bound holds for smaller inputs.
3. **Substitute** that assumption into the recurrence.
4. **Verify** that the inequality closes.

The key insight is that substitution is not a way of discovering the runtime. It is a way of confirming it. Discovery usually comes from expanding the recurrence a few steps, recognizing a pattern, and translating that pattern into a known sum or recursion depth. Substitution then formalizes what intuition suggests.

When engineers hear “quadratic time,” they often picture two nested loops. That image is useful—but incomplete. Quadratic growth can emerge even when no nested loop is visible. It appears whenever work accumulates in proportion to what has already been processed.

Consider a function that builds a report incrementally. For each new item, it recomputes a summary over everything seen so far:

```
def build_report(items):  
    report = []  
    for i in range(len(items)):  
        summary = summarize(items[:i+1])  
        report.append(summary)  
    return report
```

The structure looks innocent. There is only one explicit loop. But look at what happens inside that loop. On the first iteration, `summarize` processes one element. On the second, it processes two. On the third, three. By the time it reaches the nth element, it processes n items.
The total work performed is therefore
$1+2+3+⋯+n$

This is not a stylistic observation; it is a structural one. Each step grows slightly more expensive than the previous step. The cost accumulates. That accumulation is exactly what the recurrence
$T(n)=T(n−1)+n$ describes. To process $n$ items, we first process $n−1$ items, and then we pay an additional cost proportional to $n$.

If we expand that recurrence, it becomes a sum:

$T(n)=1+2+3+⋯+n$

That sum equals $\frac{n(n+1)}{2}$ Its dominant term is $\frac{n^2}{2}$​. The growth is therefore quadratic.

Nothing in the code announces this explicitly. There is no dramatic double loop. Yet the structure guarantees that as the dataset doubles, the work roughly quadruples. The algorithm feels linear when tested on small inputs, but its growth rate tells a different story.

The intellectual habit to cultivate is this: whenever an iteration performs work proportional to the amount of data already processed, suspect quadratic growth. The recurrence makes this precise; the substitution method proves it formally. But the deeper skill is recognizing the pattern before the proof is written. If, instead, the function maintained a running summary and updated it incrementally, each iteration would perform constant work. The recurrence would shift from

$T(n)=T(n−1)+n$

to

$T(n)=T(n−1)+1$ 

which unfolds into linear growth. A small structural change transforms quadratic scaling into linear scaling.

That is why runtime analysis matters. It disciplines the way we think about accumulation. It turns performance from an empirical observation into a predictable consequence of structure.
`
## From deterministic evaluation to probabilistic
Cormen et al contributes with their discussion on probabalistic analysis and randomized algorithms. So far the evaluation of runtime has been how it performs in the worst-case scenario. This gives us a clear answer but it is also quite pessimistic and we might need more nuanced view of how the algorithm performs over a distribution of input values. This is the idea behind probabilistic analysis and randomized algorithms. We can assume that the input follows a  probability distribution or that the algorithm itself is making random choices at runtime. These analysis can provide a more nuanced and insightful picture of how well/poort an algorithm really performs. Cormen and his co-authors spend a great deal of time writing on probabilities and also hand over some exercises such as exercise 5.4-1 from page 218. That exercise looks like the following: "How many people must there be in a room before the probability that someone has the same birthday as you do is at least 1/2? How many people must there be before the probability that at least two people have a birthday on July 4 is greater than 1/2?"

As we can see this is all probability theory and not so much about algorithms per se, however these questions are what underlies probabilistic analysis of program runtimes. If we assume that birthdays are uniformly distributed among the 365 days in a year (ignoring leap years) then we have that the probability that we do not share or match birthdays as

$P(different) = \frac {364} {365}$ 

The probability that one matches the birthday is 

$P(match) = 1 - (\frac {364} {365})^n$ 

We want to solve for $n$ in this equation where $(\frac {364} {365})^n \leq 0.5$. To do that we take the logarithm on both sides so we get get $n ln(\frac {364} {365}) \leq ln(0.5)$ and solving for $n$ we have $n \geq \frac {ln(0.5)} {ln(364/365)}$ which is approximately equal to $n \approx 253$. 

This is the logic behind the famous birthday paradox. They also have the example exercise here which states "You toss balls into b bins until some bin contains two balls. Each toss is independent, and each ball is equally likely to end up in any bin. What is the expected number of ball tosses?" 

Suppose we have bbb bins and we toss balls one at a time. Each ball independently lands in any bin with probability $1/b$. We stop as soon as some bin contains two balls. The question is: _how many tosses should we expect before this happens?_

A useful way to approach the problem is to look at the complementary event: the probability that **no collision has yet occurred**. After the first ball is thrown there can be no collision. When the second ball is thrown, it must avoid the bin of the first ball; this happens with probability $(b−1)/b$. When the third ball is thrown, it must avoid two bins, which happens with probability $(b−2)/b$. Continuing in this way, the probability that after kkk tosses every ball has landed in a different bin is

$P(\text{no collision after }k) = \frac{b}{b}\cdot \frac{b-1}{b}\cdot \frac{b-2}{b}\cdots \frac{b-k+1}{b}$.

This expression is exactly the same one that appears in the analysis of the **birthday paradox**. As kkk grows, the product shrinks rapidly, meaning that the chance that some bin already contains two balls becomes large surprisingly quickly.

A convenient approximation comes from observing that when bbb is reasonably large,

$P(\text{no collision after }k) \approx e^{-k(k-1)/(2b)}$.

The first collision typically occurs when this probability has dropped to about 1/21/21/2. Setting

$e^{-k(k-1)/(2b)} \approx \frac12$ ​

and solving for $k$ gives the estimate

$k \approx \sqrt{\frac{\pi b}{2}}$

Thus the expected number of tosses before some bin contains two balls grows on the order of the **square root of the number of bins**, not quadratically as one might first suspect.

To make this concrete, consider $b=10$. The estimate gives

$k \approx \sqrt{\frac{\pi\cdot10}{2}}  \approx 4$.

So with ten bins we should expect a collision after only about **four tosses on average**, far fewer than 100. The reason is that as we toss more balls, the number of **possible pairs of balls** grows roughly like $k^2/2$. Each pair has probability 1/b1/b1/b of landing in the same bin, so collisions accumulate quickly.

In summary, the expected number of ball tosses until some bin contains two balls is approximately

$E[T] \approx \sqrt{\frac{\pi b}{2}}$

a result that mirrors the well-known behavior of the birthday problem.
