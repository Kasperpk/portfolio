> A *binary search tree* (BST) is a binary tree where each node has a Comparable key (and an assoicated value) and satisfies the restriction that the key in any node is larger than the keys in all nodes in that node's left subtree and smaller than the keys in all the nodes in that node's right subtree. 

The binary search tree is applicable to many problems and applications. There is one property that needs to be ensured if we are going to keep the running time of operations at O(log(n)), because a binary search tree by itself can have worst case running times of O(n) on operations like insertions and deletions and then we might as well pick any other data structure. 

**Balanced search trees and the AVL property**

![[unbalanced tree]]
The **AVL property** is one that ensures that the tree is balanaced sufficiently such that the height is O(log(n)). Height is the measure of balance in this case and for AVL to hold |N.left.height - N.right.height <= 1 |. 


**The AVL problem insertions**
To implement the AVL we need to extend our set of operations somewhat. We need to rebalance the tree once we insert and delete if it has caused the property to not hold any longer. We do that by rotating the nodes. 
![](Rotating%20tree%20left%20to%20keep%20AVL%20property.png)
Here is the pseudocode for the *RebalanceRight* operation. We first let M be the left node of N node. Then if the height of it's right subtree is greater than the height of the left subtree, we rotate left. Wether not we need did, we also rotate left on the node N. Finally we may adjust the heights. 


![](Rebalanceright%20pseudocode.png)
**The AVL problem deletions**
When we delete a node, we can cause the tree to be unbalanced and therefore we need to handle that. Here is the pseudocode for the deletions that maintain the AVL property. 

![](AVL%20delete.png)

These operations can be performed in O(log(n)) time which means we have a fully functioning binary search tree. 


**Split and merge operations**
There are other useful operations to perform on binary search trees. 
* Merge: Combines two BST into one
* Split: Breaks one BST into two

Merging 
One way to merge is to find the largest leaf of the left tree we want to merge on, and then call the merge with root operation. 
![](Find%20T%20root.png)
![](Pseudocode%20Merge.png)
Unfortunately this does not ensure that the tree is balanced. To ensure balance we 

![](Pseudocode%20AVL%20tree%20merges.png)
The **split** operation is the opposite of merge. It takes a single BTS and split it into two seperate ones like seen below. One tree has all elements lower than some node X. 
![](Splitting%20trees.png)
What we do is search for the X in the tree and merge the subtrees that are smaller than that and the substrees that are greater than it. 

![](search%20for%20x.png)
We are going to use recursion. 

![](Split%20pseudocode.png)