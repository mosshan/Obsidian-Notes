#binarytree 
## Intro
#### What is a binary tree?
	- trees where each element/ node has at most 2 children
	- composed of nodes 
		- usually hold following props:
			- data element (usually an int but can be anything)
			- left pointer 
			- right pointer
```python
class TreeNode():
	def __init__(self, data=None, left=None, right=None):
		self.data = data
		self.left = left
		self.right = right
```

- common prob: search for smthn in given list
- ex:
	- given nums of lottery draw, (1, 2, 5, 10, 16, 20, 23, 36, 40, 41, 45), is number 18 a winning number?
	- if didn't know nums was sorted, would have to look through each num
	- 
	- if we know nums is sorted, stop once we reach number bgger than one we're looking for
		- how to be efficient abt this?
			- start in middle of list
			- move left or right depending on if num looking for is smaller or bigger than one we're currently comparing to
			- ex: (1, 2, 5, 10, 16, 20, 23, 36, 40, 41, 45), looking for number 18
				- 20 is middle of list
				- compare 18 and 20
				- 18 < 20 so compare 18 and 5 -- since 5 is middle of list (1, 2, 5, 10, 16)
				- 18> 5 so move to right side of remaining list, (10,16)
				- continue until no more nums to compare to
		- Efficient version is often put in the form of BSTs, Binary Search Trees
#### BST or Binary Search Tree
- for each node, all nodes to the left are less than or equal to it, and all nodes to the right are greater than it
- bc of this prop, lookups take O(log n) time on avg, if tree is well balanced


## Pros and Cons
- BSTs are best options when tyring to optimize for efficient searching and flexible updates.
	- unsorted linked lists have O(1) insertion and deletion ops but require O(n) for search ops
	- if an array is sorted, search can be O(logn) but updating array by adding/deleting els can be O(N) in worst cases
- BSTs have more overhead and complexity to initialize and maintain
	- arrays and linked lists are more straight forward due to 1D structure
	- trees require more thought due to multidimensional structure
## Time and Space Complexity
- Best cases: Accessing/Searching: O(logN), Inserting: O(logN), Deleting: O(logN)
- Worst cases: Accessing/Searching: O(n), Inserting: O(n), Deleting: O(n)
- best/ worst cases differ by how well the tree is balanced. Balanced trees are more efficient than unbalanced trees
	- ![[Pasted image 20230525110224.png]]
## Terms
- Leaf - node with no left or right children
- Full Binary Tree - every node has either 0 or 2 children
- Balanced binary tree - the depth diff btwn 2 leaves is at most 1
- Order of node or tree - the number of children it has
- Height of a node - num of edges on the longest path from the ndoe to a leaf
## Traversing binary trees
- 4 main methods: preorder, postorder, inorder, or level order (bfs/ breadth first search)
	- most tree probs can be solved using one of these methods, just have to figure out which traversal to use
- Tree for example:
	- ![[Pasted image 20230525112252.png]]
#### Preorder
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
#### Postorder
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
#### Inorder
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
#### BFS/ Level Order 
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

## Common Operations
#### Searching in a BST
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
#### Height of BST
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
#### Depth of BST
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

## Patterns
#### Binary Trees Iterative Traversal Approach
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

##### Approach Key Points
1. recall recursive way to solve problem
2. working from recursive solution, we know our desired output
3. using desired output try to create new approach which would give us same outcome
4. once we saw a pattern, able to come up with an algorithm


#### Finding 2nd Largest Node in a BST
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

##### Method 2
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