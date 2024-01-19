- undirected graphs w no cycles!!
	- connected grph w N nodes and N - 1 edges
### Terms
- depth = max level of any node in a tree
	- depth of specific node:
		- num of edges from root node to that node
- height = num of edges on longest path from root to leaf
	- depth of tree from root
- Full tree/ proper binary tree:
	- every node has 0 or 2 children
- complete tree
	- binary tree where every level is filled except for maybe last
	- last is filled from left to right
	- heap uses complete binary trees
- balanced tree
	- binary tree where diff btwn left and right subtrees isnt more than 1
	- maintains optimal search and insertion time
- multiway tree
	- tree where nodes can have more than 2 kids
```python
class TreeNode():
	def __init__(self, data=None, left=None, right=None):
		self.data = data
		self.left = left
		self.right = right
```
## Binary Search Trees

- binary tree-> each node has as most 2 kids
- for each node, all nodes to the left are less than or equal to it, and all nodes to the right are greater than it
- bc of this prop, lookups take O(log n) time on avg, if tree is well balanced
#### Pros/Cons
- Pros:
	- efficient search -> o(logn) on avg
		- unsorted LL O(1) insertion & deletion but O(n) search
		- sorted array search -> O(logN) but update can be O(n) in worst cases
	- flexible updates
	- ordered data storage
	- 
- Cons
	- more overhead & complexity
#### Time & Space complexity
- Best cases: Accessing/Searching: O(logN), Inserting: O(logN), Deleting: O(logN)
- Worst cases: Accessing/Searching: O(n), Inserting: O(n), Deleting: O(n)
- best/ worst cases differ by how well the tree is balanced. Balanced trees are more efficient than unbalanced trees
- Space: O(n)
	

#### Traversing binary trees
- 4 main methods: preorder, postorder, inorder, or level order (bfs/ breadth first search)
	- most tree probs can be solved using one of these methods, just have to figure out which traversal to use
- Tree for example:
	- ![[Pasted image 20230525112252.png]]
##### Preorder
```python
# root -> left -> right
# good for exploring roots b4 leaves, ex: copying a tree
def printPreorder(node:TreeNode):
	if (node == None):
		return
	print(node.data)
	printPreorder(node.left)
	printPreorder(node.right)
# ex tree traversal would be 1, 2, 4, 5, 3
```
##### Postorder
```python
# left -> right -> root
# good for exploring leaves b4 roots
def printPostorder(node:TreeNode):
	if (node == None):
		return
	printPostorder(node.left)
	printPostorder(node.right)
	print(node.data)
# ex tree traversal would be 4, 5, 2, 3, 1
```
##### Inorder
```python
# left -> root -> right
# good for converting BST into an array
def printInorder(node:TreeNode):
	if node == None:
		return
	printInorder(node.left)
	print(node.data)
	printInorder(node.right)
#ex tree traversal would be 4, 2, 5, 1, 3
```
##### BFS/Level Order
```python
from collections import deque
def printBFS(root:TreeNode):
	queue = deque()
	if (root == None):
		return
	queue.append(root)
	while queue:
		node = queue.popleft()
		print(node.data)
		if (node.left != None): queue.append(node.left)
		if (node.right != None): queue.append(node.right)
# ex tree traversal would be 1, 2, 3, 4, 5
```

