#problems #linkedlist 
## Problem #1: Swap nodes in pairs
Original Problem on Leetcode: [Swap nodes in pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

**Example:**
![Image of example #1 linked lists](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg) Source: [LeetCode](https://leetcode.com/problems/swap-nodes-in-pairs/)

```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

#### Understand
-   Established a set (2-3) of test cases to verify their own solution later.
    - Input: 1-> 3-> 6->2
    - Output: 3->1->2->6 
    - Input: 4->2
    - Output: 2-> 4
-   Established a set (1-2) of edge cases to verify their solution handles complexities.
    - Input:1
    - Output: 1
    - Input: None
    - Output: None
    - Input: 1->3 ->2
    - Output: 3->1-> 2
-   Have fully understood the problem and have no clarifying questions.
    - Will there be empty sets?
    - What to do with odd number sets?
-   Have you verified any Time/Space Constraints for this problem?
#### Match 
- link list 
	- options: multiple pass, dummy head, 2 ptr iterating at diff speeds
	- want to use dummy head!
#### Plan
- if none, return head
- create dummy head to point to head of list
- create ptr 1 and 2 to point to head and head.next
- loop: check if ptr 2 points to anything
	- swap nodes
	- move ptr 1 and ptr 2 down 1 
- return dummy head .next
#### Implement

```python
class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head

        tempHead = ListNode("temp")
        tempHead.next = head

        currentNode = tempHead
        
        while currentNode and currentNode.next and currentNode.next.next:
            first = currentNode.next
            second = currentNode.next.next
            currentNode.next = second
            first.next = second.next
            second.next = first
            currentNode = first
        return tempHead.next
```

#### Review
- remember to return tempHead.next not tempHead!!!!

#### Evaluate
-   What is the **Space** complexity?
    - O(1)
-   What is the **Time** complexity?
    - O(n)
-   Could your solution have been made any more efficient?

## Problem #2: Rotate List
Original Problem on Leetcode: [Rotate List](https://leetcode.com/problems/rotate-list/description/

Given the `head` of a linked list, rotate the list to the right by `k` places.
**Example:**
![Image of example #1 rotated linked lists](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg) Source: [LeetCode](https://leetcode.com/problems/rotate-list/)
```
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```
#### Understand
-   Established a set (2-3) of test cases to verify their own solution later.
    - Input: 1->2->3 k = 1
    - Output: 2->3->1
-   Established a set (1-2) of edge cases to verify their solution handles complexities.
    - Input: none, k = 1
    - Output: none
    - Input: 1->2 -> 3 , k = 3
    - Output: 1->2 -> 3
-   Have fully understood the problem and have no clarifying questions.
    - Make sure that last ptr is null
    - if k is larger than the list length -> rotate by int(k % n)
    - k will be non negative
-   Have you verified any Time/Space Constraints for this problem?

#### Match
- linkedlist
- could use dummy head and multiple pass?

#### Plan
- if none or 1 item or if  int(k %  list length) == 0 , return list
- make list circular
	- ptr = head
	- for loop to navigate to end of list - movinng list length - 1 times
		- ptr = ptr.next
		- make it pt to head
- calculate actual number of rotations , r = int(k %  list length)
- loop for length of list - r away from head
	- head = head.next
- make un circular
	- for loop to navigate to end of list - movinng list length - 1 times
		- ptr = ptr.next
		- make it pt to null
#### Implement
```python
class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not head or k == 0:
            return head
        
        listLen = 1
        end = head
        while end.next:
            listLen += 1
            end = end.next

        end.next = head
        r = int(k % listLen)

        for i in range(listLen - r):
            head = head.next
            end = end.next
        
        end.next = None
        return head
```
#### Review
- missed issue which created cycles - by creating early if statement which prevented reaching end.next = none
#### Evaluate
-   What is the **Space** complexity?
    O(n)
-   What is the **Time** complexity?
    O(1)
-   Could your solution have been made any more efficient?

## Remove Nth Node From End of List
Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

**Input:** head = 1,2,3,4,5, n = 2
**Output:** 1,2,3,5

#### Understand
- test cases: 
	-1, 2, 3, 4, n = 4
	output: 1, 2, 3
- Edge cases
	-Input: 1 , n = 1
	Output: 
- clarifying qs
	- can n be greater than length of list? no
	- Nth from END
#### Match
- dummy head

#### Plan
- if head.next does not exist, return none
- use dummy head to keep track of head
- find length of list
- find node to remove by moving lengh - n times from dummy head
	- node to remove will be at .next
- reconnect

#### Implement
```python
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        length = 1
        ptr = head
        while ptr.next:
            length += 1
            ptr = ptr.next

        tempHead = ListNode("temp")
        tempHead.next = head

        ptr = tempHead
        for i in range(length - n):
            ptr = ptr.next
        
        ptr.next = ptr.next.next
        return tempHead.next
```

#### Review
- 2 issues
	- wasnt traversing from dummy head originally - caused issues when needed to remove head

## Merge Two Sorted Lists

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists in a one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return _the head of the merged linked list_.

Example: 
**Input:** list1 = [1,2,4], list2 = [1,3,4]
**Output:** [1,1,2,3,4,4]
![[merge_ex1.jpg]]


#### Understand
- happy cases
	- input: 1-> 2 -> 3, 2-> 5-> 6
	- output: 1-> 2 -> 2-> 3 -> 5 -> 6
	- input: 1-> 2, -1-> 2-> 3
	- output: -1 -> 2-> 2-> 3
- edge cases
	- input: , 2-> 3
	- output: 2-> 3
- clarifying Qs
	- resulting list needs to be sorted
	- are initial lists sorted? yes, in nondecreasing order
	- Can one be empty? yes
	- values can be negative

#### Match
- Linked List 
	- options: two pointers x, dummy head yes, multiple traversals unneeded

#### Plan
- if either list doesnt exist, return other list
- create dummy head
- end = tempHead 
- while both lists have elements :
	- if both have values find smaller value
		- attach to end.next
		- end = end.next
		- move that list's head to next value
- if only one has elements:
	- attach whole rest of list to end.next
- return tempHead.next

#### Implement:
```python
def mergeTwoLists(self, list1, list2):
        """
        :type list1: Optional[ListNode]
        :type list2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        if not list1:
            return list2
        if not list2:
            return list1

        tempHead = ListNode("temp")
        end = tempHead

        while list1 or list2:
            if list1 and list2: 
                if list1.val < list2.val:
                    end.next = list1
                    list1 = list1.next
                else:
                    end.next = list2
                    list2 = list2.next
            elif list1:
                end.next = list1
                return tempHead.next
            else:
                end.next = list2
                return tempHead.next
            end = end.next
        return tempHead.next
```
#### Review
- ran through test cases and looked for bugs - none found
- was accepted on leetcode

#### Evaluation
- space: 
	- O(1)
- time:
	- O(n)
- improvements: 
	- could clean up if else statements 


## Find the Duplicate Number
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return _this repeated number_.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

**Example 1:**
**Input:** nums = \[1,3,4,2,2]
**Output:** 2

**Example 2:**
**Input:** nums = \[3,1,3,4,2]
**Output:** 3

#### Understand
- happy cases
- edge cases
	- Input: 2 2 2 2
	- Output: 2
- clarification
	- not all nums between 1 to n must be in array
	- constant extra space and cant mod array
		- cant sort or use hash set
	- repeated num can be repeated multiple times
#### Match
- linked list
	- Cycle!! use fast and slow pointer

#### Plan
##### General understanding
length = n + 1
nums \[i] in \[i, n]
	- view array as telling graph connections
	- ![[Pasted image 20230511130648.png]]
	- but 0 is 1 in graph drawing
	- index = graph element
	- array value = connected element
	- start both fp and sp at nums\[0]
		- i = 1, n = 3 means graph element 1 -> 3
		- i = 2, n = 4 means graph element 2 -> 4
		-
		- sp moves - sp = Array\[sp]
		- fp moves - fp = Array\[Array\[fp]]
	- 
	- Array\[1] = 3 --> move to index 3
##### Breakdown of solution process
- knowns
	- there will be a cycle
	- there will be a portion before the cycle bc we only have one number that can be duplicated
		- that number is the start of the cycle
	- want to identify beginning of cycle bc we knpw that that is the num which is the dup
- how to identify beginning of cycle?
	- [[Floyd's Algorithm]]
	- 
- 

## Reverse Linked List
Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

**Input:** head = \[1,2,3,4,5]
**Output:** \[5,4,3,2,1]

```python
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        curr = head
        prev = None
        next = head.next
        while next:
            curr.next = prev
            prev = curr
            curr = next
            next = curr.next
        curr.next = prev
        return curr
```

## Reverse Nodes in k- Group
https://leetcode.com/problems/reverse-nodes-in-k-group/
Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.
**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = \[1,2,3,4,5], k = 2
**Output:** \[2,1,4,3,5]

#### Understand
- happy path
	-  input: 7 -> 2 -> 4, k = 2
	- output: 2-> 7 -> 4
- edge cases
	- Input: 1 -> 2 -> 3 , k = 1
	- Output: 1-> 2 -> 3
- clarifying qs
	- k = pos int, less than or equal to length of linked list
	- if num of nodes isnt multiple of k, leave left out nodes at end of list alone
	- cant alter vals of nodes
	- are nodes sorted?
		- no
	- if k = 1, is list returned without changes? 
		- yes
	- can list be empty?
		- no, k <= 1 and length of list is <= k
#### Match
- Linked list prob
	- options: multiple traversal , sp and fp , temp head
	- use temp head
#### Plan
- pg = temp head
- current node = head
- find kth from pg
	- if kth exists:
		- kth.next = ng
		- reverse group
			- p = pg
			- c = pg.next
			- while c != ng
				- reverse
		- 



