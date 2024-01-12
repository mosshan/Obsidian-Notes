- given text and pattern, print all occurences of pattern in t!

- Use rolling hash value, removing contribution of old char and adding new as you slide over text
Step 1: choose suitable base and mod
- prime number p as mod
- base b -> usually size of char set (256 for ASCII)
Step 2: Init hash value
- set init hash value to 0
Step 3: Calc initial hash for pattern
- iterate over pattern left to right
- for each char c at position i -> contribution to hash value is 
	- c * (b ^(pattern_length - i - 1)) % p
- add to hash
Step 4: slide pattern over text
- start by calcing first substring of text same length as pattern
Step 5: update hash val for each subsequent substring
- remove leftmost char contribution and add char on right contribution
- ![[Pasted image 20240112105525.png]]
Step 6: compare hash values
- if hash value of substring matches pattern -> potential match
- do char by char comparison