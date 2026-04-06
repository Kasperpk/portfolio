We've just begun the journey into computer science laying the theoretical and practical foundation which leads to applied computer science. There are interesting topics such as developing software and using computers for all sorts of practical problems including advanced analytics, aritificial intelligence and data science. In the next section we will dive into the computer science topics that lay the foundation for becoming a better programmer but here we will work on some fun projects where we can use our newfound knowledge of computing systems. 

The first problem we will look at is from the CSES problemset and is called *Ferris Wheel*. It's a problem with *n* children and each with a weight of their own and we need to find out the minimum number of gondolas needed for the children. An example input is the following, where the first intput is the number of children, the second input is the weight allowed in the gondolas and the third is the weight of each child. 
```
4 10
7 2 3 9
```
The greedy choice here is to keep summing the weights until it exceeds 10 and then when it does increment the number of gondolas needed and begin from the index of the last summed child until the end of the array is reached. The flowchart here is might explain how this algorithm will proceed. 
![[Flowchart of algorithm|center]]
The following sketch shows how this conceptually would look like. Here we can see that we need to somehow have a pointer on the current child that we can progress. We also need a current weight of the gondola that we can compare the weight with. 
![[Sketches/drawing of ferris wheel algorithm|center]]
To solve this exercise we have to think smart and one brilliant idea is to sort the child first and use two pointers to progress the program. This idea has been introduced in several problems that i have been solving and it's  perhaps best understood with a little visualization. Here we see three children and the two pointers start from each side of the sorted array. It then compares the sum of the weights to the maximum weight allowed, if the weight is to great then the child at the right pointer must ride alone since there is no combination where it could ride with anyone given that we have sorted the array. The right pointer is then decrement and the comparison again is above the maximum weight allowed so again we increment the gondolas and decrement right pointer. Now the right pointer has reached the left pointer and at this point we increment the gondolas and also break out of the code to return the final result. 

![](Two%20pointer%20approach.png)
