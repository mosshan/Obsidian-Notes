 #problems #stringsarrays 

## Problem #1: Substring
#stringsarrays 
Write a function that takes in two strings and returns `true` if the second string is **substring** of the first, and `false` otherwise.  
  
**Examples:**

```
Input: laboratory, rat
Output: true

Input: cat, meow
Output: false
```

U: Understand 
-   Established a set (2-3) of test cases to verify their own solution later.
	    Input: catharsis, cat
	    Output: true

			Input: wow, sub
			Output: false
-   Established a set (1-2) of edge cases to verify their solution handles complexities.
	- Input: cat, catharsis
	- Output: false

		Input: try, ""
		Output: true
-   Have fully understood the problem and have no clarifying questions.
	    - Just letter chars?
	    - Can we have empty strings?
	    - can the 2nd string be larger than the first?
	    - are both inputs only strings?
	    - 
-   Have you verified any Time/Space Constraints for this problem?
	- Best Space: 
	- Best Time: 

#### Match
- String/Array problem
	- Common solutions: 
		- 2 ptr solution, left and right ptr vars, or a ptr on each string
		- Storing chars of string in hashmap or a set
		- sliding window traversal

#### Plan
- Edge cases
	- if 2nd string is larger, return false
	- if 2nd string is empty, return true
- Use sliding window
	- traverse 1st string until we find match to 2nd string first character
		- If find match, check 2nd char and continue traversing until either: 
			- have full string matched -> return true
			- hit unmatched letter
				- don't move on to next but start again at 1st string first character
	- if hit end of 1st string without full match, return false
	- 2 while loops?

```python
def isSubstring(s1, s2):
	#even though using len multiple tmes, has a runtime of O(1) bc it is automatically incremented when data is defined/stored so doesnt make sense to create new vars
	if len(s2) > len(s1):
		return False
	if len(s2) == 0:
		return True
	for i in range(len(s1)):
		largeIndex = i
		j = 0
		# while chars match and not out of bounds of either string, loop
		while s1[largeIndex] == s2[j] and largeIndex < len(s1) and j < len(s2):
			if j == (len (s2) - 1):
				return True
			j++
			largeIndex++
	return False
```
#### Review
	- Check that the code works with happy cases 
	- Check that the code works with edge cases 

#### Evaluate
- Space Complexity?
	- O(1)-> I dont use any auxiliary structures, just vars
- Time Complexity?
	- O(n * m ) where n = length of string 1 and m = length of string 2
- Could I make my solution more efficient?
	- could assign mult vars at once, not more efficient but less lines
	- also could increment before checking if at end of s2, then just check if j == len(s2)

## Problem #2 Valid Palindrome

Original Problem on Leetcode: [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a **palindrome**, or `false` otherwise.

**Examples:**

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```
#### Understand
-   Established a set (2-3) of test cases to verify their own solution later.
	- Input: hannah
	- Output: true
	- Input: !cat tac
	- Output: true
    
-   Established a set (1-2) of edge cases to verify their solution handles complexities.
	- Input: ""
	- Output: true
	- Input: CAc
	- Output: true
    
-   Have fully understood the problem and have no clarifying questions.
	- Can be given strings w nonalpha chars
	- can be given empty string
    
-   Have you verified any Time/Space Constraints for this problem?
	- space: O(1)
		- can use two pointers one at front one at end
	- time: O(n)

#### Match
- String problem
	- cna be approached w two pointer, sliding window, or storing string charas in hashmap or set
	- chosen: two pointers

#### Plan
- have ptr at beginning and end of string
	- while start ptr < end (cant check if they meet bc could be even num of chars):
		- move strt pointer to right until at an alphanumeric char
		- move end ptr to left until reaches alphanumeric
		- if alpha, put to lowercase
		- check if chars are same
			- if not, return false
			- if true, keep going 
	- return true

#### Implement https://leetcode.com/problems/valid-palindrome/
```python
# iterative
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        start = 0
        end = len(s) - 1
        while start < end:
            while start < len(s) and not s[start].isalnum():
                start += 1
                continue
            while end > -1 and not s[end].isalnum():
                end -= 1
                continue

            if start < len(s) and end > -1 and s[start].lower() != s[end].lower():
                return False
            start += 1
            end -= 1
        return True
# can also make recursive version
```

#### Review
- works for both cases!
- realized had not actually incremented start and end !!!! 

#### Evaluate
- Space: O(1)
- Time: O(n)
- efficiency improvements: 



## Find a Celebrity
Suppose you are at a party with `n` people (labeled from 0 to n - 1) and among them, there may exist one celebrity. The definition of a celebrity is that all the other `n - 1` people know them but they do not know any of them.

**Goal:** You want to find out who the celebrity is or verify that there is not one.
**Output:** The number associated with the celebrity, or -1 if no celebrity present.  
  
The only thing you are allowed to do is to ask questions like:

```
"Hi, A. Do you know B?" to get information of whether A knows B. 
```
You need to find the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).  

You are given a helper function `knows(a, b)-->bool` which tells you whether `A` knows `B`.

Implement a function `findCelebrity(n)-->int`, your function should minimize the number of calls to `knows(a, b)`.
#### Understand
- there can be no celebrity yep! return -1
- can there be two?
	- no, paradox, a celeb is known by all, so other would have to know them and then be by def not a celeb
- can there be 0 ppl at the party?
	- yes, no celeb
- what if just 1?
	- has a celebrity
```
HAPPY CASE
Input: 5
   0  1  2  3  4
0 |0  0  1  0  0
1 |0  0  1  0  0
2 |0  0  0  0  0
3 |0  0  1  0  0
4 |0  0  1  0  0

Output: 2

HAPPY CASE
Input: 5
   0  1  2  3  4
0 |0  0  0  0  1
1 |0  0  0  1  0
2 |0  1  0  0  0
3 |0  0  0  0  0
4 |1  0  0  1  0

Output: -1

EDGE CASE
Input: 0 (No people at the party)
Output: -1
```

#### Match
- stack or queue
	- ordering isnt helpful
- hash map
	- helpful, quick access to marking who knows who
- heap
	- will only be 1 celeb
#### Plan
	-two pointers 
	-start at person 0 and person n -1
	- check if l knows r
		- if l knows r, l can't be celeb
			- 1++ 
		- if l doesnt know r, r cant be celeb
			- r--
		- if l == r
			- might have celeb
			- loop through rest and check that all know them and they dont know any others
### Implement
```python
def findCelebrity(n):
	l , r = 0, n - 1
	while l < r:
		if knows(l, r):
			l += 1
		else:
			r -= 1
	for i in range(n):
		if i != l and (knows(l, i) or not knows(i, l)):
			return -1
	return l
```
#### Review
- try at least 15 minutes of thinking through solutions when cant find one, or one is long runtime
#### Evaluate
space: O(1)
runtime: O(n)