As programmers have tackled computational problems over the years, recurring ideas have crystallized into paradigms. In algorithm design, these paradigms provide reusable ways of thinking about problems. Insertion sort, introduced in Section 2, follows an incremental approach: it iterates through the array and inserts each element into an already sorted prefix (Cormen et al. 2022, chap 2). This is a logical way of approaching sorting a set of elements. More sophistacted designs also exists among them the well known greedy algorithm paradigme. 

There are four main ingredients when it comes to greedy algorithm:
* The **safe choice:** A choice is safe if there it's an optimal solution consistent with this first choice
* The proof that this is the safe choice
* Solve subproblems
* Estimate runtimes

Some problems have obvious greedy algorithm solutions, for example if you had to concatenate a list of single digits to construct the highest possible number. That will always entail putting the largest digit to the left, then solving for the remaining digits. This is a **safe choice**. If you use the same greedy strategy on numbers with multiple digits like ([2, 21]) then it would return 212 and in this case the greedy strategy fails because the correct solution is 221 (concatenating 2 with 21). Thus, there are _rare_ cases when a greedy strategy works and to ensure that one should be able to prove its correctness a priori keeping in mind that there is no reason why a sequence of _locally_ optimal moves leads to a _global_ optimum.

Another classical problem is the knapsack problem and we can apply the greedy algorithmic paradigme for this problem. Here is the problem statement

Find the maximal value of items that fit into the backpack. The inputs into the problem is the capacity of a backpack $W$ as well as the weights $(w1, . . . , wn)$ and costs $(c1, . . . , cn)$ of $n$ different items. The output is the the maximum total value of fractions of items that fit into the backpack of the given capacity: i.e., the maximum value of $c1 · f1 + · · · + cn · fn$ such that $w1 · f1 + · · · + wn · fn ≤ W$ and $0 ≤ fi ≤ 1$ for all i (fi is the fraction of the i-th item taken to the backpack).

Consider the following input parameters with a knapsack of total capacity of 9 and three items with weight 5,4 and 3. 
![[Sketches/Knapsack problem greedy algorithm|center]]
Figure 1.2 Sketch of knapsack problem

Solving this problem using a greedy algorithm means defining a safe choice and as we want to maximize the total amount of loot in the knapsack we want to take as much as possible of the item with the maximum value per unit. In this example we could take the first two items for a total value of 58 dollars. A better solution is to take the first item, then the third item and 1/4 of the second item, this yields a total value of $61. But there is an ever better solution. That is to take the third item, the second item and 2/5 of the first item for a total value of $64. The reason it is most optimal to take the third item is that it has the highest value per unit weight of $8 while the others are $7 and $6. 

We might have the following procedure:
* While the knapsack is not full
* Chooise item with maximum value 
* If item fits into knapsack, take all of it
* Otherwise take so much as to fill the knapsack
* Return total value and amounts taken

The following algorithm makes use of a helper function *best_item()* which finds the current item with the highest value per unit weight. The helper function is called from the *knapsack()* procedure which starts by initializing two variables first amounts which is holding the number of units taken of the items and total value which holds the total value of the knapsack. 

code example 1.1 knapsack algorithm
```
def best_item(items):  
    max_value_per_weight = 0  
    best_item = 0  
    for i in range(1, len(items)):  
        if items[i][0] > 0:  
            if items[i][1]/items[i][0] > max_value_per_weight:  
                max_value_per_weight = items[i][1]/items[i][0]  
            best_item = i  
    return best_item
    

def knapsack(w, items):  
    amounts = [0] * len(items)  
    total_value = 0  
    for i in range(0, len(items)):
	    # check if knapsack capacity is full  
        if w == 0:  
            return (total_value, amounts)  
        
		# use helper function to find best item    
        i = best_item(items=items)  
        
        # find the number of units to take of the best item
        a = min(items[i][0], w)  
          
        # calculate the new total value of knapsack   
		total_value = total_value+a*(items[i][1]/items[i][0])  
          
        # decrease the amount of item i with unit a   
		items[i][0] = items[i][0]-a  
          
        # reflect that we took a units of weight of the item at position i  
        amounts[i] = amounts[i] + a  
        w = w - a  
    return total_value, amounts
```

The major challenge with this algorithm is that it runs two for loops. First the algorithm which finds the best item has to run at $O(n)$ and then the knapsack procedure itself also runs at $O(n)$ which means the running time of this algorithms is $O(n^2)$. A brilliant idea here is to first sort the list of items descending order of value per unit. This means we can avoid the helper function. Since we know sorting can be done in running time $O(n \space log \space n)$ 

