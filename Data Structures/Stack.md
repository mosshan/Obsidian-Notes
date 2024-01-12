	
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

