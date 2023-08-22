#heaps #problems 
## Top K Frequent Words
https://leetcode.com/problems/top-k-frequent-words/
Given an array of strings `words` and an integer `k`, return _the_ `k` _most frequent strings_.

Return the answer **sorted** by **the frequency** from highest to lowest. Sort the words with the same frequency by their **lexicographical order**.

**Example 1:**
**Input:** words = \["i","love","leetcode","i","love","coding"], k = 2
**Output:** \["i","love"]
**Explanation:** "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.

### Understand: 
- happy path
	- Input =  bird, cat, cat
	- Output: cat, bird
- edge cases:
	- Input = hi , hi, hill, hill
	- Output = hi, hill
- clarifying questions
	- can there be nonalphabetic chars?
		- no
	- will all words be lowercase?
		- yes
	- what is lexicographical order?
		- sort alphabetically
	- array is nonempty
	- only return k most frequent
### Match
- get count associated w each word
	- use hash table
- return k most frequent
	- use heap
### Plan
- get count associated with each word (word -> count, hash table)
- grab k most frequent words
	- option1: sorting algortihm ~ nlogn 
	- option2 : max heap - creation = O(n), grabbing top k elements = k * log(n) -> O(n) bc k is prob smaller than n
##### Pseudocode
```python
'''
wordToCount = calculateCount(words) # returns dictionary of word to counts
wordCountHeap = heapify(wordToCount)
result = []
for i in range(k):
	result.append(wordCountHeap.pop())
return result
'''
```
#### Implement
```python
import heapq
import collections
class Solution(object):
    def topKFrequent(self, words, k):
        """
        :type words: List[str]
        :type k: int
        :rtype: List[str]
         1. get count associated with each word (word -> count, hash table)
            - grab k most frequent words
	            - option1: sorting algortihm ~ nlogn 
	            - option2 : max heap - creation = O(n), grabbing top k elements = k * log(n) -> O(n) bc k is prob smaller than n

        wordToCount = calculateCount(words) # returns dictionary of word to counts
        wordCountHeap = heapify(wordToCount)
        result = []
        for i in range(k):
            result.append(wordCountHeap.pop())
        return result
        """
        wordToCount = self.calculateCount(words) # {word : count}
        # [(count, word), (count2, word2), ...]
        # since heapq in python is a min heap, just store count as a neg
        wordCountPairs = []
        for word, count in wordToCount.items():
            wordCountPairs.append((-count, word))
        
        heapq.heapify(wordCountPairs)
        result = []
        for i in range(k):
            result.append(heapq.heappop(wordCountPairs)[1])
        return result

    def calculateCount(self, words):
        result = collections.defaultdict(int)
    
        for word in words:
            result[word] += 1

        return result
```

#### Review
#### Evaluate
- Storage: O(n) dictionary + O(n) pair list+ O(1) heapify sorts all in place, so no extra storage+ O(k) result list - since k <= n we get O(N)
- Runtime: O(n) for dict creation + O(n) create pair list + O(n) to build heap + O(k * logn) to build result list, popping from heap --> O(N) + O(k * log N)


## Find K Pairs with Smallest Sums
https://leetcode.com/problems/find-k-pairs-with-smallest-sums/description/
You are given two integer arrays `nums1` and `nums2` sorted in **ascending order** and an integer `k`.

Define a pair `(u, v)` which consists of one element from the first array and one element from the second array.

