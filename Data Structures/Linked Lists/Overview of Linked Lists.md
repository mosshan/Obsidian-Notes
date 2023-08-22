#linkedlist 
## Overview of Linked Lists 
#### [Overview of Linked Lists](https://guides.codepath.org/compsci/Linked-Lists)

-   call stack as a linked list -> trail back from where program is back to beginning of process or thread
	-   allows computer to know what to do when current function working on exits
-   common varients - singly linked, doubly linked: each node has next and previous, circular
-   python def of Linked List node for singly linked list:

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

// list 1->2 where 1 is at the head of the list
head = ListNode(1)
head.next = ListNode(2)
```

### Pros and Cons of a Linked List
#### Pros
-   good when operations are confined to 1 end of data structure
-   good w small sizes
-   simple and efficient in above cases, small size, ops at one end
 #### Cons
	-   bad at random access
	-   bad for large
		-   have to have node object for each item I want to store

    
    -   Best Case occurs when node is at head of the list
    -   Worst case is when node is at end of the list
### Time and Space Complexity
 - Best Case: occurs when operating on the head of the list
	 - Accessing/Seaching: O(1)
	 - Inserting at Head: O(1)
	 - Deleting at Head: O(1)
 - Worst Case: occurs when operating at the end of the list
	 - N is num of elements in list
	 -  Accessing/Seaching: O(N)
	 - Inserting: O(N)
	 - Deleting: O(N)
### Terms
-   Sentinel - dummy node - usually put at head or end of list to aid operations or indicate end of the list

### Common Operations
#### Insert
```python
#Insert
def insert(self, val):
	#create node
	n = ListNode(val)
	#make n into new head of list
	n.next = self
	return n 
```
#### Delete
```python
def delete(self, val):
	#create pointer to head
	sentinel = ListNode("sentinel")
	sentinel.next = self
	#create 2 ptrs to move through list
	ptr1 = sentinel
	ptr2 = self
	#while not at end of list, nav until we find it
	while ptr2:
		if ptr2.val == val:
			ptr1.next == ptr2.next
			return sentinel.next
		ptr1 = ptr2
		ptr2 = ptr2.next
	# we didnt find the node to delete so just return the list without changes
	return sentinel.next
```

#### Length Of List
```python
#Length of List
def __len__(self):
	pointer = self
	length = 0
	while pointer:
		length += 1
		pointer = pointer.next
	return length
```

#linkedlist
## Solving Techniques
### Temp Head
- [Dummy Head](https://github.com/codepath/compsci_guides/wiki/Temp-Head)
#### why does this help?
- prevents u from needing special edge condition logic when operating on head of linked list
- for example when need to manipulate ptrs and create same list but with different ordering
#### how work?
- create one extra ptr, temp head
	- points to final answer or list you'll return
	
##### Delete Node
- given val of node to delete, delete node in LL
- vals are unique in LL
```python
class Node(object):
	def __init__(self, v):
		selv.val = v
		self.next = None
		
def delete_node(head, val):
	tempHead = Node("temp")
	tempHead.next = head
	ptr1 = tempHead
	ptr2 = head
	while ptr2:
		if ptr2.val = val
			ptr1.next = ptr2.next #don't need to treat deleting head any differently
			return tempHead.next
		ptr1 = ptr2
		ptr2 = ptr2.next
	return tempHead.next
			
```




### Two Pointer
-   [Linked List Two Pointer](https://guides.codepath.org/compsci/Linked-List-Two-Pointer)
#### why?/ how
- iterate through list w 2+ ptrs - in diff patterns ie ptr1 moves +1 & ptr2 moves +2
- diffs in how ptrs iterate can make list calculations more efficient

#### Example: Detect Cycle in LL 
Given a linked list, determine if it has a cycle in it. Can you do it with constant extra space?

##### Answer: Using extra storage time = O(N), space = O(N)
- cycle = list where we pt to same node twice
- use other data struct -> hash list (constant time insert + lookup) to store nodes already seen as traverse list
- then move through nodes and see if already stored
```python
class Node(object):
    def __init__(self, v):
        self.val = v
        self.next = None
        
    def insert(self, n):
        n.next = self
        return n

