
## User Defined

	- linked list
		- added to github
		- need section
	- graph
		- need on github + need section
	- trees
	- heaps
	
	
- hashtable vs hashset vs hashmap vs dictionary
#### Trees
```python
class TreeNode():
	def __init__(self, data=None, left=None, right=None):
		self.data = data
		self.left = left
		self.right = right
```
##### Binary Search Trees
- for each node, all nodes to the left are less than or equal to it, and all nodes to the right are greater than it
- bc of this prop, lookups take O(log n) time on avg, if tree is well balanced
Pros/Cons
- Pros:
	- efficient search
		- unsorted LL O(1) insertion & deletion but O(n) search
		- sorted array search -> O(logN) but update can be O(n) in worst cases
	- flexible updates
- Cons
	- more overhead & complexity
Time & Space complexity
- Best cases: Accessing/Searching: O(logN), Inserting: O(logN), Deleting: O(logN)
- Worst cases: Accessing/Searching: O(n), Inserting: O(n), Deleting: O(n)
- best/ worst cases differ by how well the tree is balanced. Balanced trees are more efficient than unbalanced trees
	- ![[Pasted image 20230525110224.png]]
Terms:
	
###### Traversing binary trees
- 4 main methods: preorder, postorder, inorder, or level order (bfs/ breadth first search)
	- most tree probs can be solved using one of these methods, just have to figure out which traversal to use
- Tree for example:
	- ![[Pasted image 20230525112252.png]]
###### Preorder
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
Postorder
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
Inorder
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
BFS/Level Order
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

#### Queue -> use collections.deque
- FIFO (like a line lol)
##### Option 1: Implement with a list
- Pros/Cons
	- Pros
		- simple
	- Cons
		- slow!!!! - insert/delete at beginning means shifting all other elements by 1 so O(n) gross
```
queue = []
queue.append('a')
queue.append('b')

print(queue.pop(0)) # must choose index to pop at, bc pop automatically does last
# Output -> a
```

##### Option 2: Implement with collections.deque
- Pros/Cons
	- pros
		- Quicker pop at beginning -> O(1)
		- No issue with resizing causing possible O(n) append like list
	- cons
		- if want to access by index / in the middle -> O(n)
``` python
from collections import deque

queue = deque(['name, 'age', 'DOB]) 

queue.append("append_from_right") # append from right
queue.pop() # pop from right

queue.appendLeft("append_from_left") #append from left
queue.popLeft() # pop from left

queue.index(element, begin_index, end_index) # returns first index of element btwn the 2 indices
queue.insert(index, element)
queue.remove() # removes the first occurence
queue.count()

queue.reverse()

```
#### Stack -> use list
##### Option 1: Stack using list
- Pros / cons
	- Pros:
		- built in, easy syntax
		- finding element -> have index -> O(1)
	- Cons
		- speed issues when bigger
			- items stored next to eachother in mem so if gets too big, must find new block
		- if we want to insert/delete near beginning (all must move) -- not rly stack use tho
- Operations
	- use append to append at end of list
	- use pop to pop from end
		- pop gives index error if popping from empty list
- Time Complexity
	- ![[Pasted image 20240109113437.png]]
	

```python
# implementstack as a list in python
stack = []
# push element onto top of stack
# end up with stack = [3, 2, 1]
stack.append(3)
stack.append(2)
stack.append(1)
# access last element/top
# prints 1
print(stack[-1])
# remove the top element
# end up with stack = [3, 2]
stack.pop()
```
##### Option 2: Using Collections.deque
- Pros/Cons
	- Pros
		- Can append and pop from both right and left -> not rly needed as a stack
		- Good for 'last 5' added -> allow setting of maximum length
			- can also be done in lists but built in for deque
	- Cons
		- To find an item, since it isn't indexed like a list - must iterate over, potentially whole deque
			- worst case O(n)
- Time Complexity
- 
- ![[Pasted image 20240110101207.png]]
	![[Pasted image 20240109122301.png]]
- 


#### HashMap / HashTable
- use when need to store key-val pairs and efficiently retrieve values based on their keys
	- when you add the same key, it changes vkey- value pair
	- track frequencies, counts, or occurences of elements in arrray or list
- use a dictionary

#### HashSet
- does NOT have key/value pairs
- use when need to efficiently check for presence of elements in a collection and ensure uniqueness
	- no duplicates, like a set!
	- find unique elements, identify if there is an overlap btwn 2 collecitons
	- doesnt preserve order