Return _the_ `k` _pairs_ `(u1, v1), (u2, v2), ..., (uk, vk)` _with the smallest sums_.
#### Working but unoptimal solution:
```python

import heapq
class Solution(object):
    def kSmallestPairs(self, nums1, nums2, k):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type k: int
        :rtype: List[List[int]]
        Understand
            clarifying
                -  are u and v same length?
                    no
                - can i have less pairs possible than k?
                    yes
                - can one be empty?
                    no
                - can either have neg numbers?
                    - yes
                - can i use an element from 1 multiple times in pairs?
                    - yes as long as pairs arent repeated
        Match
            - min heap, return k els with smallest sums
        Plan
            - does grabbing smallest and making as many pairs with other always work?
                - no
                - [-1, 2, 3] and [0, 1, 3, 7 ] k =7 smallest pairs arent always including -1
            1. create a list of all pairs and their sums
            2. create a min heap from list
            3. return top k pairs
        Review
        Evaluate
            works but slow!!
        """
        # 1
        pairs = []
        for num1 in nums1:
            for num2 in nums2:
                pair = [num1, num2]
                sum = num1 + num2
                pairs.append((sum, pair))

        heapq.heapify(pairs)
        result = []
        for i in range(k):
            result.append(heapq.heappop(pairs)[1])

        return result

```
#### Optimal solution

```python

import heapq
class Solution(object):
    def kSmallestPairs(self, nums1, nums2, k):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :type k: int
        :rtype: List[List[int]]
        Understand
            clarifying
                -  are u and v same length?
                    no
                - can i have less pairs possible than k?
                    yes
                - can one be empty?
                    no
                - can either have neg numbers?
                    - yes
                - can i use an element from 1 multiple times in pairs?
                    - yes as long as pairs arent repeated
        Match
            - min heap, return k els with smallest sums
        Plan
            - does grabbing smallest and making as many pairs with other always work?
                - no
                - [-1, 2, 3] and [0, 1, 3, 7 ] k =7 smallest pairs arent always including -1
            - since this doesnt always work, add items slowly to min heap and pop as we add
                - smallest will always be i = 0, j = 0 index items sum
                - from there, next smallest could be i = 1, j = 0 or i = 0, j = 1
                    - but then from there, smallest might be i = 2, j = 0 or i = 0, j = 2
                        or i = 1, j = 1 
                        - so use min heap and add gradually
                        - and make sure you dont double add
            1. use min heap - add 0, 0 element
            2. create set to store added elements - init w 0, 0 element
            3. pop smallest in min heap
                - add i + 1, j and i, j + 1 elements to min heap, checking if already in set
                - add to set if added to min heap
                - repeat k times
        Review
        Evaluate
          
        """
        # 1
        pairList = [(nums1[0] + nums2[0], (0, 0))]
        heapq.heapify(pairList)
        # 2
        usedPairs = set((0, 0))

        # 3
        result = []
        while len(result) < k and pairList:
            sum, (i, j) = heapq.heappop(pairList)
            result.append((nums1[i], nums2[j]))

            if i + 1 < len(nums1) and (i + 1, j) not in usedPairs:
                heapq.heappush(pairList, (nums1[i + 1] + nums2[j], (i + 1, j)))
                usedPairs.add((i + 1, j))

            if j + 1 < len(nums2) and (i, j + 1) not in usedPairs:
                heapq.heappush(pairList, (nums1[i] + nums2[j + 1], (i , j + 1)))
                usedPairs.add((i, j + 1))

        return result
```
## K Closest Points to Origin
https://leetcode.com/problems/k-closest-points-to-origin/
Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x1 - x2)2 + (y1 - y2)2`).

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).
![](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

**Input:** points = \[\[1,3],\[-2,2]], k = 1
**Output:** \[\[-2,2]]
**Explanation:**
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just \[\[-2,2]].
```python
import heapq
class Solution(object):
    def kClosest(self, points, k):
        """
        :type points: List[List[int]]
        :type k: int
        :rtype: List[List[int]]

        Understand
            - x and y can be negative
            - k will be less than the number of points given and nonzero
            - num of points given is greater than zero
            - points are not sorted
            - can have multiple correct answers
            - if given 0, 0 return it automatically

        Match
            - k closest -> use min heap sorted by distances
        Plan
            - treat like sum problem but instead of starting at smallest index, start at point with smallest absolute value - when abs value of both nums is added? nope
            
            - add all values to min heap sorted by distance
            - pop k 
        Review:
        - 
        Evaluate
        space: O(n) + O(k) -> O(n)
        time: O(nlogn) + O(klogn) -> O(nlogn)
        """
        heap = []
        for x, y in points:
            d = (x * x) + (y * y)
            heapq.heappush(heap, (d, (x, y)))

        res = []
        for i in range(k):
            res.append(heapq.heappop(heap)[1])
        return res