#### Common Operations
##### Insertion
``` python
def insert(self, val):
	newnode = Node(val):
	if self.root is None:
		self.root = newnode
	else:
		curr = self.root
		parent = None
		while curr is not None:
			parent = curr:
			if val < curr.data:
				curr = curr.left
			else:
				curr = curr.right
		if value < parent.data:
			parent.left = newnode
		else:
			parent.right = newnode
```
##### Deletion
``` python
def findMin(node):
	node = node.right
	while(node != None and node.left != None):
		node = node.left
	return node
	
def deleteNode(root, val):
	#Base cAse
	if root is None:
		return root
	# node to be deleted in left subtree
	if root.val > val:
		root.left = deleteNode(root.left, val)
	# node to be deleted in right subtree
	elif root.right < val:
		root.right = deleteNode(root.right, val)
	else:
	#we have found node to be deleted
		#case 1, no children
		if root.left == None and root.right == None:
			return None
		#case 2 only 1 child
		if root.left == None:
			return root.right
		if root.right == None:
			return root.left
		# case 2, 2 kids
		else: # replace self with inorder successor, which will be the minimum node in our right subtree -> node with smallest value greater than current node 
			#find inorder successor of child
			successor = findMin(root)
			# copy inorder successor data to node
			root.val = successor.val
			# delete inorder successor
			root.right = deleteNode(root.right, successor)
	 return root
```
##### Searching in a BST
```python
def doesNodeExistInBST(bstRoot:TreeNode, searchValue:int):
	# if we've ran out of values to search through, return false
	if bstRoot == None:
		return False
	elif bstRoot.data == searchValue:
			return True
	else:
		#if the node we're at is smaller than the val we're looking for, traverse on the right side
		if bstRoot.data < searchValue:
			doesNodeExist(bstRoot.right, searchValue)
		else:
		# if the node we're at is bigger than what we're looking for, traverse left
			doesNodeExist(bstRoot.left, searchValue)
```
###### Height of BST
```python
# height is length of path from root to deepest node in the tree
def getBinaryTreeHeight(node:TreeNode):
	if node == None:
		return -1
	leftHeight = getBinaryTreeHeight(node.left)
	rightHeight = getBinaryTreeHeight(node.right)
	if leftHeight > rightHeight:
		return leftHeight + 1
	else:
		return rightHeight + 1
"""
pseudocode:
- if node doesnt exist, don't count it in total (subtract 1 by return -1)
- recursively get height of left kid
- recursively get height of right kid
- return taller kid's height + 1 to count this node's height
"""
```
###### Depth of BST
- what's the diff btwn depth and height of a bst?
	- depth of a node:
		- number of edges from node to tree's root node
		- root node will have depth of 0
	- depth of a tree:
		- tree doesnt have depth, individual nodes do

	- height of node:
		- number of edges on LONGEST path from node to a leaf
			- leaf node will have height of 0
	- height of tree:
		- number of edges on Longest path from root to leaf

##### Patterns
###### Binary Trees Iterative Traversal Approach
- Why?
	- usually recursive traversal is first approach but this can lead to big memory footprints
	- might be asked for iterative traversal bc of this
- How?
	- usually use a stack or a queue
	- Common pattern
		1. Determine if we want to use a stack or queue to store nodes we need to visit
			1. stacks are LIFO
			2. queues are FIFO
		2. while stack/queue isn't null, retrieve nodes from it
			1. when we pop a node to visit, also have to figure out how to push its child nodes
- Example:
	- Preorder traversal (root, left, right)
```python
# Usual recursive approach
def printPreorder(node : TreeNode):
	if node == None:
		return
	print(node.data)
	printPreorder(node.left)
	printPreorder(node.right)
```
- ![[Pasted image 20230525122254.png]]
	- considerations
		- Want to visit roots b4 leaves
		- want to visit left child b4 right
	- pattern:
		- create empty stack
		- push root
		- while stack isn't empty:
			- pop node from stack and print
			- push right child
			- push left child
```python
# iterative preorder traversal using stack
def preorderTraversal(root:TreeNode):
	stack = []
	stack.append(root)
	while stack:
		curr = stack.pop()
		print(curr.data)
		if curr.right:
			stack.append(curr.right)
		if curr.left:
			stack.append(curr.left)
```
- Time complexty: O(n)
	- we push/pop each node of tree
- Space Complexity: O(h), h is height of the tree

###### Approach Key Points
1. recall recursive way to solve problem
2. working from recursive solution, we know our desired output
3. using desired output try to create new approach which would give us same outcome
4. once we saw a pattern, able to come up with an algorithm


##### Finding 2nd Largest Node in a BST
```python
class TreeNode():
	def __init__(self, data=None, left=None, right=None):
		self.data = data
		self.left = left
		self.right = right
```
##### Method 1
- given BST - might want to do inorder traversal 
```python
# left, root, right
def printInorder(node:TreeNode):
	if node == None:
		return
	printInorder(node.left)
	print(node.data)
	printInorder(node.right)
```
- would allow to print every node in BST in ascending order, then store nodes in array and return 2nd to last element in array
- runtime: O(n) - have to look at each node
- space: O(n)

###### Method 2
- use main props of BST, 1) all els to the right are greater 2) all els to left are smaller
- rightmost element of a tree is the largest element
- how to find largest:
```python
def getLargest(node:TreeNode):
	if node.right != None:
		return getLargest(node.right)
	else:
		return node
```
- how to find 2nd largest?
	- if was balanced, could return parent of largest element
	- might not be balanced though!
		- if not balanced:
			- if rightmost element has a left child:
				- rightmost child of left child will be 2nd largest element
			- else:
				- parent of rightmost element will be 2nd largest element
```python
def get2ndLargest(node:TreeNode):
	# if we're at largest element (ie right most element) and
	# it has a left child
	# the 2nd largest will be the largest element in left child
	if node.right == None and node.left != None:
		return getLargest(node.left)
	# if we're at parent of largest element and the 
	# the largest element has no children, this is the node we want
	if node.right != None and node.right.left == None and node.right.right == None:
		return node
	# recurse on right kid until we match one of the above scenarios
	return get2ndLargest(node.right)
		
```