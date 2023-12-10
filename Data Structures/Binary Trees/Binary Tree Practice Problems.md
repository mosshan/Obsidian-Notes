#binarytree #problems
## Invert Binary Tree
https://leetcode.com/problems/invert-binary-tree/
Given the root of a binary tree, invert the tree and return its root
#### Understand
- what order is binary tree given in and must be returned in?
	- root, left, right (bfs/level order)
- how to invert?
	- left and right children are swapped at each level
- can binary tree be empty or just have one node?
	- yes to both
- is the binary tree balanced?
	- doesnt matter for inversion as we are inverting per level
- is it a bst?
	- no
- edge:
	- empty tree: input:  root = \[] output: root = \[]
	- tree w one child on last level: input: root = \[1, 2] output: root= \[1, 2]
#### Match
- binary tree type problem
	- no specific pattern needed to help
#### Plan
- if root doesnt exist or root has no children
	- return root
- else:
	- temp = left 
	- left child = invert right
	- right child = invert temp
- return root
#### Implement
```python
class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root or (not root.left and not root.right):
            return root
		temp = root.left
		root.left = self.invertTree(root.right)
		root.right = self.invertTree(temp)
        return root

## other option
def invertTree(root):

	if not root:
		return None
		
	temp = root.left
	root.left = invertTree(root.right)
	root.right = invertTree(temp)
	
	return root
```
#### Review
- either way works!
- make sure to check that pseudocode = actual code you write
#### Evaluate
- space: O(h), h = height of tree (no auxiliary data structures but because of the recursive calls, O(h), we have up to h calls on stack at once, or O(log n) bc height = logn
- runtime: O(n)

## Symmetric Tree
https://leetcode.com/problems/symmetric-tree
Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).
#### Understand
- root can be empty or have 1 element:
	- return true
#### Plan
- plan1:
	- if split tree into 2, lc and rc
		- lc should = rc inverted vertically
	- could invert by layer/iteratively? - would have to modify current situation
		- invert recursive
			- if root is none or root doesnt have kids
				- return root
			-  temp = left kid
			- left kid = invert (right kid)
			- right kid = invert (left kid)
			- return root
		- check if trees are same
