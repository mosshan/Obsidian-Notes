- Recursive, uses divide and conquer
- Time Complexity
	- Avg: O(nlogn)
	- worst: O(n^2)
		- if pivot is always smallest or largest element in the array
- Space Complexity:
	- O(logn) on avg -> makes logn recursive calls
	- or O(n) at worst if pivot is smallest/largest element and we need to make O(n) calls
- How it works:
	- select pivot element
	- partition array into 3 subarrays
		- less than pivot, more than pivot, equal to pivot
			- compare pivot to all items starting wiht first index
			- if element > pivot
				- add 2nd pointer pointing to larger element
			- if element < pivot
				- swap w larger element
			- all sorted?
				- swap pivot w 2nd pointer
	- recursively sorts left and right
	- all work is in partition - none in quick sort
	- 
``` python
def quickSort(arr):
	# base case
	if(low < high):
		# Find Index of chosen pivot when partitioned such that
		# element smaller than pivot are on left
		# element larger than pivot are on right
		pivotIndex = partition(arr, low, high)
		# recursively sort left elements
		quickSort(arr, low, pivot - 1)
		#recursively sort right elements
		quickSort(arr, pivot + 1, high)

def partition(arr, low, high):
	pivot = arr[high]
	# index of smaller element indicates right position of pivot found so far
	pivotIndex = low
	for i in range(low, high):
		if arr[i] <= pivot:
			# smaller element than pivot, move it to the current planned position for pivot
			arr[pivotIndex], arr[i] = arr[i], arr[pivotIndex]
			# update pivot position to 
			pivotIndex += 1
			# if bigger, no need to do anything, pivot index doesnt change and we wont swap
	# swap pivot 
	arr[pivotIndex ], arr[high] = arr[high], arr[pivotIndex]
	return pivotIndex
			
	
			
	
```