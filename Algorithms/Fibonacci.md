- 0, 1, 1, 2, 3, 5, 8, 13, 21
- calculate nth element of fibonacci
- Time Complexity
	- O(2^n)
		- each call to fib(n) results in 2 additional recursive calls
		- think of it like a tree of calls with n layers
			- each call spawns 2 calls 
- Space Complexity:
	- O(n)
		- depth of tree of calls is proportional to size n  
		- fib(n -1) is evaluated completely before fib(n -2) so never more than n levels of recursion on stack at once
	
``` python
def fib(n):
	# base case
	if n == 0:
		return 0
	if n == 1:
		return 1
		
	return fib(n - 1) + fib(n - 2)
```