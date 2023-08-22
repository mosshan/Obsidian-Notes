 #heaps 
### Introduction
- tree based data structs
- satisfy 2 properties:
	- 1. all nodes ordered in specific way depending on type of heap. 2 types, min heaps and max heaps
		- min heaps - root node holds smallest el, all nodes in heap contain els less than or equal to their child nodes
		- max heaps - root node contains largest el, all nodes in heap contain els greater than or equal to child nodes
	- 2. complete binary tree. binary tree nodes will have at most 2 kids, right and left. heap is complete - fills each level except last - all nodes in one level will have 2 kids before any of those nodes have grandkids
- ![[Pasted image 20230517111858.png]]
### Heap Operations
#### Insertion
- when new el inserted, add into next empty spot in the heap, in the right most position in the last level of the heap
	- but might violate ordering
- Then bubble up
	- min heap:
		- if parent of new el is greater than it, swap w parent
		- keep bubbling up until at root or has been put in right spot
	- max heap
		- if parent of new el is less than it, swap w parent
		- keep bubbling up until at root or in right spot
#### Removal
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
#### Building a Heap from a List
- one option to build a heap of N elements
- NONOPTIMAL:  start w empty heap, add each el from a list one at a time
	- takes O(nlogn) time
		- performs N insertions, each taking log N time
- OPTIMAL: Takes O(N) time but is complex
- Python - heapify: constructs heap from a list in linear time

#### Implementation
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
#### Runtimes
- in worse case scenario insertion + deletions will move el through height of heap
	- since heaps are complete, num of levels in heap/ height is log n
- ![[Pasted image 20230517113404.png]]
#### Key Takeaways
- esp useful for getting smallest or largest els and when you dont care abt fast lookup, delete, or search
- especially useful for getting x-largest or x-smallest else of data set
- building onlly takes O(n) time so can maybe optimize solution by building heap from list instead of running insertion n times to create the heap