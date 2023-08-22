#stack #queue
### Intro
- useful when adding or removing in particular orders
- DFS and BFS use them for graph traverslas
### Stacks
- LIFO: last in first out
	- like stack of plates
##### Common Operations
- push: add els to stack
- pop: remove els from stack
- top (peek): returns first value/what is on top of stack but doesnt remove
- isEmpty: checks if stack is empty or not
- size: returns num of elements on stack
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


### Queues
- FIFO: first in, first out
	- like a line at a bank
##### Common Operations
- enqueue: add els to queue
- dequeue: remove first element from stack
- peek: return first value (first in queue) but doesnt remove it
- isEmpty: checks if queue is empty
- size: returns number of elements in queue at any given time
### Key Takeaways
![[Pasted image 20230517110542.png]]
- Stacks are useful for backtracking features
	- parsing Qs use stacks bc of LIFO
- stacks can be used to implement recursive solutions iteratively
- Queues useful when ordering of data matters
	- like for caching