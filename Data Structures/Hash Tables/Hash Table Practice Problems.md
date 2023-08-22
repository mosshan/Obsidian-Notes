#hashtables #problems 
## Isomorphic Strings
https://leetcode.com/problems/isomorphic-strings/description/
Given two strings `s` and `t`, _determine if they are isomorphic_.

Two strings `s` and `t` are isomorphic if the characters in `s` can be replaced to get `t`.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.
```python
import collections
class Solution(object):
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        Understand:
            edge: 
                input: s = "ss" t = "tt"
                output: true
                input: s = egd t = adf
                output: true
            clarifying: 
                - nonalpha?
                    yes
                - strings are same length
                - can a string be empty?
                    - no
                - can it map to itself? 
                    - yes
        Match:
            - see if throughout both strings, there is a one to one char match
            - hash table
        Plan:
            1. two hash maps
                - one to verify if same char from s maps to a different char t
                - one to verify if char t maps to dfferent char from s 
        Review:
            - initially got first thing but not second, ensuring each char from s can only map to one char from t ie if a-> b, then a-> c will return false
            - however, missed out on logic of 1 to 1 mapping ensuring that it each char from t can only map to one char from s ie if a <- b then e <- b will return false 
        Evaluate:
            - space: O(n) + O(n) + O(1) = O(n)
            - runtime: O(n)
        """
        sAsKeys = collections.defaultdict(list)
        tAsKeys = collections.defaultdict(list)
        length = len(s)
        for i in range(length):
            charS = s[i]
            charT = t[i]
            # scenario s = bab t = bdf
            if charS in sAsKeys:
                if sAsKeys[charS] != charT:
                    return False
            else:
                sAsKeys[charS] = charT
            # scenario s = badc t = baba
            if charT in tAsKeys:
                if tAsKeys[charT] != charS:
                    return False
            else:
                tAsKeys[charT] = charS
        return True
        
```
## Happy Number
https://leetcode.com/problems/happy-number/description/
Write an algorithm to determine if a number `n` is happy.

A **happy number** is a number defined by the following process:

-   Starting with any positive integer, replace the number by the sum of the squares of its digits.
-   Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
-   Those numbers for which this process **ends in 1** are happy.

Return `true` _if_ `n` _is a happy number, and_ `false` _if not_.
```python
import collections
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        Understand:
	        happy: 
	        Input: n = 19
		        19 -> 82 -> 68 -> 100 -> 1
			Output: true
		
            edge:
                input n = 2
                    2 -> 4 -> 16 -> 37 -> 58 -> 89 -> 145 -> 42 -> 20 -> 4
                output: false
            clarifying:
                - n cannot = 0
                - ints given are positive
        Match:
            - hash table
                - this can detect a loop in the numbers
        Plan:
            - create a hash table key = sum of squared ints value = 1
            - loop until either sum of squared ints == 1 or we hit a value that already exists in our hash table, meaning we have a cycle
        Review:
            - make sure modulo math is understood
            - could simplify digit square sums section
        Evaluate:
            - space: O(n)
            - runtime: O(n) * log base 10 n + 1
        """
        digitSquareSums = collections.defaultdict(int)
        while True:
            if n == 1:
                return True
            if n in digitSquareSums:
                return False
            digitSquareSums[n] += 1
            n = self.sumOfDigitsSquared(n)
        
    def sumOfDigitsSquared(self, n):
        sum = 0
        while n > 0:
            digit  = n % 10
            sum += (digit * digit)
            n /= 10
        return sum
```

## Brick Wall
https://leetcode.com/problems/brick-wall/
There is a rectangular brick wall in front of you with `n` rows of bricks. The `ith` row has some number of bricks each of the same height (i.e., one unit) but they can be of different widths. The total width of each row is the same.

Draw a vertical line from the top to the bottom and cross the least bricks. If your line goes through the edge of a brick, then the brick is not considered as crossed. You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.

Given the 2D array `wall` that contains the information about the wall, return _the minimum number of crossed bricks after drawing such a vertical line_.
**Input:** wall = \[\[1,2,2,1],\[3,1,2],\[1,3,2],\[2,4],\[3,1,2],\[1,3,1,1]]
**Output:** 2

#### Understand
- can there be multiple paths which cross the same amt of bricks?
	- yes
- cant go at edge of wall
- if at edge of brick, cant cross
- where are places I can cross?
	- if the wall has 6 width, can cross at 1, 2, 3, 4, 5
	- if width = n, can cross at 1 to n-1 inclusive
- wall has same total width accross
- input array cannot be empty
#### Match
- stack - not useful for this, sense of order unhelpful
- queue - not useful for this, sense of order unhelpful
- hash table - useful for this, can store num of noncollisions per row for easy access
- heap -nope
#### Plan
- put all crossing values in a min heap
	- how to calculate num of bricks crossed at each row? rows = 1 through n - 1 (n == total width of wall)
	- calculate array of rows which are brick edges for each layer
		- with bricks lengths 1, 2, 2, 1 edges are 0, 1, 3, 5, 6 (start at 0, add lengths of bricks to total width 1 by 1 putting total into array as we go)
	- for each row 1 btwn 1 and n -1,  count the number of times it is present in the edge array, keeping track of max
		- these are how many times it doesnt pass through a brick
		- row with max number of times it doesnt pass through a brick will have min number of crossed bricks
	- return the total height - the max number of times a row doesnt cross a brick
- Really bad for looking through lots of rows
- V2
- use a hashmap storing how many times a row has not collided with a brick
- for each row in the wall use a running total to calculate edges and store in the hashmap
- then return the length of the wall (total number of possible collisions) - the max vlaue in the hashmap ( row with most times noncollided)
#### Implement
```python
import collections
class Solution(object):
    def leastBricks(self, wall):
        """
        :type wall: List[List[int]]
        :rtype: int
        """
        m = collections.defaultdict(int)
        for row in wall:
            total = 0 
            for brick in row[:-1]:
                total += brick
                m[total] += 1
        if len(m) < 1:
            return len(wall)

        return len(wall) - max(m.values())
```
#### Review
- focus on using data structures not brute forcing wihtout!
- had right idea but using a data structure improved it greatly
#### Evaluate
- space: O(n * m) where n = max bricks per row and m = number of rows
- runtime: O(n * m)



## Contains Duplicate
given int array nums,
	return true if any val appears at least twice in the array or false if every element is distinct
#### Understand
- element can appear more than twice
- can more than one element appear more than once?
	- yes
- can array be empty? no
- can array have single value?
	- yes, return false
- edge:
	- input \[1]
	- output: false
	- input \[2, 2, 4, 4]
	- output: true
	- input: \[-1, 1]
	- output: false
- happy: 
	- input: \[1, 2, 3]
	- output: false
	- input: \[1,2, 2]
	- output = true
#### Match
- hash set
#### Plan
- create empty dictionary
- for num in nums
	- check if num is in dict
		- if yes
			- return true
		- if no
			- put in dict
- return false
#### Implement
```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        foundNums = {}
        for num in nums:
            if num in foundNums:
                return True
            else:
                foundNums[num] = 1
        return False
```
#### Review
- make sure to mark True and False not true and false!!!!
#### Evaluate
- space: O(n) where n is number of ints in nums
- runtime: O(n)