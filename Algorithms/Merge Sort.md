- divide and conquer
- Time Complexity:
	-O(nlogn)
		- logn levels of calls
		- and each level will take time proportional to number of records so O(n)
		- ![[Pasted image 20240112151126.png]]

- Space Complexity:
	- O(n) - only n deep on call stack at once (finishes mergesort(l) b4 it goes to mergesort(r))

- cut list into sublists until each has only 1 item then merges sublists into a sorted list
``` python
def mergeSort(arr):
	if len(arr) > 1:
		mid = len(arr) //2
		l = arr[:mid]
		r = arr[mid:]
		# merge sort on l and right which changes our l and r
		mergeSort(l)
		mergeSort(r)

		i = j = k = 0
		# copy data to temp arrays l[] and r[]
		while i < len(l) and j < len(r):
			if l[i] <= r[j]:
				arr[k] = l[i]
				i += 1
			else:
				arr[k] = r[j]
				j += 1
			k += 1
		while i < len(l):
			arr[k] = l[i]
			i += 1
			k += 1
		while j < len(r):
			arr[k] = r[j]
			j += 1
			k += 1 
```