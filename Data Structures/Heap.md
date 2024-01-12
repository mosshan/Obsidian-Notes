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
