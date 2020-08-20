# Min Stack

### 原题： https://www.lintcode.com/problem/min-stack

Implement a stack with following functions:

push(val) push val into the stack
pop() pop the top element and return it
min() return the smallest number in the stack
All above should be in O(1) cost.

## 解
必须用额外一个stack来保存min value
与原本stack结构同步更新

**注意可以用python中array，也有pop（）**

```python
class MinStack:
    
    def __init__(self):
        # do intialization if necessary
        self.stack = []
        self.minStack = []
    """
    @param: number: An integer
    @return: nothing
    """
    def push(self, number):
        # write your code here
        self.stack.append(number)
        if( not self.minStack) or (number < self.minStack[-1]):
            self.minStack.append(number)
        else:
            self.minStack.append(self.minStack[-1])

    """
    @return: An integer
    """
    def pop(self):
        # write your code here
        self.minStack.pop()
        return self.stack.pop()
    """
    @return: An integer
    """
    def min(self):
        # write your code here
        return self.minStack[-1]

```
