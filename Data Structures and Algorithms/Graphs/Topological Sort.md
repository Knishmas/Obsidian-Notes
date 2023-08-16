
![[Pasted image 20230816144425.png|400]] 

# **What is it?**
- A way to arrange things that have dependencies in a specific order such that the order allows for a task to not depend on another that has yet to be completed. 
- It's like creating a step-by-step plan where each step only depends on the ones that should come before it.

# Why use top sort? 
- Many real life situations can be modeled as directed graphs with edges which require some events to occur before others.  

	*Examples*
	- Class prerequisites 
	- Program dependencies 
	- Assembly instructions 
	# Deep dive: Class prerequisites
	**Scenario:** You're a student at a university and you'd like to take class H. In order to take class H you must take classes A,B,D,E,H first because they are prerequisites.
	
	![[Pasted image 20230816150729.png|400]]   

# Important Notes 
- Topological orderings are NOT unique. There can be multiple valid orderings. 
- Not all directed graphs have a topological ordering. 
	*Example* 
	- **Directed Cyclical Graphs**:  contain a cycle, thus it can't have valid orderings. ****
     ![[Pasted image 20230816153020.png||300]]
      (*Why?** There's no where to start. Every node in the cycle depends on another. 
      - The ONLY graphs with valid topological orderings are **Directed Acyclical Graphs**, directed graphs with NO cycles. 

- **Every tree has a topological ordering,** because by definition they do not have cycles.
	*How to get a trees topological ordering*  
	- An EASY way is to iteratively pick off the leaf nodes until there are no nodes left. 
	 ![[Pasted image 20230816154205.png|| 300]]    
	 ![[Pasted image 20230816154321.png||300]]

# General top sort guide for directed acyclical graphs 
	1. Choose an unvisited node
	2. Starting with that node, perform a DFS exploring only unvisited nodes 
	3. On the recursive callback of the DFS, add the current node to the
	topological ordering in reverse order

**Snapshot Example of Acyclical graph topological sort**
	![[Pasted image 20230816160410.png||400]] 
	**Practice Challenge:** continue the topological sort and get a complete valid ordering for the graph above. 

# Top sort Pseudo Code 

	![[Pasted image 20230816163309.png||400]] 
	![[Pasted image 20230816163339.png || 400]]