#referenceguide #hashtables #stringsarrays #heaps #math

# Useful Libraries and Functions for Data Structs
## For Strings and Arrays
#### Find Length
len(str)
	- calls method _ _ len__ ()
	- acts as a counter which is automatically incremented as data is defined/stored
		- makes it run in O(1)
	Runtime:
		O(1)

#### Access last index in string?
len(string)
endchar is index at len(string) - 1

#### Iteration - some options
```python
#option 1
for char in str:
	print(char)

#option 2, using range()
for index in range(0, len(str)):
	print(str[index])
```
- Option 1
	- runtime: O(n), where n is length of string
	- auxiliary space: O(1)
- Option 2: 
	- runtime: O(n), where n is length of string
	- auxiliary space: O(1)


#### Check if char/ string is alphanumeric
- isalnum(char) or isalnum(str)
- returns true / false

### Check if char/ string is alphabetic 
- char.isalpha() or str.isalpha()

### Convert to lowercase
- lower(str)
## For Hash Sets/ Tables
#### Collections Library - defaultdict
- supports some additional functions as long as usual dict functions
```python

import collections
# for non count key value pairs
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = defaultdict(list)

# if key is encountered for first time, not already in mapping
# entry is automatically created and then item is appended
for k, v in s:
    d[k].append(v)

sorted(d.items())
[('blue', [2, 4]), ('red', [1]), ('yellow', [1, 3])]

# create dictionary holding count of items
countDict = collections.defaultdict(int)
# add item
# if item doesnt exist, will input it with value = 0 then will update it as instructed
for key in listofkeyvalpairs:
	countDict[key] += 1
```
#### Dictionaries
##### Create Dictionaries
```python
emptyDict = {}
dictWithItems = {
	"brand" ="Ford",
	"model" = "Mustang",
	"year" = 1964
}
```
##### Add Items to Dictionaries
```python
# add an item
thisDict["key"] = "value"

# update dictionary - if item does not exist it will be added
thisDict.update({"color":"red"})
```
##### Python - Access Dictionary Items
```python
# dictionary = {key -> value , key2, value2, ...}
thisDict = {
	"brand" ="Ford",
	"model" = "Mustang",
	"year" = 1964
}
# get value of key
x = thisDict["model"]
# or
x = thisDict.get("model")

# get list of all keys in the dictionary
keyList = thisDict.keys()

# get list of all values in the dictionary
valList = thisDict.values()

# get list of key : value pairs
pairList = thisDict.items()

# check if key exists
if "model" in thisDict:
	print("yeehaw, 'model' is one of the keys in thisdict dictionary")
## Dictionaries
# Create Dictionaries
```python
emptyDict = {}
dictWithItems = {
	"brand" ="Ford",
	"model" = "Mustang",
	"year" = 1964
}
```

## For Heaps
#### Heapq Library
```python
import heapq
newDict = {
	"hey" = 1, 
	"there" = 2, 
	"the" = 2
}

# make min heap, sorted first by value, then by key
heapq.heapify(newDict)

# need max Heap?? create different type of dict
# for example, storing frequency of words and want most frequent?
# store counts as negative values
newDict = {
	"hey" = -1, 
	"there" = -2, 
	"the" = -2
}

```
# For Math
### Remainder of division
- % is modulo
- k % i = the remainder of k / i
- want it in integer form?
	- int(k % i)

### Convert value into an integer
int(object)
# Other
#### Can I use parenthesis in if statements?
	- yes! but usually unneeded - they just force an order of operations

#### Not equal
- !=

#### Assign multiple values at once using 1 line
```python
var1, var2 = 1, 2
```

	- var1 now == 1 and var2 == 2'=

#### Increment/Decrement Var 
	- By 1 : -- or ++
	- By other vals: var += 1 , var -= 1 ** Use this option to be safe btwn different versions of python

#### Range
range starts from 0 by default

#### Quick Tips
- using a function on object: 
	- object.function()
	- ex: string.isalpha()
- accessing built in characteristic
	- function(object)
	- ex: len(string)

### How to access last element of array?
	- array = [peas, pears, plums]
	- array[-1] = plums

