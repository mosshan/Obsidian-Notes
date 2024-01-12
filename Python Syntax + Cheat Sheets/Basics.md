### Built-in or Library Functions
##### functs to iterate over list/ other iterable (tuple, dictionaries)
```
** map(fun, iter) **
#fun : It is a  transformation function to which map passes each element of given iterable.
#iter : It is a iterable which is to be mapped.
# Defining a function
def mul(i):
    return i * i

# Using the map function
x = map(mul, (3, 5, 7, 11, 13))

print (x) # output: <map object at fjdoifjo>
print(list(x)) # output: [9, 25, 29, 121, 169]

** zip(list,list) **
for elem1,elem2 in zip(firstList,secondList):
	# will merge both lists and produce tuples with both elements
	# Tuples will stop at shortest list (in case of both lists having different len)
#Example
'''
a = ("John", "Charles", "Mike")
b = ("Jenny", "Christy", "Monica")

x = zip(a, b)

#use the tuple() function to display a readable version of the result:

print(tuple(x))
o/p: (('John', 'Jenny'), ('Charles', 'Christy'), ('Mike', 'Monica'))
'''

** any(list) ** [ OPPOSITE IS => ** all() ** ]
any(someList) # returns true if ANY element in list is true [any string, all numbers except 0 also count as true]

** enumerate(list|tuple) ** 
# [when you need to attach indexes to lists or tuples ]
enumerate(anyList) # ['a','b','c'] => [(0, 'a'), (1, 'b'), (2, 'c')]

** filter(function|list) **
filter(myFunction,list) # returns list with elements that returned true when passed in function

***************** import bisect ***********************

** bisect.bisect(list,number,begin,end) ** O(log(n))
# [ returns the index where the element should be inserted 
#		such that sorting order is maintained ]
a = [1,2,4]
bisect.bisect(a,3,0,4) # [1,2,4] => 2 coz '3' should be inserted in 2nd index to maintain sorting order

# Other variants of this functions are => bisect.bisect_left() | bisect.bisect_right()
# they have same arguments. Suppose the element we want to insert is already present
# in the sorting list, the bisect_left() will return index left of the existing number
# and the bisect_right() or bisect() will return index right to the existing number

# ** bisect.insort(list,number,begin,end)       ** O(n) to insert
# ** bisect.insort_right(list,number,begin,end) ** 
# ** bisect.insort_left(list,number,begin,end)  ** 

The above 3 functions are exact same of bisect.bisect(), the only difference
is that they return the sorted list after inserting and not the index. The
left() right() logic is also same as above.
```
##### Getting the ASCII val of a char
```
** ord(str) **
# returns ascii value of the character , Example ord("a") = 97
** chr(int) ** 
#return character of given ascii value , Example chr(97) = "a"
```

### Make a Class in python
https://runestone.academy/ns/books/published/pythonds/Introduction/ObjectOrientedProgramminginPythonDefiningClasses.html

``` python
class Fraction:
	def __init__(self, top, bottom):
		self.num = top
		self.den = bottom
		
	def show(self):
		print(self.num, "/", self.den)

	#allows print(myfraction) to operate as we want vs print memory address of myfraction
	# overriding standard method that all classes in python have
	# default is return instance address string, but we want it to be able to print
	def __str__(self):
		return str(self.num, "/", self.den)

myfraction = Fraction(3,5)
myfraction.show() # 3/5
print(myfraction) # 3/5
```









``` python
class MinStack():

    def __init__(self, randomVal):
        self.stack = [(None, float('inf'))]
        self.randomVal = randomVal
    
    def push(self, val):
	    print(self.randomVal)
        currMin = self.stack[-1][1]
        if val < currMin:
            self.stack.append((val, val))
        else:
            self.stack.append((val, currMin))

    def pop(self):
        self.stack.pop()

    def top(self):
        return self.stack[-1][0]
    
    def getMin(self):
        return self.stack[-1][1]
```

### Math
##### Max and Min int
- float('inf') and float('-inf')
##### Summation
 - Summation of values from o to n : n( n+ 1) / 2
##### Bitwise Manipulation
- XOR 
	- Exclusive or
	- outputs 1 when either of the operands is 1 but both are not 1 and both are not 0
	- any number xored with itself = 0
	- communitive
		- 4 xor 1 xor 1 xor 4 = 0 bc 4 xor 4 = 0 and 1 xor 1 = 0 
		- 4 xor 1 xor 1 xor 4 xor 3 = 3  bc 4 xor 4 = 0 and 1 xor 1 = 0 but 3 xor 0 = 3
	- order doesnt matter 
		- 4 xor 1 xor 3 == 3 xor 1 xor 4
```
xor_num = num1 ^ num2
```
##### Modulo
- % in python
- 4 % 2 == 0
- check if odd:
	- n % 2 == 1 -> odd
	- n % 2 == 0 -> even
### Data Types
![Untitled](https://user-images.githubusercontent.com/47276307/172329842-38f3de07-62d9-4d7d-9a19-fc576ee396a9.jpg)

- Operators and their precedence
![Untitled](https://user-images.githubusercontent.com/47276307/172329850-61fc0809-a4b0-416c-848b-1c502ecb4772.jpg)


### Random

#### Object Oriented Programming
- Inheritance - ability for one class to be related to other class 
	- child classes can inherit characteristic data + behavior from parent class
	- child class = subclass, parent = superclass
	- inheritence heirarchy
		- ![[Pasted image 20240110154304.png]]
- why is organization of classes helpful?
	- ie in inheritance
	- allow previously written code to be extended to meet needs of new situation
- A class constructor should always invoke the constructor of its parent before continuing on with its own data and behavior.
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

#### How to access last element of array?
	- array = [peas, pears, plums]
	- array[-1] = plums