def has_cycle_with_aux(ll):
    aux = set()
    while ll:
        if ll in aux:
            return True
        aux.add(ll)
        ll = ll.next
    return False
```
##### Anser: two Pointers, time = O(N) space = O(a)
- get rid of aux data struct by using 1 addit ptr
- move through list at diff speeds
- if cycle, list is like circle at some pt - faster ptr will eventually cross paths w slower

```python
def has_cycle(11):
	if not ll or not ll.next:
		return False
	fp = ll.next
	sp = ll
	while fp and fp.next:
		if fp == sp or fp.next == sp: 
			return True
		fp = fp.next.next
		sp = sp.next
	return False
```
### Multiple Pass
-   [Multiple Pass](https://guides.codepath.org/compsci/Multiple-Pass)
#### why? + what
- Most list comps require O(N) time complexity
- Pass through list multiple times to get summary of list to aid algorithm

#### Example: Intersection of 2 LL
- > **Wr**ite a **pro**gram **t**o **fi**nd **t**he **no**de **a**t **wh**ich **t**he **inters**ection **o**f **t**wo **sin**gly **lin**ked **li**sts **beg**ins. **F**or **exam**ple, **t**he **foll**owing **t**wo **lin**ked **lis**ts:
> ![[160_statement.png]]
> **be**gin **t**o **inte**rsect **a**t **no**de **c**1.
> 
> **Not**es:
> 
> -   **I**f **t**he **t**wo **lin**ked **li**sts **ha**ve **n**o **inters**ection **a**t **al**l, **ret**urn **nu**ll.
> -   **T**he **lin**ked **li**sts **mu**st **ret**ain **th**eir **orig**inal **stru**cture **af**ter **t**he **func**tion **retu**rns.
> -   **Y**ou **m**ay **ass**ume **th**ere **a**re **n**o **cyc**les **anyw**here **i**n **t**he **ent**ire **lin**ked **struc**ture.
> -   **Yo**ur **co**de **sho**uld **prefe**rably **r**un **i**n O(n) time **a**nd **u**se **on**ly O(1) mem**ory.
- How to make this simpler?
	- 1. once a list has intersected, the rest of the list is identical
	- 2. can only be identical if same length
	- Ignore prefix of longer of 2 lists! - cant be part of intersection
	- Creates subtask: 
		- take 2 lists of any length and return 2 of same lenfth\
```python
class Node(object):
    def __init__(self, v):
        self.val = v
        self.next = None
	# returns string representation of object of the class
    def __repr__(self):
        return f"{self.val} --> {self.next}"

	#inserts at head
    def insert(self, v):
        n = Node(v)
        n.next = self
        return n
#recursive length
# has greater storage penalty than iterative - looping is done implicitly -> for each call of the function, (each move in while ll loop essentially), data is added to call stack
def get_len_recur(ll):
	# pt1. base case
    if not ll: return 0 # A None path has 0 length
    # pt2. given any node, how to calc length from that to end 
    # pt3. how to relate answer to final recursive computation - equal in this case!
    return get_len_recur(ll.next) + 1 # The length at this node is 1 + length of rest
    
#iterative length
#nav through whole link list counting items
def get_len(ll):
    l = 0
    while ll:
        l += 1
        ll = ll.next
    return l

def make_same_length(ll1, ll2):
    len1 = get_len(ll1)
    len2 = get_len(ll2)
    # find longer list and assign easy vars
    if len1 > len2:
        long_ll, short_ll = ll1, ll2
        long_len, short_len = len1, len2
    else:
        long_ll, short_ll = ll2, ll1
        long_len, short_len = len2, len1
    # take items off of longer list until lengths match
    while long_len > short_len:
        long_len -= 1
        long_ll = long_ll.next
    return short_ll, long_ll
    
# use example based on lists from earlier
common = Node('c1')
short = common.insert('a2').insert('a1')
long = common.insert('b3').insert('b2').insert('b1')
make_same_length(short, long)

#Output would be
#"(a1 --> a2 --> c1 --> None, b2 --> b3 --> c1 --> None)"
```
