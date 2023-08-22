#stack #problems #queue
## Minimum Stack
https://leetcode.com/problems/min-stack/
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class: -> constrained to O(1) for all Min Stack Operations

-   `MinStack()` initializes the stack object.
-   `void push(val)` pushes the element val onto the stack.
-   `void pop()` removes the element on the top of the stack.
-   `int top()` gets the top element of the stack.
-   `int getMin()` retrieves the minimum element in the stack
#### Understand
- ```
HAPPY CASE
Input: 
["MinStack","push","push","push","getMin","pop","top","getMin"]
[        [],   [3],   [2],   [1],      [],   [],   [],      []]
Output:
[      null,  null,  null,  null,       1, null,    2,       2]

MinStack minStack = new MinStack();
minStack.push(3);
minStack.push(2);
minStack.push(1);
minStack.getMin(); // return 1
minStack.pop();
minStack.top();    // return 2
minStack.getMin(); // return 2

HARDER CASE
Input: 
["MinStack","push","push","push","push","getMin","pop","top","getMin"]
[        [],   [1],  [-1],  [2],   [-8],      [],   [],   [],      []]
Output:
[      null,  null,  null, null,  null,       -8, null,    2,      -1]

MinStack minStack = new MinStack();
minStack.push(1);
minStack.push(-1);
minStack.push(2);
minStack.push(-8);
minStack.getMin(); // return -8
minStack.pop();
minStack.top();    // return 2
minStack.getMin(); // return -1

- clarifying:
	- can pop/top/getMin be called on an empty stack?
		- always on nonempty
	- should pop return something?
		- no just remove not return
	- does top also remove? 
		- no
#### Match
- min heap to help return smallest element - cant use min heap bc operations are not constant time
	- sorted array?
		- nope, sorting is not constant time
- stack for stack
	- Stack is LIFO
#### Plan
- store current minimum with each level pushed to stack
- when initializing min stack
	- list to represent stack - has built in functions which help a lot
	- each node has own value, next and curr min value
	- init 2 ptrs, one for head, one for end
- push
	- if item is smaller than current minimum from the end of the ll item change its curr min value to its own value
	- add item to end of linked list O(1)
- pop
	- remove head from linked list O(1)
- getMin 
	- return curmin value from item at end of linked list
- top
	- remove head and return its value
#### Implement
```python
class MinStack(object):
    def __init__(self):
        self.stack = [(None, float('inf'))]


    def push(self, val):
        """
        :type val: int
        :rtype: None
        """
        self.stack.append((val, min(self.stack[-1][1], val)))
            
    def pop(self):
        """
        :rtype: None
        """
        self.stack.pop()
        

    def top(self):
        """
        :rtype: int
        """
        return self.stack[-1][0]
        

    def getMin(self):
        """
        :rtype: int
        """
        return self.stack[-1][1]
        


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
#### Evaluate
- runtime: O(1) for all
- space: O(n )

## Implement Queue Using Stacks
https://leetcode.com/problems/implement-queue-using-stacks/
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

-   `void push(int x)` Pushes element x to the back of the queue.
-   `int pop()` Removes the element from the front of the queue and returns it.
-   `int peek()` Returns the element at the front of the queue.
-   `boolean empty()` Returns true if the queue is empty, false otherwise.

Notes:
-   You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
-   Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

**Examples:**

```
Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[       [],    [1],    [2],     [],    [],      []]
Output
[     null,   null,   null,      1,     1,   false]

Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

#### Understand
- clarifying
	- will pop and peek be performed on empty queue?
#### Match
- two stacks
#### Plan
- queue is FIFO stacks are LIFO
- move back and forth between stacks to turn lifo into fifo
	- higher runtime to do this for each operation
	- just move for pops
		- do i need to move for all pops?
			- no - only when queue holding elements organized in fifo order is empty
#### Implement
```python
class MyQueue(object):

    def __init__(self):
        self.lifoStack = []
        self.fifoStack = []

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.lifoStack.append(x)
        

    def pop(self):
        """
        :rtype: int
        """
        if len(self.fifoStack) == 0:
            while len(self.lifoStack) != 0:
                self.fifoStack.append(self.lifoStack.pop())
        return self.fifoStack.pop()
        

    def peek(self):
        """
        :rtype: int
        """
        if len(self.fifoStack) == 0:
            while len(self.lifoStack) != 0:
                self.fifoStack.append(self.lifoStack.pop())
        return self.fifoStack[-1]

        

    def empty(self):
        """
        :rtype: bool
        """
        if len(self.fifoStack) + len(self.lifoStack) == 0:
            return True
        return False

# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```
#### Review
	- want to get more comfy with the self in python
#### Evaluate
- space: O(n)
- runtime: O(1) for all queue operations, (**amortized** O(1) for pop() and peek())
	- we only move all els from 1 stack to other if stack is empty
	- so its like doing 1 op for each 