To do this we may use an insertion sort algorithm and then calling the knapsack procedure 

code example 1.2 insertion sort algorithm to improve the knapsack problem
```
def sort_items(items):  
    for i in range(0, len(items)):  
        key = items[i]  
        j = i-1  
        unit_value = items[i][1] / items[i][0]  
        while j >= 0 and unit_value > items[j][1]/items[j][0]:  
            items[j+1] = items[j]  
            j-=1  
        items[j+1] = key  
  
    return items
```

code example 1.3 improved knapsack algorithm
```
def knapsack(w, items):  
    items = sort_items(items)  
    amounts = [0] * len(items)  
    total_value = 0  
    for i in range(0, len(items)):  
        if w == 0:  
            return (total_value, amounts)  
  
        a = min(items[i][0], w)  
  
        # calculate the new total value of knapsack  
        total_value = total_value+a*(items[i][1]/items[i][0])  
  
        # decrease the amount of item i with unit a  
        items[i][0] = items[i][0]-a  
  
        # reflect that we took a units of weight of the item at position i  
        amounts[i] = amounts[i] + a  
        w = w - a  
    return total_value, amounts
```

To show that this works i made a very simple example with three items with the following values 

items = (1,2), (5,28), (3,24) and then calling the procedure with the inputs knapsack(5, items). The result from the greedy algorithm is (35.2, (3, 2, 0)) which is first the value of the knapsack 35.2 and we can see that is 3 units of the most valueable item and 2 units of the second most. 

This example shows that we incorporate many of ideas we have previously discovered about algorithms to optimize and design for other seemingly unrelated problems. 

Another challenge we can solve with a greedy algorithm is the money change problems, another classic toy example in computer science. The problem is as such. You get some integer which is a value of money you need to get someone back in change. You then have a collection of denominations such as 1,5,10 which you can use to change that number of coins into. The greedy solution chooses a safe choice that might only be locally optimal and so we need a strong proof that it is also globally optimal. In this situation the safe choice might be to choose the highest possible coin value we can and so we get a very simple procedure that looks at the current change needed to give back. In code example 1.4 the greedy algorithm design shows how this approach goes about solving the problem. 

code example 1.4 money change greedy algorithm design
```
def money_change(n):  
    '''  
  
    :param n: integer coin    :return: the minimum number of coins with denominations 1,5,10 that  
    changes that money    '''
      
    num_coins = 0  
    coin_value = n  
    while coin_value != 0:  
  
        if coin_value >= 10:  
            coin_value = coin_value - 10  
            num_coins += 1  
  
        elif coin_value >= 5:  
            coin_value = coin_value - 5  
            num_coins += 1  
  
        else:  
            coin_value = coin_value - 1  
            num_coins += 1  
    return num_coins
```

The third algortihm i know is called the *car fueling* problem from the data structures and algorithms specialization from coursera. This problem is about finding the number of refills that a car need when travelining between to the start and stop. The inputs is the number of miles between the start and stop, the miles the car can travel on a full tank, number of gas stations and then distances between the gas stations. 
![](car%20fueling%20problem.png)
1.3 Car fueling problem

The sketch above helps us understand exactly what the problem is about and that we have to somehow get from A to B if possible given the constraints on car milage, gas station distances and distances between A and B. We can also make a flow chart that might help us write the first pseudocode. 
![[01 Computer engineering and architecture/sketches/flowchart for car fueling problem|center]]
Like when we deal with algorithms and other procedures we might start from the general flow to more specific tasks, such as when we have a business process and subprocesses underneath. Lets try to develop pseudocode for this procedure 

```
def car_fueling(distance, miles, stops):
	num_stops = 0
	
	if distance < miles:
		return num_stops
	
	if next_stop > miles:
		return -1
	best_stop = 0
	while distance > 0:
		# find the optimal stop
		for stop in stops:
			if stop <= miles:
				best_stop = stop
		
		num_stops += 1
		
		best_stop_index = stops.index(best_stop)
		stops = stops[best_stop_index:]
		stops = [stops-best_stop for stop in stops]
		distance = distance - best_stop
		
	return num_stops
```

To sum up greedy algorithms we have that 
1. **Greedy algorithms** build solutions incrementally, as illustrated by the **Largest Concatenate Problem** and the **Money Change Problem**.
2. The **fractional knapsack problem** demonstrates how to maximize value by selecting items based on their **value per unit weight**.
3. Proving the **correctness** of greedy strategies is essential, as local optimal choices do not always guarantee a global solution.