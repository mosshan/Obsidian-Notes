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