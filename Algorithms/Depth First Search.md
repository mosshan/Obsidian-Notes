- explore edges and nodes of a graph
- Time complexity - O(V + E)
- Depth first!!
	- starting on chosen node
	- goes as **deep** as possible until cannot go any further (either leaf or only options are already visited)
		- backtracks until hit a node which is not a leaf and has options which we have not already visited
		- continue
``` python 
#pseudo code
# global or class scope vars
n = number of nodes in the graph
g = adjacency list representing graph
visited = [False, ...., False] #size n

function dfs(at):
	# recursive base case
	# if we've already visited we have no business here so should return
	if visited[at]: 
		return
	# mark self as visited
	visited[at] = true

	# explore all neighbors
	neighbors = graph[at]
	for next in neighbors:
		dfs(next)
# start dfs at node 0
start_node = 0
dfs(start_node)
```

### Use Cases:
#### Connected Components
- find how many components there are!
	- if we've run dfs but havent visited all nodes, all nodes are not connected
	- how many tmes we need to run dfs is how many connected components there are
- Algorithm:
	- label all nodes from (0, n)
	- start DFS at every node (except if its already been visited & mark all reachable nodes as being part of the same component