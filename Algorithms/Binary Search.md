``` python
def binarysearch(l, r):
	if l > r:
		return -1
	m = l + r //2
	if nums[m] == target:
		return m
	elif nums[m] > target:
		return binarysearch(1, m -1)
	else:
		return binarysearch(l, m + 1)
```