The exact definition of trees is  

It can be an efficient data structure for example to store ones directory of files on the hard drive. In general trees are useful for many purposes be it computer science or just to model many real world concepts, 
* such as organizational hierarchies, 
* the animal kingdom or 
* family hiearchies. 

![](syntax%20tree.jpg)

Compilers for example use tree like structures to evaluate syntax of code such as the while loop here or the expression seen below that. 
![](Abstract%20syntax%20tree.png)

![](abstract%20syntax%20tree%20expression.jpg)
This tree shows a subset of the hiearchy of the animal kingdom.
![](Tree%20hiearchy.jpg)
**Binary search trees** are also heavily used in computer science. In binary trees a node maximum have two childs and in this case the alphabetic order of the names are splitting this tree. So Cathy is "less" than Les and Sam is "greater than". 

![](Binary%20search%20tree.png)
We can quite easily search for keys like "Tony" because we can do four comparisons. 

**Tree traversal**
It's typical that we are interested in traversing the tree in some order. There are two main ways
* Depth-first: Completely traverse on sub-tree before exploring siblings sub-trees
* Breadth-first: Traverse all nodes at one level before progression to the next. 
How we want to traverse it depends on the applicaton. For an abstract syntax tree that shows for example arithmetic expressions we want to make sure we explore the subtree and do depth-first search in post-order fashion. 

