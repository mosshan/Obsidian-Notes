
## Representation of Graphs
#### Adjacency Matrix
- 2d array m where m\[\i]\[j] reps edge weight of going from node i to node j
- from i to itself? -> 0
- Pros
	- space efficient for dense graphs
	- simplest representation
	- edge weight lookup is O(1)
- cons
	- space req -> requires O(v^2) space ( v= vertices)
	- iterating over all edges takes O(v^2)
		- imagine if graph was sparse!
#### Adjacency list
- graph as a map from nodes to lists of edges
	- A -> \[(B,4), (C, 1)] -> storing edge and weight
- Pros
	- space efficient for sparse graphs
		- only tracks what u have
	- iterating over all edges is efficient
- Cons
	- less space efficient for denser
	- Edge weight lookup is O(V)
		- if our vertice is connected to all other vertices, might have to look through list of V neighbors to find edge we're looking for
	- more complex
#### Edge List
- rep as unordered list of edges. 
	- ie triplets (u,v,w) "the cost from node u to node v is w"
	- \[(c, a, 4)]
- not often used due to lack of structure
- Pros
	- space efficient for sparce
	- iterating over all edges is efficient
	- simple structure
- Cons
	- less space efficient for denser
	- edge weight lookup is O(E)
## Types of Graphs
#### Undirected
- edges have no orientation 
- edge (u,v) is same as edge (v,u)
#### Directed (Digraphs)
- edges have orientation
- edge (u,v) is edge from node u to node v
#### Weighted Graphs
- edges can have weights
- (u,v,w)




#### Directed Acyclic Graphs (DAGs)
- directed graphs w no cycles
- rep structures w dependencies
- like class prereqs
	- need to take class a and b before you can take class c
#### Bipartite
- vertices can be split into 2 groups, U and V such that each edge connects btwn groups U and V 
- 2 colourable
#### Complete
- unique edge btwn every pair of nodes
- n vertices -> denoted as K sub n


## Depth First Search
