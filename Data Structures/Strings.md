
#### General Characteristics
	Built in to Python
- immutable ( so cannot be modified)
- ordered

### Common String Algos
- Rabin-Karp 
	- find substrings in text which match given pattern
- KMP
	-  find substrings in text which match given pattern

#### Big O
![[Pasted image 20240112110310.png]]

#### Functions

```python
#Find Length
len(str)

# last index is len(str) - 1

#Iteration options
#option 1
for char in str:
	print(char)

#option 2, using range()
for index in range(0, len(str)):
	print(str[index])


# split function
# breaks up a string at the specified seperator and returns a list of strings
text = 'Python is a fun programming language'

#split the text from space
print(text.split(' '))

#Output: ['Python', 'is', 'a', 'fun', 'programming', 'language']

#convert string to list
s="abcd"
s=list(s)

#list to string!!!
"".join(s)

# count function
# the count() method returns the number of occurrences of a substring in the given string
#example
message= 'python is a popular programming language'
#number of occurences of 'p'
print('Number of occurrences of p:', message.count('p'))

#the isnumeric() method returns True if all chars in a string are numeric chars, otherwise False
s='12343'
print(s.isnumeric()) #output: True

#The find() method returns the index of first occurrence of the substring (if found). If not found, it returns -1.
# check the index of 'fun'
print(message.find('fun')) # Output: 12

#The isalnum() method returns True if all characters in the string are alphanumeric (either alphabets or numbers). If not, it returns False.

name = "M3onica Gell22er "
print(name.isalnum()) # Output : False

#The isalpha() method returns True if all characters in the string are alphabets. If not, it returns False
name = "Monica"
print(name.isalpha()) #output true

#other imp functions
string.strip([chars]) #The strip() method returns a copy of the string by removing both the leading and the trailing characters (based on the string argument passed).
string = string.upper() #he upper() method converts all lowercase characters in a string into uppercase characters and returns it.
string = string.lower() #The lower() method converts all uppercase characters in a string into lowercase characters and returns it.
string.islower()
string.isdigit()
string.isupper()
```

#### Common Problems
Counting Characters
- hash table/map
- space complexity is O(1) not O(n)!
	- upper bound is range of chars! 26!
String of Unique chars
- determine which chars are in string of chars
- use 26 bit bitmask 
``` python
mask = 0
for c in word:
	mask |= (1 << (ord(c) - ord('a)))
```
Anagram
- sort both strings - should produce same resulting string
	- O(lnlog(n)) time and space
- match each char to prime number and multiply all mapped nums together - anagrams should have same multiple
	- O(n) time, O(1) space
- Frequency count of chars
	- O(n) time, O(1) space
Palindrome
- Reverse string should equal itself
- 2 ptrs at start and end of string
- Count num of palindromes
	- 2 ptrs moving outward away from middle
	- for each middle pivot, check 2 times, once including char once excluding (aba vs abba)