## Validate Stack Sequences
Given two integer arrays `pushed` and `popped` each with distinct values, return `true` if this could have been the result of a sequence of push and pop operations on an initially empty stack, or `false` otherwise.
**Examples:**

```
Input: pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
Output: true

Explanation: We might do the following sequence:
push(1), push(2), push(3), push(4),
pop() -> 4,
push(5),
pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

```python
class Solution(object):
    def validateStackSequences(self, pushed, popped):
        """
        :type pushed: List[int]
        :type popped: List[int]
        :rtype: bool

        Understand
        Match
            - can use a stack to replicate 
        Plan
            - check if we can pop
                - is top element on stack equal to next item in popped?
                    if not: push 
                    if yes: pop
                - if we reach end of pushed but cant pop, then false

        Review: MAKE EDGE CASES!!!
        Evaluate: 
            - space: O(n)
            - runtime: O(n) + O(n) = O(n)
        """
        stack = []
        popIndex, pushIndex = 0, 0
        while pushIndex < len(pushed):
            if len(stack) == 0:
                stack.append(pushed[pushIndex])
                pushIndex += 1
            else:
                top = stack[-1]
                if top == popped[popIndex]:
                    stack.pop()
                    popIndex += 1
                else:
                    stack.append(pushed[pushIndex])
                    pushIndex += 1

        while popIndex < len(popped):
            top = stack[-1]
            if top == popped[popIndex]:
                stack.pop()
                popIndex += 1
            else:
                return False

        return True
```



## Evaluate Reverse Polish Notation
~ essentially postfix notation
- number?
	- add to stack
- operator?
	- pop operand2 and operand1
	- find answer = operand1 operator operand2
	- push answer to stack
- use hashmap to map operands to operations?

## Sum of Subarray Minimums
https://leetcode.com/problems/sum-of-subarray-minimums/
Given an array of integers arr, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer **modulo** `10^9 + 7`.
#### Understand
- happy
	- input \[9, 2, 7]
	- output: 
		- 9 + 2 + 7 + 2 + 7 + 2 + 2 = 31
- edge
	- input: \[1]
	- output: 1
- clarifying
	- can values repeat in the arr
		- yes
	- can arr be empty - no
	- can values in arr be negative - no, but they can be very large
#### Match
- hashset
- stack - order does not matter
- queue - order does not matter
- heap - not grabbing k 
#### Plan
- Unoptimized:
	- find all subarrays
		-NOT  permutations of set
	- sum mins of each 
- Given input `A=[3,1,2,5,4]` we can cycle through array and write out all subarrays **ending** with i-th element.

```python
[3]
[3,1], [1]
[3,1,2], [1,2], [2]
[3,1,2,5], [1,2,5], [2,5], [5]
[3,1,2,5,4], [1,2,5,4], [2,5,4], [5,4], [4]
```
- denote sum of min values of those subarrays with result\[i]
	3
	1 + 1
	1 + 1 + 2
	1 + 1 + 2 + 5
	1 + 1 + 2 + 4 + 5
- if A\[i - 1] <= A\[i] then result\[i] = result\[i - 1] + A\[i]
- subarrays ending with ith value are basically same subarrays for i-1th value with extra element A\[i] added to each 1 and then extra subarray consisting of just A\[i]. Adding bigger or same value to subarrays doesnt change minimum. 
- Generalize:
	- if we find previous less or equal value A\[j] <= A\[i] (j < i) then result\[i] = result\[j] + A\[i] * (i - j)
	- How?
		- Let's consider our previous example to see why. Let's take `i=4` and look at subarrays for the element `A[i]=4`:  
			`[3,1,2,5,4], [1,2,5,4], [2,5,4], [5,4], [4]`

		- First part of these subarrays look similar to subarrays generated previous less value `2` at `j=2` as if we took those subarrays (`[3,1,2], [1,2], [2]`) and added elements `[5,4]` to each of them. Sum of those subarrays equals `result[j]`.

		- The rest of our i-th subarrays consist of elements after `j` and up to `i`: `[5,4], [4]` . They are not less then our element `4` so their sum equals to `(i-j)*A[i]`

		- Together these two observations give us formula `result[i] = result[j] + A[i]*(i-j)`
- want to build monotonously increasing / (nondecreasing) stack
	- find the previous less or equal value and reuse sum


## Basic Calc
https://leetcode.com/problems/basic-calculator/
Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, non-negative integers and empty spaces .

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

**Examples:**

```
Input: s = "1 + 1"
Output: 2

Input: s = " 2-1 + 2 "
Output: 3