- plan2:
	- recursive checking for symmetry:
		- if neither exist
			- return true
		- if both exist and both have same values:
					- continue recursion 
						- return check if left.left = right.right and left.right = right.left
		- return false -> either only 1 exists or they don't have the same values
	helper function to call recursive check
	- return root does not exist or (recursively check if (left and right are symmetric)
	- BETTER
#### Implementation
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root is None:
            return True

        leftTree = root.left
        rightTree = self.invertTree(root.right)

        return self.checkIfSame(leftTree, rightTree)

    def checkIfSame(self, lr, rr):
        # if neither exist, return true
        if (not lr and not rr):
            return True
        # if they both exist, compare them and then check if their children are the same
        elif lr and rr:
            if lr.val != rr.val:
                return False
            else:
                return self.checkIfSame(lr.left,rr.left) and self.checkIfSame(lr.right, rr.right)
        # only one exists, so they arent same
        return False
        

    def invertTree(self, node):
        if node is None or (not node.left and not node.right):
            return node

        temp = node.left
        node.left = self.invertTree(node.right)
        node.right = self.invertTree(temp)

        return node

# plan 2
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return (not root) or self.recursiveSymmCheck(root.left, root.right)

    def recursiveSymmCheck(self, lr, rr):
        if not lr and not rr:
            return True
        elif (lr and rr) and (lr.val == rr.val):
            return self.recursiveSymmCheck(lr.left, rr.right) and self.recursiveSymmCheck(lr.right, rr.left)
        return False
```
#### Review
- Plan 1, overcomplicated
	- verify logic of dismissing easier plan before moving to harder
- both plans had similar runtime/space needs but plan 2 was much simpler
#### Evaluate
Plan1
- space: O(h) + O(h)
- runtime: O(n / 2) + O(n)
Plan 2
- space: O(h)
- runtime: O(n)

## Balanced Binary Tree
https://leetcode.com/problems/balanced-binary-tree/
determine if a tree is height balanced
- depth of the two subtrees of every node never differs by more than one.
- find height of left and right subtree 
	- if balanced
	- traverse left and right and check if the subtrees of both are balanced
- find if whole tree is balanced
```
if root == None:
	return -1
lHeight = isBalanced(self, root.left) + 1
rHeight = isBalanced(self, root.right) + 1
return (abs(lHeight - rHeight) < 2)
```
- need to do this for each subtree
	- This approach if checking for each node would be O(n^2)
- Instead, ask this question starting from bottom up
	- using a helper function
		- if root = None:
			- we are balanced and have a height of 0
			- return true, 0
		- call helper on left and right
		- we're balanced at this node if the diff of heights of left and right are < 2 AND both our left and right subtrees are balanced
		- and our height is the max height of our left/ right subtrees + 1
		- then return a tuple of both of those values, (balanced, height)
	- call helper on our root, and check if it returns balanced
```
class Solution(object):
    def isBalanced(self, root):
		def dfs(root):
			# return bool and height of tree
			if not root:
				return [True, 0]
			# find height and balance of left + right subtrees
			left, right = dfs(root.left), dfs(root.right)
			# check if root is balanced, and left + right subtrees
			balanced = (abs(left[1] - right[1]) < 2) and left[0] and right[0]
			height = 1 + max(left[1], right[1])
			
			return [balanced, height]
	        
	return dfs(root)[0]
```
- Final code is O(n) runtime with space complexity of O(n) for stacks

## Maximum Depth of Binary Tree
https://leetcode.com/problems/maximum-depth-of-binary-tree/
- max depth is num of nodes along longest path from root to leaf
- check each path while keeping running max? - iterative
	- traversals of trees
		- preorder
		- postorder
		- inorder
		- bfs
- go to simplest case/ simplest tree
	- check which child has bigger depth
		- return bigger depth
- recursively, similar to finding height for tree
- base case:
	- if root is none:
		- return 0
- recursive calls:
	- leftDepth = function(root.left) + 1
	- rightDepth = function(root.right) + 1
- case 1:
	- if leftDepth > rightDepth
		- return leftDepth
- case 2
	- return rightDepth
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root == None:
            return 0
            
        leftDepth = self.maxDepth(root.left) + 1
        rightDepth = self.maxDepth(root.right) + 1
        
        if leftDepth > rightDepth:
            return leftDepth

        return rightDepth
```
Runtime: 
	n  = num of nodes 
	O(n)
Space Complexity:
	O(n)

## Diameter of Binary Tree
https://leetcode.com/problems/diameter-of-binary-tree/
Given the root of a binary tree, return the length of the DIAMETER of the tree
- what is the diameter?
	- the length of the longest path btwn any 2 nodes in a tree - can pass through the root
	- length of a path btwn 2 nodes = num of edges btwn them
		- ie node1 is the root, node2 is left child of the root, then length of path btwn the two is 1 for 1 edge
- Thought1:
	- left most child to right most child is longest path?
		- verify on examples:
			- nope, not always the case..
- Thought2:
	- longest path goes from 2 nodes with largest max depth from last common node (perhaps not root)
	- Is it always including leaf node which has largest max depth?
		- yes
	- Thought3:
		- find node with largest max depth first
		- check from each node up from it, 
			- NOO
- Brute Force: O(n^2)
	- take every node, use it as "top most node"/common/conjoining node in diameter
		- go as far down right as possible
			- (find lowest node on right side)
		- go as far down left as possible/ find lowest node on left side
- If left path is shorter than child's left path, we arent the top most node
- Thought4: 
	- Think of it in subproblems, find max diameter of subtree
	- START from bottom
		- find diameter and height of each node
		- diameter = leftheight + rightheight + 2 (for 2 added edges)
		- height of null node = -1 
		- height of node with no children = 0
		- height = 1 + max(leftHeight, rightHeight)
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        maxDiam = [0]
        def dfs(root):
            if root == None:
                return -1
            leftH = dfs(root.left)
            rightH = dfs(root.right)
            maxDiam[0] = max((leftH + rightH + 2), maxDiam[0])
            return 1 + max(leftH, rightH)
        dfs(root)
        return maxDiam[0]
```
Runtime & Space Complexity: O(n)

  *Need to Revisit*
  