#### Overview
- Used to store mult items in a single variable
	- items can be of diff types
	- ordered
	- size is dynamic
	- built in to python
	- ![[Pasted image 20240110151014.png]]
	- ![[Pasted image 20240110151054.png]]
#### Pros/Cons
- Pros
	- store mult items in single var
	- access is fast as long as u have index (w ll travel from head)
- Cons
	- addition/removal is slow in middle or front bc all elements must be shifted
#### Common Terms
- subarray - range of contiguous vals within array
- subsequence - sequence that can be derived from given sequence by deleting some or no elements without changing order

#### Time Complexity
![[Pasted image 20240111155050.png]]
		- avg case -> parameters are generated uniformly and at random
		- represented internally as an array
		- biggest costs from 
			- growing beyond allocation size (all must move)
			- insert/delete near beginning (all must move)
		- ** if need to add/remove at both ends -> collections.deque

#### Things to look out for in interviews
1. Validating Assumptions
	1. Duplicates?
	2. Sorted/unsorted
2. Boundary Condits
	2. Negative Index to access from end of array
3. Efficiency
	1. Slicing and concat take O(n) time!!

#### Techniques
- sliding window
	- often used for subarray/substring probs
	-  2 ptrs move in same direction never overtake eachother
- Two pointers
	- more general version of sliding window - pointers can cross eachother and be on 2 diff arrays
	- like in merge arrays
- traversing from the right
- Sorting the array
	- allows for binary search
- precomputation
	-summation or mult of a subarray
	- can precomputer using hashing or prefix/suffix sum/product
- index as a hash key
	- use array as a hash table 
	- array has vals from 1 to N, n being length of array, negate value at that index to indicate presence of that number
- multiple [ass
	- O(n)




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
	



