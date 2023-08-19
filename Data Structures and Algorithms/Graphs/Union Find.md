Source: https://www.youtube.com/watch?v=ayW5B2W9hfo&ab_channel=PotatoCoders
# What is it? 
- A data structure that helps keep track of different groups of items
- Also allows to quickly merge two groups into one and determine which group of a specific item belongs 

# Operations
 - **Union(x , y)** - Unifies the groups containing x. 
	 *Example*
	 ![[Pasted image 20230818172226.png ||600]]
- **Find(x)** - Find the group x belongs to.

# Implementation
- Turn each group into a graph by connecting all the objects within a group with an edge
- To distinguish groups, we need a representative from each grouping. 
	*Example* 
	 - 0 and 5 are the **representatives** for their group
	 - If we call **find(x)** , x being any of the elements within either group, it will **return the representative** of whatever grouping the element resides. 
	 - find(4) = 0, find(1) = 0, find(0) = 0, find(2) = 5
	![[Pasted image 20230818174109.png||400]]

# Tree Interpretation
We can re-arrange the graph as a tree with the representative being the root node. 
![[Pasted image 20230818174937.png|| 500]] 
## Find 
- **Parents and children** for any given element we find the representative by traveling upwards towards the root. 
	**Example**
	- **find(4) = 0 by the process**:  Parent(4) = 3 ----> Parent(3) = 0       ----> Parent(0) = 9
- We keep doing this and we know when to stop because the parent of a root is itself. 
- If we can keep track of the parent of every object then we can travel up the tree towards the root
## Union 
- If we want to find the union two trees we can set the root of one tree to be the child of the other. 
	**Example** 
	- Union(1,2) -----> Parent(find(2)) = find(1)
	- The root 5 is given the parent of the other tree with root 0
	![[Pasted image 20230818184159.png]]

#  Complexity
For both find and union
- **Time complexity:** O(log N)
- **Space complexity:** O(N)