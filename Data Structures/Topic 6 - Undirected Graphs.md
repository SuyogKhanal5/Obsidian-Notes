- ### Graph Terminology
	- **Graph** - Set of vertices connected pairwise by edges
	- **Path** - Sequence of vertices connected by edges
	- **Connected** - Two vertices are connected if there is a path between them
	- **Cycle** - Path whose first and last vertices are the same ![[Pasted image 20231007190200.png]]
	- ### Graph Sample Class
		- Graph drawing provides intuition about structure of graph![[Pasted image 20231007190227.png]]![[Pasted image 20231007190234.png]]![[Pasted image 20231007190307.png]]
		- Adjacency Matrix Representation![[Pasted image 20231007190329.png]]
		- Adjacency List graph representation![[Pasted image 20231007190346.png]]
		- In practice use adjacency list to represent graphs
		- Adjacency List Graph Representation Java Implementation![[Pasted image 20231007190425.png]]
		- Edges have costs associated with them![[Pasted image 20231007190440.png]]![[Pasted image 20231007190445.png]]![[Pasted image 20231007190452.png]]
		- Max number of edges on a graph of $v$ vertices is $\frac{v(v-1)}{2}$

- ### Depth First Search
	- Keep going from children to children until there are no more children to traverse, then go back and visit the children you missed
	- Traverse through left subtrees (or just through the graph) until no longer possible, then traverse the right subtrees ![[Pasted image 20231007190810.png]]
- ### Breadth First Search
	- Go to all of a nodes children until there are no children left, then visit those children's children
	- Search layer by layer outwards or into subtrees ![[Pasted image 20231007190904.png]]