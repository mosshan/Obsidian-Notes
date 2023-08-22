#algorithms 
- Identify cycle
- Identify element at beginning of cycle
	- Why is this useful?
		- Find the Duplicate Number
			- array w one dup number from problem 287 can be represented in a graph form 
			- when graphed, the duplicate number will cause a cycle and be the beginning of the cycle
PHASE 1 - find if there's a cycle, also step 1 to identifying begining element of cycle
- find the first intersection point of a fp and a sp
- Using a fast and slow pointer on a graph, with fast moving 2 at a time and slow moving 1 at a time, the node where they intersect will be the beginning of the cycle
- Cycle is there!

PHASE 2 - identify beginning element of a cycle
	- leave sp at intersection point
	- take a 2nd slow pointer, put it at beginning of array
	- -------------
	-**key point** 
		distance btwn where sp is and start of cycle and from the beginning of the array to the beginning of the cycle will ALWAYS be the same
					why? - https://youtu.be/wjYnzkAhcNk?t=567
	-----------------
	- shift both by 1 until they intersect
		- intersection is the start of the cycle
