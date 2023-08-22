#referenceguide #bigo
- Very important in interview
	- helps to evaluate diff approaches quickly
- Both time and space complexity are important
	- Talk abt time/space trade offs for different approaches
- Be clear what vars mean in analysis!
	- what is N?
## Diff runtimes
- constant O(1)
	- Runtime does not scale with input
	- ![[Pasted image 20230524094039.png]]
- Logarithmic O(logn)
	- numbers in problem space get divided by some factor each time
	- ![[Pasted image 20230524094055.png]]
- Linear O(n)
	- Grows proportionally with the size of the input
	- ![[Pasted image 20230524094202.png]]
- Quadratic O(n^2)
	- common for double for loops
	- Note: the series 1 + 2 + 3 + ... + n is also O(n^2)
	- ![[Pasted image 20230524094255.png]]
- Exponential: O(2^n)
	- Can occur w recursive solutions
	- ![[Pasted image 20230524094332.png]]
## Rules for Big O Analysis
- diff steps get added together
	- drop non dominant terms O(N^2 + N) = O(N^2)
	- Preprocessing which is less than dominant term doesnt impact overall runtime
- Drop the constants
	- O(2N) = O(N)
- Specify diff vars for diff inputs/ input dimensions
	- ie n is number of ints and m is number of arrays 

## Example
#### Problem
You have k lists of sorted integers in ascending order. Find the smallest range that includes at least
one number from each of the k lists. We define the range \[a,b] is smaller than range \[c,d] if b-a < d-c or a < c if b-a == d-c.
- Example 1:
	- Input:  \[\[4,10,15,24,26], \[0,9,12,20],\[5,18,22,30]]
	- Output: \[20,24]
	- 
	- Input: \[\[1, 22, 24, 27, 28, 35, 36],\[7, 8, 12, 32, 37, 39],\[2, 5, 14, 18, 23, 29]]
	- Output:\[28, 32] 
- Key Pts
	- lists are sorted
	- lists are various sizes
	- can have duplicate elements
	- overwhelming example
#### Brute Force
- Steps
	- Generate all possible ranges from all items
	- For each range, check if num from each array falls into range
	- keep track of the smallest range, updating accordingly
- Runtime? N = number of items in the matrix
	- Number of Ranges * Checking every item = O(N^2) * O(N) = O(N^3)
- Inefficiencies
	- redundant range checks
		- once we find a valid range, we keep checking larger ranges
	- don't take advantage of lists being sorted
#### Working through example
- Input: \[\[1, 2, 6],\[5, 7],\[2, 8, 20]]
- Look at first element in each list:
	- 1, 5, 2 - 1= min 5 = max
	- best range  = \[1,5]
- Options
	- Option 1: in the first row, swap the 1 to a 2 
		- Range for these # = \[2, 5]
		- Previous Range= \[1,5]
	- Option #2: in the 2nd row, swap a 5 for a 7
		- Range for these #: \[1,7]
		- Previous Range: \[1,5]
	- Option #3: in the 3rd row, swap a 2 for an 8
		- range for these= \[1, 8]
		- previous range: \[1,5]
- Best option = #1 so current best range is \[2,5]
	- ![[Pasted image 20230524100336.png]]
- Options round 2: 
	- smallest val in range is 2 so swap to neighbor
	- ![[Pasted image 20230524100358.png]]
- options round 3: current range: \[2,6] best:\[2,5]
	- smallest el is 2, swamp to neightbor, 8
	- ![[Pasted image 20230524100616.png]]
- Options round 4: current range \[5, 8] best: \[2, 5]
	- smallest el is 5, swap to 7
		- minimum value of the range is the end of an array
	- New best: \[6,8]
	- ![[Pasted image 20230524100802.png]]

#### High Level Plan
1. look at first els in each list as initial working set
2. calculate range for this set by finding min & max
3. Find the smallest number from the working set
4. swap the smallest number w its neighbor ( next in list)
5. Calculate new range from new working set from the min and max
	1. if better than old range, store new one
6. rpt until last element of a list is the min of a range and we're done
Runtime: N is num of elements, K is num of lists O(K * N)
Improvements: Running max, use a heap
#### Pseudocode
- put first els of list in a min heap
- get range and max of those nums
- while heap is not empty:
	- remove num from the heap, use it as a new min
	- calculate the new range, running max - new min
	- update the best range if this new range is smaller
	- get the list correlating to this min
	- if this min has no neighbor in its list (end of list):
		- stop and return the best range
	- else:
		- move one index down in that list and fetch the neighbor
			- (need to store which row, index in row in the heap)
		- compare new element: set new max to be this element if needed
		- add to min heap
##### Space and time complexity:
- k lists and N total elements
- Space: O(K)
- time complexity: O(n * logk)