Input: s = "(1+(4+5+2)-3)+(6+8)"
Output: 23
```
#### Understand
- edge case:
	- input: -(2+ -3) -> unsure if this is valid vs -(2 + (-3))
	- output: 1
	- input: 1
	- output:1
- happy case:
	- input: 2 - 3 + 1
	- output: 0
- expression must be valid - dont need to worry abt error checking
- will there be negative numbers?
	- yes, - can be used as a unary operation (ie we could have -1)
- will there be floats
	- just ints
- which operators?
	- ( ) + - 
#### Match
- stacks + queues
#### Plan
- equations are given to us in infix
	- since just + and - left to right order of operations doesn't matter
	- WRONG
- 2 stacks, one w #, one w operators + parentheses
- while things are left in equation:
	- if num, put on num stack
	- if operator  or ( put on op stack
	- if ) 
		- while operation pop isn't (:
			- pop 2 nums, operand2 and operand1
			- complete operation and put answer on stack
- if nothing left in equation and operator stack isnt empty
	- pop 1 num
		- see if num stack is empty
		- if not:
			- pop 2nd num and an op
		- if so: we have a unary - operator 
			- pop operator
			- answer is - num popped
	- put answer onto num stack
- return answer from top of num stack

Plan2
- solve first if no parenthesis
	- have operand, result, sign = 0, 0, positive
	- if we hit a number, just save it in our operand, don't do anything with it until we hit a + or 1
		- need to deal w multiple digits in number
			- while our char is a digit, multiply the current operand by 10 and then add the digit
				- if we had 121, we'd read it in as operand = 1, then operand = 1 * 10 + 2 = 12, then operand = 12 * 10  + 1 = 121
	- if + or -:
		- add or subtract operand from the current result - based on current sign
		- change sign to be pos if + and negative if - 
	
- if have parenthesis, add stack to deal with it as if it were recursive
	- stack holds 
	- if (:
		- add result and sign to stack 
		- reset result and sign to 0 and pos and operand to 0
	- if ):
		- complete current operation w operand
		- pop sign from stack and mult by result
		- add prev result to current result
#### Implement
```python
class Solution(object):
    def calculate(self, s):
        """
        :type s: str
        :rtype: int
        """
        result = 0
        sign = 1 # sign starts at positive, we have not hit a neg operator yet
        operand = 0
        stack = [] # want to be able to treat parenthesis in recursive manner

        for char in s:
            if char.isdigit():
                operand = (operand * 10) + int(char)
            elif char == '-':
                result = result + (sign * operand)
                sign, operand = -1, 0
            elif char == '+':
                result = result + (sign * operand)
                sign, operand = 1, 0
            elif char == '(':
                stack.append(result)
                stack.append(sign)
                
                result, sign = 0, 1
            # cant make this an else bc we have ' ' in the equation
            elif char == ')':
                result = result + (sign * operand)
                #multiply by sign which came before parenthesis
                result = result * stack.pop()
                # add previous result to current result
                result = result + stack.pop()
                operand = 0

        result = result + (sign * operand)
        return result

```
#### Review
- turns out left to right rly does matter lol
- and need to deal with ints greater than 10 too
- as go, mark down considerations to make sure to implement in code
	- ie, equation has spaces, digit can be multiple chars long
#### Evaluate
- space: O(n)
- runtime: O(n)

## Asteroid Collision
https://leetcode.com/problems/asteroid-collision/
We are given an array `asteroids` of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Examples:**

```
Input: asteroids = [5,10,-5]
Output: [5,10]
Explanation: The 10 and -5 collide resulting in 10. The 5 and 10 never collide.

Input: asteroids = [8,-8]
Output: []
Explanation: The 8 and -8 collide exploding each other.
```
#### Understand
	- any asteroids with opposite signs will collide - with one next to them
	- can we have odd numbers of asteroids? yes
	- cant be empty
	- will they continue colliding? yes
	- will they only collide in pairs? no
	- edge:
		- input = 10, 2, -5
		- output = 10
			- 2 hits -5 = 10, -5 then 10 hits -5 leaving 10
		- input = -4, 4, -5, 10, -15
		- output: -15
	- happy:
		- input: -2, -2
		- output: -2, -2
		- input: 5, 10, -5, -2
		- output: 5, 10
#### Match
- order matters so use a stack?
#### Plan
- will collide if asteroid moving right hits asteroid moving left
- if start w asteroid moving left, has nothing to hit
- if asteroid moving right
	- put in stack
- if asteroid moving left:
	- while stack isnt empty and stack top is moving right and stack top < asteroid
		- pop
	- if stack isnt empty and stack top is moving right and stack top == asteroid
		- pop
	- else if  not stack or stack top is moving left too
		- append asteroid
#### Implement
```python
class Solution(object):
    def asteroidCollision(self, asteroids):
        """
        :type asteroids: List[int]
        :rtype: List[int]
        """
        stack = []
        for asteroid in asteroids:
            if asteroid > 0:
                stack.append(asteroid)
            else:
                while stack and stack[-1] > 0 and stack[-1] < -asteroid:
                    stack.pop()
                if stack and stack[-1] > 0 and stack[-1] == -asteroid:
                    stack.pop()
                elif not stack or stack[-1] < 0:
                    stack.append(asteroid)
        return stack

```
#### Review
- go through logic better
#### Evaluate
space: O(n)
runtime: O(n)