- Creation
	- Use dict or set
		- dict replaces duplicates lol




#### Linked List
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

##### Pros and Cons of a Linked List
###### Pros
-   good when operations are confined to 1 end of data structure
-   good w small sizes
-   simple and efficient in above cases, small size, ops at one end
 ###### Cons
	-   bad at random access
	-   bad for large
		-   have to have node object for each item I want to store

    
    -   Best Case occurs when node is at head of the list
    -   Worst case is when node is at end of the list
##### Time and Space Complexity
 - Best Case: occurs when operating on the head of the list
	 - Accessing/Seaching: O(1)
	 - Inserting at Head: O(1)
	 - Deleting at Head: O(1)
 - Worst Case: occurs when operating at the end of the list
	 - N is num of elements in list
	 -  Accessing/Seaching: O(N)
	 - Inserting: O(N)
	 - Deleting: O(N)

##### Common Operations
##### Insert
```python
#Insert
def insert(self, val):
	#create node
	n = ListNode(val)
	#make n into new head of list
	n.next = self
	return n 
```
##### Delete
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

##### Length Of List
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
##### Solving Techniques
##### Temp Head
- [Dummy Head](https://github.com/codepath/compsci_guides/wiki/Temp-Head)

###### Delete Node
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




##### Two Pointer
-   [Linked List Two Pointer](https://guides.codepath.org/compsci/Linked-List-Two-Pointer)
##### why?/ how
- iterate through list w 2+ ptrs - in diff patterns ie ptr1 moves +1 & ptr2 moves +2
- diffs in how ptrs iterate can make list calculations more efficient

##### Example: Detect Cycle in LL 
Given a linked list, determine if it has a cycle in it. Can you do it with constant extra space?

``` python
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
###### Multiple Pass
-   [Multiple Pass](https://guides.codepath.org/compsci/Multiple-Pass)
##### why? + what
- Most list comps require O(N) time complexity
- Pass through list multiple times to get summary of list to aid algorithm

###### Example: Intersection of 2 LL
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

## Built In
#### Lists
- Used to store mult items in a single variable
- ordered
- can store things of diff types
- ![[Pasted image 20240110151014.png]]
- Methods:
	- ![[Pasted image 20240110151054.png]]
Time complexities
		- avg case -> parameters are generated uniformly and at random
		- represented internally as an array
		- biggest costs from 
			- growing beyond allocation size (all must move)
			- insert/delete near beginning (all must move)
		- ** if need to add/remove at both ends -> collections.deque
	![[Pasted image 20240109113437.png]]

``` python
	nums = [1, 2, 3]
	# or
	nums = [0] * 3 #-> nums = [0,0,0]
	# or
	nums = list(range(2)) # -> nums =  [0, 1]

	nums * 3 # -> nums = [0,3]

	len(nums) # -> 2
	
	nums.index(1) # returns index of specified element from list
	nums.append(1) # appends 1
	nums.insert(0, 10) # inserts 10 at 0th index
	nums.remove(3) # removes all instances of 3
	nums.copy() # returns copy of the list
	nums.count(1) # returns no. of times '1' is present in the list
	nums.extend(someOtherList) # adds all elements of otherlist to end of list
	nums.pop() #pops last element - can also tell which index to pop
	nums.reverse() # reverses list
	nums.sort() # sorts list - does NOT return sorted list
	
	# default sort uses Tim sort, combo of merge and insertion sort
```

##### Slicing

	a[start:stop] # items start through stop-1
	a[start:] # items start through rest of array
	a[:stop] # items from beginning of array through stop-1
	a[:] # a copy of the whole array

Step Value - can be used w any of above
	a[start:stop:step] # start through stop-1 by step interval
	
	**stop is first value not in selected slice. so the diff btwn stop and start is # of elements selected if step is 1

Start or stop as neg number:
	- counts from end of the array instead of start
	
	a[-1] # the last item in the array
	a[-2:] # last two items in the array
	a[:-2] # everything except the last 2 numbers

Step as a neg number:
	a[::-1] # all items in the array, reversed
	a[1::-1] # the first two items, reversed
	a[:-3:-1] # the last two items, reversed
			# go left from end ending at item at -3 position
	a[-3::-1] # everything except the last two items, reversed
			# start at index -3 (with last item as -1, 2nd to last -2 etc) and go left

Relation to slice() object
	slicing operator [] is being used in above code with a slice() object using : notation (which is only valid within []) i.e.
		a[start:stop:step] == a[slice(start,stop,step)]
	slice objects behave diff depending on number of arguments, like range
		-could do both slice(stop) and slice(start, stop[, step])
		-a[start:] == a[slice(start, None)]
		- a[::-1] == a[slice(None, None, -1)]
	



#### Dictionary
Used to store data values in key:value pairs
![[Pasted image 20240110152445.png]]
- Operations time complexities
	- Avg case times for dict objects assume hash function is sufficiently robust to make collisions uncommon. Also assumes keys used in params are selected uniformly at random from the set of all keys
	- ![[Pasted image 20240109120601.png]]
```python
dict = {'a':1, 'b':2, 'c':3}

dict.keys() # returns list of keys of dictionary
dict.values() # returns list of values of dictionary
dict.get('a') # returns values for any corresponding key
# or
dict['a'} # but this option can give indexerrors
dict.items() # returns [('a',1),('b',2),('c',3)]
# NOTE : items() Returns view object that will be updated with any future changes to dict
dict.copy() # returns copy of the dictionary
dict.pop(KEY) # pops key-value pair associated with that key
dict.popItem() # removes most recent pair added
dict.setDefault(KEY, DEFAULT_VALUE) # returns value of key if key exists, else default value returned
# if the key doesnt exist, DEFAULT_VALUE becomes the key's value. 2nd argument's default is None. 
dict.update({KEY:VALUE}) #inserts pair in dictionary if not present, if present, corresponding value is overridden 
```
#### Counter
- container which will hopld the count of each of the elements present in the container. sub-class available inside dictionary class used for element frequencies
```python
from collections import Counter # capital C
# can also be used as 'collections.Counter()' in code

list1 = ['x','y','z','x','x','x','y', 'z']

#Initialization
Counter(list1) # => Counter({'x':4, 'y':2, 'z' : 2})
Counter("Hello there")#=> Counter({'h':2, 'e':3, ...})

#Updating
counterObject = collections.Counter(list1)
counterObject.keys() = ['x','y','z']
most_common_element = counterObject.most_common(1) # [('x', 4)]
counterObject.update("ooouuuee") # => Counter({'o':3, 'u': 3, 'e':2})
counterObject['o'] += 1 # Increase/decrease frequency

#Accessing
frequency_of_o = counterObject['o']

#Deleting
del counterObject['s']
```

#### Deque
- A double-ended queue, or deque, is able to add and remove elements from either end
- Operations time complexities
	- collections.deque
	- represented internally as double linked list. both ends accessible but looking/adding/removing from middle is slow
	- ![[Pasted image 20240109122301.png]]
```
from collections import deque

queue = deque(['name, 'age', 'DOB]) 

queue.append("append_from_right") # append from right
queue.pop() # pop from right

queue.appendLeft("append_from_left") #append from left
queue.popLeft() # pop from left

queue.index(element, begin_index, end_index) # returns first index of element btwn the 2 indices
queue.insert(index, element)
queue.remove() # removes the first occurence
queue.count()

queue.reverse()
```

#### Heapq
###### Properties
- all nodes ordered in specific way depending on type of heap. 2 types, min heaps and max heaps
		- min heaps - root node holds smallest el, all nodes in heap contain els less than or equal to their child nodes
		- max heaps - root node contains largest el, all nodes in heap contain els greater than or equal to child nodes
- complete binary tree. binary tree nodes will have at most 2 kids, right and left. heap is complete - fills each level except last - all nodes in one level will have 2 kids before any of those nodes have grandkids
- ##### Heap Operations
##### Insertion
- when new el inserted, add into next empty spot in the heap, in the right most position in the last level of the heap
	- but might violate ordering
- Then bubble up
	- min heap:
		- if parent of new el is greater than it, swap w parent
		- keep bubbling up until at root or has been put in right spot
	- max heap
		- if parent of new el is less than it, swap w parent
		- keep bubbling up until at root or in right spot
###### Removal
- always remove root node
- then last element, right most node of last element is removed + set as root
	- but might violate ordering
- then bubble down
	- min heap
		- if either of new root's kids are less than parent, swap w smaller of 2 kids
		- continue bubbling down until either at last level of heap or in right position
	- max heap
		- if either of new root's kids are greater than parent, swap w greater of 2 kids
		- continue bubbling down until either at last level of heap or in right position
###### Building a Heap from a List
- Python - heapify: constructs heap from a list in linear time

##### Implementation
```python
heapq.heapify(x)
heapq.heappush(heap, item)
heapq.heappop(heap)
```
- can be represented as an array
- root is first elementt in the array
- rest of array is filled by going through each level of heap, left to right, top to bottom
- Since heaps are complete - can calculate indices of parents + kids of each node as follows
	- -   Parent: (current index - 1) // 2 (round down)
	-   Left child: (current index * 2) + 1
	-   Right child: (current index * 2) + 2
	- ![[Pasted image 20230517113235.png]]
	- Since we have formulas, insertion and removal in array is easier
##### Runtimes
- in worse case scenario insertion + deletions will move el through height of heap
	- since heaps are complete, num of levels in heap/ height is log n
- ![[Pasted image 20230517113404.png]]
##### Key Takeaways
- esp useful for getting smallest or largest els and when you dont care abt fast lookup, delete, or search
- especially useful for getting x-largest or x-smallest else of data set
- building onlly takes O(n) time so can maybe optimize solution by building heap from list instead of running insertion n times to create the heap
- 
- Operations Time Complexities
	- 1. using heaps.heapify() can reduce time and space complexity - it is an in-place heapify and costs linear time
	- 2. both heapq.heappush() and heapq.heappop() cost O(logn)
```python
import heapq

def findKthLargest(self, nums, k):
	heaps.heapify(nums) #in place heapify - O(n)
	for _ in range(len(nums) - k): # run (N-k) times
		heapq.heappop(heap) # cost O(logn)
	return heapq.heappop(heap)
```
- total time complexity is O((n-k)logN)
- total space complexity is O(1)
``` python
import heapq # (minHeap by default)

nums = [5,7,9,1,3]

heapq.heapify(nums) # converts list into heap. can be converted back to list by list(nums)
heapq.heappush(nums, element) #push an element into the heap
heapq.heappop(nums) # pop an element from the heap
heappush(heap, element) #insert element into heap and adjust order to maintain heap
heappop(heap) # remove and return smallest element from heap and adjust order to maintain heap

# other methods available in library
# used to return the k largest elements from the iterable specified
# the key is a function which accepts a single element from iterable
# and the returned value from that function is then used to rank that element in the heap
heapq.nlargest(k, iterable, key = fun)
heapq.nsmallest(k, iterable, key = fun)
```
- Can also use key value pairs
``` python
import heapq
newDict = {
	"hey" = 1, 
	"there" = 2, 
	"the" = 2
}

# make min heap, sorted first by value, then by key
heapq.heapify(newDict)

# need max Heap?? create different type of dict
# for example, storing frequency of words and want most frequent?
# store counts as negative values
newDict = {
	"hey" = -1, 
	"there" = -2, 
	"the" = -2
}


```

#### Sets
- collection which is unordered, immutable, unindexed, no duplicates
- ![[Pasted image 20240110152250.png]]
- ![[Pasted image 20240110152403.png]]
-
``` python
set = {1,2,3}

set.add(item)
set.remove(item)
set.discard(item) | set.remove(item) # removes item | remove will throw error if item is not there, discard will not
set.pop() # removes random item (since unordered)

set.isdisjoint(anotherSet) # returns true if no common elements
set.issubset(anotherSet) # returns true if all elements from anotherSet is present in original set
set.issuperset(anotherSet) # returns true if all elements from original set is present in anotherSet

set.difference(anotherSet) # returns set containing items ONLY in first set
set.difference_update(anotherSet) # removes common elements from first set [no new set is created or returned]
set.intersection(anotherSet) # returns new set with common elements
set.intersection_update(anotherSet) # modifies first set keeping only common elements
set.symmetric_difference(anotherSet) # returns set containing all non-common elements of both sets
set.symmetric_difference_update(anotherSet) # same as symmetric_difference but changes are made on original set

set.union(anotherSet) # ...
set.update(anotherSet) # adds anotherSet without duplicate

```

#### Tuple
- collection that is ordered, unchangable (immutable), can contain duplicates
- Operations Time Complexities are similar to list
``` python
tuple = (1,2,3,1)
tuple[1] # output: 2
tuple * 3 # (3, 6, 9, 3)
len(tuple) # 4
tuple[0:2]

tuple.count(1) # returns occurence of an item
tuple.index(1) # returns index of 1 in array
```
#### Strings
General Characteristics
- immutable ( so cannot be modified)
- ordered

```python
#Find Length
len(str)

# last index is len(str) - 1

#Iteration options
#option 1
for char in str:
	print(char)

#option 2, using range()
for index in range(0, len(str)):
	print(str[index])


# split function
# breaks up a string at the specified seperator and returns a list of strings
text = 'Python is a fun programming language'

#split the text from space
print(text.split(' '))

#Output: ['Python', 'is', 'a', 'fun', 'programming', 'language']

#convert string to list
s="abcd"
s=list(s)

# count function
# the count() method returns the number of occurrences of a substring in the given string
#example
message= 'python is a popular programming language'
#number of occurences of 'p'
print('Number of occurrences of p:', message.count('p'))

#the isnumeric() method returns True if all chars in a string are numeric chars, otherwise False
s='12343'
print(s.isnumeric()) #output: True

#The find() method returns the index of first occurrence of the substring (if found). If not found, it returns -1.
# check the index of 'fun'
print(message.find('fun')) # Output: 12

#The isalnum() method returns True if all characters in the string are alphanumeric (either alphabets or numbers). If not, it returns False.

name = "M3onica Gell22er "
print(name.isalnum()) # Output : False

#The isalpha() method returns True if all characters in the string are alphabets. If not, it returns False
name = "Monica"
print(name.isalpha()) #output true

#other imp functions
string.strip([chars]) #The strip() method returns a copy of the string by removing both the leading and the trailing characters (based on the string argument passed).
string.upper() #he upper() method converts all lowercase characters in a string into uppercase characters and returns it.
string.lower() #The lower() method converts all uppercase characters in a string into lowercase characters and returns it.
string.islower()
string.isdigit()
string.isupper()
```


## Built-in or Library Functions
##### functs to iterate over list/ other iterable (tuple, dictionaries)
```
** map(fun, iter) **
#fun : It is a  transformation function to which map passes each element of given iterable.
#iter : It is a iterable which is to be mapped.
# Defining a function
def mul(i):
    return i * i

# Using the map function
x = map(mul, (3, 5, 7, 11, 13))

print (x) # output: <map object at fjdoifjo>
print(list(x)) # output: [9, 25, 29, 121, 169]

** zip(list,list) **
for elem1,elem2 in zip(firstList,secondList):
	# will merge both lists and produce tuples with both elements
	# Tuples will stop at shortest list (in case of both lists having different len)
#Example
'''
a = ("John", "Charles", "Mike")
b = ("Jenny", "Christy", "Monica")

x = zip(a, b)

#use the tuple() function to display a readable version of the result:

print(tuple(x))
o/p: (('John', 'Jenny'), ('Charles', 'Christy'), ('Mike', 'Monica'))
'''

** any(list) ** [ OPPOSITE IS => ** all() ** ]
any(someList) # returns true if ANY element in list is true [any string, all numbers except 0 also count as true]

** enumerate(list|tuple) ** 
# [when you need to attach indexes to lists or tuples ]
enumerate(anyList) # ['a','b','c'] => [(0, 'a'), (1, 'b'), (2, 'c')]

** filter(function|list) **
filter(myFunction,list) # returns list with elements that returned true when passed in function

***************** import bisect ***********************

** bisect.bisect(list,number,begin,end) ** O(log(n))
# [ returns the index where the element should be inserted 
#		such that sorting order is maintained ]
a = [1,2,4]
bisect.bisect(a,3,0,4) # [1,2,4] => 2 coz '3' should be inserted in 2nd index to maintain sorting order

# Other variants of this functions are => bisect.bisect_left() | bisect.bisect_right()
# they have same arguments. Suppose the element we want to insert is already present
# in the sorting list, the bisect_left() will return index left of the existing number
# and the bisect_right() or bisect() will return index right to the existing number

# ** bisect.insort(list,number,begin,end)       ** O(n) to insert
# ** bisect.insort_right(list,number,begin,end) ** 
# ** bisect.insort_left(list,number,begin,end)  ** 

The above 3 functions are exact same of bisect.bisect(), the only difference
is that they return the sorted list after inserting and not the index. The
left() right() logic is also same as above.
```
##### Getting the ASCII val of a char
```
** ord(str) **
# returns ascii value of the character , Example ord("a") = 97
** chr(int) ** 
#return character of given ascii value , Example chr(97) = "a"
```


## Big Overall Stuff:
 - list, string, tuple : ordered
	 - lists can be modified, strings and tuples cannot
 - dict, set: unordered
	 - dict mutable, set immutable (non modifiable)
