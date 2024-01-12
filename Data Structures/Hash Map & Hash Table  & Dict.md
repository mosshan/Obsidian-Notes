#### HashMap / HashTable
- use when need to store key-val pairs and efficiently retrieve values based on their keys
	- when you add the same key, it changes vkey- value pair
	- track frequencies, counts, or occurences of elements in arrray or list
- use a dictionary



#### Dictionary
Used to store data values in key:value pairs
![[Pasted image 20240110152445.png]]
- Operations time complexities
	- Avg case times for dict objects assume hash function is sufficiently robust to make collisions uncommon. Also assumes keys used in params are selected uniformly at random from the set of all keys
	- ![[Pasted image 20240109120601.png]]
```python
dict = {'a':1, 'b':2, 'c':3}

dict.keys() # returns list of keys of dictionary
dict.values() # returns list of values of dictionary
dict.get('a') # returns values for any corresponding key
# or
dict['a'} # but this option can give indexerrors
dict.items() # returns [('a',1),('b',2),('c',3)]
# NOTE : items() Returns view object that will be updated with any future changes to dict
dict.copy() # returns copy of the dictionary
dict.pop(KEY) # pops key-value pair associated with that key
dict.popItem() # removes most recent pair added
dict.setDefault(KEY, DEFAULT_VALUE) # returns value of key if key exists, else default value returned
# if the key doesnt exist, DEFAULT_VALUE becomes the key's value. 2nd argument's default is None. 
dict.update({KEY:VALUE}) #inserts pair in dictionary if not present, if present, corresponding value is overridden 
```
