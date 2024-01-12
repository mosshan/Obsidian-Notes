- Time Complexity: O(n^2)
	- goes through array n times looking at n elements each time
- Space Complexity: O(1) -> in place
- ![[Pasted image 20240112131348.png]]
- Traverse from left
	- compare adjacent elements
	- higher one is placed at right side
- largest element is moved to rightmost end first
- continued to find 2nd largest and place it until sorted

- bubble up largest element 1 at a time
``` python
def bubbleSort(arr):
	n = len(arr)
	# we need to move n times
	for i in range(n):
		# option for spots decreases each time, as we find next largest
		# in first round, we compare until last index, putting biggest all the way to the right
		# in the second round, we compare until 2nd to last index
		for j in range(0, n - 1 - i):
			if arr[j] > arr[j + 1]:
				temp = arr[j]
				arr[j] = arr[j + 1]
				arr[j + 1] = temp
```