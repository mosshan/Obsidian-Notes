#math #problems 
## Problem #3: Next Prime

Given a number, return the next smallest prime number

_Note:_ A **prime** number is greater than one and has no other factors other than 1 and itself.  
  
**Examples:**

```
Input: 3
Output: 5
```

#### Understand
-   Established a set (2-3) of test cases to verify their own solution later.
    - Input: 11
    - Output: 13
    - Input: 1 
    - Output: 2
-   Established a set (1-2) of edge cases to verify their solution handles complexities.
    - Input: -3
    - Output: 2 -> smallest prime
-   Have fully understood the problem and have no clarifying questions.
    - what to do if no next smalles?
	    - wont occur, we are guaranteed a solution
	- Could it be negative?
		- yes
	- primes only have factors of itself and 1
		- This means 2, 3, 4, 5 … N-1 are not factors of this number
-   Have you verified any Time/Space Constraints for this problem?

#### Match 
- no match, math intuition

#### Plan
- if negative or 0, return 2
- infinitely loop above number, and check if num is prime
- improve checking of if number is prime: 
	- largest factor of any number: is sqrt of it
	- can loop to check if num is prime until O(sqrt n)

#### Implementation
```python
def nextPrime(n):
	if n <= 1:
		return 2
	n += 1
	while True:
		if isPrime(n):
			return n
		n +=1

def isPrime(n)
	if n < 2:
		return False
	if n < 4:
		return True
	for i in range(4, int(math.sqrt(n))):
		if n % i == 0
			return False
	return True
```

#### Evaluate
- space complexity: O(1)
- time: O(sqrt(n))