```




## Sort Chars by Frequency
https://leetcode.com/problems/sort-characters-by-frequency/description/
Given a string `s`, sort it in **decreasing order** based on the **frequency** of the characters. The **frequency** of a character is the number of times it appears in the string.

Return _the sorted string_. If there are multiple answers, return _any of them_.
#### Understand
- happy
	- input = cac
	- output = cca
- edge
	- input = cat
	- output = cat or tac or atc or act or tca
	- input = ccaa
	- output: ccaa or aacc (not acac or caca, chars must be together)
- clarifying
	- can there be mult correct answers? yes
	- can the string be empty? no
	- can there be uppercase chars? yes, treated as seperate from lowercase A != a
	- can there be non alphabetic? no
#### Match
- hashset: used to count frequency of chars
- heap: want to pull them out according to frequency so yes!
#### Plan
- use hashset to count frequency of chars
- make into a list of tuples with (-count, char)
- convert to maxheap
	- add chars to string as you pull out of maxheap, appending freq # of chars to result string
	
#### Implement
```python
import collections
import heapq
class Solution(object):
    def frequencySort(self, s):
        """
        :type s: str
        :rtype: str
        """
        uniqueChars = 0
        charFrequency = collections.defaultdict(int)
        for char in s:
            if char in charFrequency:
                charFrequency[char] += 1
            else:
                charFrequency[char] = 1
                uniqueChars += 1
        charFrequencyList = []
        for char, count in charFrequency.items():
            charFrequencyList.append((-count, char))
        
        heapq.heapify(charFrequencyList)
        result = ""
        for i in range(uniqueChars):
            nextChar = heapq.heappop(charFrequencyList)[1]
            timesPresent = charFrequency[nextChar]
            for j in range(timesPresent):
                result += nextChar
        
        return result
```
#### Evaluate
- space: O(n) + O(n) + O(n) 
- runtime: O(n) + O(n) + O(logn) + O(nlogn) = O(nlogn)

## Kth Largest Element in a Stream
https://leetcode.com/problems/kth-largest-element-in-a-stream/
Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.
#### Understand
- k > 0
- at least k elements will be in array when i look for kth largest element
#### Match
	- min heap
#### Plan
- build min heap which contains only k elements
	- go through array 
		- add k els to heap O(k * log k)
		- when at k start to compare before adding O(n - k * logk)
			- if curr element is larger than min 
				- pop min O(log k)
				- add curr element to heap O(log k)
			- else
				- move to next element
		- total: O(k * log k) + O(n - k * logk) = O(n * log k)
	- or
		- for k -> O(k * n)
			- grab the max of the array -> O(n)
			- remove the max from the array O(n)
			- append to new array of maxes O(1)
		- heapify maxes array -> O(logk)
		- total -> O(k * n) + O(logk) = O(k * n)
- when adding, 
	- if heap doesnt exist or length of heap < k
		- add element to heap
		- return smallest element
	
	- compare to current min in heap
		- if smaller:
			- return current min
		- if larger:
			- pop curr min from heap
			- put element in min heap
			- return current min in heap

#### Implement
```python
#initiation slower runtime
self.k = k
maxEls = []
for i in range(k):
	currMax = max(nums)
	nums.remove(currMax)
	maxEls.append(currMax)
return heapq.heapify(maxEls)

#2nd version

