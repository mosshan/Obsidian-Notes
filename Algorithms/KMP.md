- given text and pattern print all occurrences of pattern in text
- O(m + n) worst case -> n = num of chars in text, m = num of chars in pattern
Basic Idea
- whenever detect a mismatch after some matches, already know some of chars in text of next window
	- when we see a mism