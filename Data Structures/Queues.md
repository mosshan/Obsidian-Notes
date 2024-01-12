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
		- represented internally as double linked list
- Time Complexity
	- ![[Pasted image 20240109122301.png]]
- Code
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