import heapq
class KthLargest(object):

    def __init__(self, k, nums):
        """
        :type k: int
        :type nums: List[int]
        """
        self.k = k
        maxList = []
        heapq.heapify(maxList)
        for i in range(len(nums)):
            if i < k:
                heapq.heappush(maxList, nums[i])
            else:
                smallestMax = maxList[0]
                if smallestMax < nums[i]:
                    heapq.heappop(maxList)
                    heapq.heappush(maxList, nums[i])
        self.nums = maxList

    def add(self, val):
        """
        :type val: int
        :rtype: int
        """
        if not self.nums or len(self.nums) < self.k:
            heapq.heappush(self.nums, val)
            return self.nums[0]

        smallestMax = self.nums[0]
        if smallestMax < val:
            heapq.heappop(self.nums)
            heapq.heappush(self.nums, val)
            return self.nums[0]
        else:
            return smallestMax
        
# improved logic final
import heapq
class KthLargest(object):

    def __init__(self, k, nums):
        """
        :type k: int
        :type nums: List[int]
        """
        self.k = k
        length = len(nums)
        kLargest = []
        heapq.heapify(kLargest)
        for i in range(length):
            heapq.heappush(kLargest, nums[i])
            # keep heap at k size
            if i >= k:
                heapq.heappop(kLargest)
        self.nums = kLargest
        

    def add(self, val):
        """
        :type val: int
        :rtype: int
        """
        if not self.nums or not len(self.nums) == self.k:
            heapq.heappush(self.nums, val)
        else:
            if val > self.nums[0]:
                heapq.heappop(self.nums)
                heapq.heappush(self.nums, val)

        return self.nums[0]
# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)
```

#### Review
- remember to check for edge cases
	- the list might not have k elements until you add items first
#### Evaluate
- init
	- space: O(k)
	- runtime: O(n logk)
- add
	- space: O(1)
	- runtime: O(logk)

## Last Stone Weight
Given an array of ints stones where stones\[i] is the weight of the ith stone
Playing game w stones. on each turn - choose heaviest 2 stones w weights x and y where x <= y and smash together
	- if x == y both destroyed
	- if x != y, stone of weight x is destroyed. other now has weight y -x 
At end of game at most 1 stone left
- return weight of last remaining stone or 0 if none are left
	
#### Understand
- can i have no stones? no
- can weight only be positive? yes
- can i have just one stone? yes
- edge:
	- input = \[2]
	- output = 2
	- input = \[2,2]
	- output = 0
#### Match
- could use a heap to quickly pull heaviest stones 
#### Plan
- start by putting all of stones into a max heap 
	- since python only has a min heap built in, convert weights to negative values in array before putting into heap so that max weight will be at top
	- two options
		- convert to negative then make whole list into heap -> better option
			- O(n) + O(logn) = O(n)
		- convert 1 by 1 and then 1 by 1 add to heap
			- O(n * logn)
- while heap: O(n * logn)
	- grab 1 stone, and convert weight to positive, weight = y  O(logn)
	- if heap: # need to check if there was just one stone, in case, we return
		- grab 2nd stone and convert weight to positive, weight = x O(logn)
			- if they are equal:
				- continue
			- if y > x:
				- push onto heap stone with weight -(y - x) O(logn)
	- else:
		- return y
- return 0 # no stones left!!
#### Implement
```python
import heapq
class Solution(object):
    def lastStoneWeight(self, stones):
        """
        :type stones: List[int]
        :rtype: int
        """
        for i in range(len(stones)):
            stones[i] = -stones[i]
        heapq.heapify(stones)

        while stones:
            y = -heapq.heappop(stones)
            if stones:
                x = -heapq.heappop(stones)
                if y > x:
                    heapq.heappush(stones, -(y-x))
            else:
                return y
        return 0
```
#### Review
- check for loops and while loops for : and what I am accessing (is it the correct range?)
- make sure all edge cases are accounted for, like if we don't end up with any stiones bc theyve all destroyed eachother, still need a relevant return
#### Evaluate
- Space: O(n)
- Runtime: O(n) + O(nlogn) = O(nlogn)

		
	
