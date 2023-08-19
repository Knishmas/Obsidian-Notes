
**Source**: https://www.geeksforgeeks.org/printing-pre-and-post-visited-times-in-dfs-of-a-graph/#

# Context 
- DFS goes through all connected nodes within a graph and marks them as visited. 
- We can also make additional use of DFS by storing extra information. 
	- *Example*: The visiting order of nodes while running a DFS. 

# Pre and post DFS 
* Pre-visit and Post-visit numbers is extra information that can be stored and utilized. 
* **Pre-visit**: Tells us when the node is stored on the recursion stack 
* **Post-visit:** Tells us when the node pops out of the DFS recursion stack. 

