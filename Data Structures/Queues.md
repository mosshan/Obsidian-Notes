#### Queue -> use collections.deque
- FIFO (like a line lol)
### Simple Queues
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
		- represented internally as double linked list
- Time Complexity
	- ![[Pasted image 20240109122301.png]]
- Code
``` python
from collections import deque

queue = deque(['name, 'age', 'DOB]) 

queue.append("append_from_right") # append from right
queue.pop() # pop from right

queue.appendleft("append_from_left") #append from left
queue.popleft() # pop from left

queue.index(element, begin_index, end_index) # returns first index of element btwn the 2 indices
queue.insert(index, element)
queue.remove() # removes the first occurence
queue.count()

queue.reverse()

```
##### Option 3: Implement w linkedlist (self made)
``` python
class Node():
	def __init__(self, val):
		self.val = val
		self.next = None
class Queue():
	def __init__(self):
		self.front = None
		self.rear = None
		self.size = 0
		
	def enqueue(self, val):
		node = Node(val)
		if self.size == 0:
			self.front = node
			self.rear = node
		else:
			self.rear.next = node
			self.rear = node
		size += 1
		
	def dequeue(self):
		if self.size == 0:
			return null
		else:
			popped = self.front
			self.front = self.front.next
			self.size -= 1
			if self.size == 0:
				self.rear = None
			return popped.val
			
	def peek(self):
		if self.size == 0:
			return None
		return self.front.val
		
	def isEmpty(self):
		return self.size == 0
		
	def getSize(self):
		return self.size
		
```


### Circular Queues and Deques (double ended queue)
- deque allows operations on both sides
- circular queues
	- enqueue:
		- add it to rear and increment rear pointer
			- if we reach biggest index of our array, wrap around and continue from front (unless array is full)
	- dequeue:
		- remove from front and increment front pointer
		- if we reach biggest index of array of array while dequeuing, wrap around and continue from 0 th index of array, if there are elements there to deque
	- essentially front doesnt always stay at 0 and rear could go from 7 to 0 if array has size 8


### Common Uses
- BFS
	- visit nodes of tree in breadth first manner. start at given node and add all neighbor nodes at current depth to queue. then  we explore all neighbor nodes at current depth, and when we explore each, we add its neighbor nodes at next depth to end of queue.   queue tells us order of exploration