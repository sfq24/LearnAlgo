# SubTree 

### 原题： http://www.lintcode.com/en/problem/subtree/

You have two every large binary trees: T1,
with millions of nodes, and T2, with hundreds of nodes.
Create an algorithm to decide if T2 is a subtree of T1.

Example
T2 is a subtree of T1 in the following case:
       1                3
      / \              /
T1 = 2   3      T2 =  4
        /
       4
T2 isn't a subtree of T1 in the following case:
       1               3
      / \               \
T1 = 2   3       T2 =    4
        /
       4
Note
A tree T2 is a subtree of T1 if there exists a node n in T1 such that
the subtree of n is identical to T2.
That is, if you cut off the tree at node n,
the two trees would be identical.


需要写单独的判断是否identical的函数，之后都用递归。
一些条件判断比较tricky，需要记一下

```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param T1: The roots of binary tree T1.
    @param T2: The roots of binary tree T2.
    @return: True if T2 is a subtree of T1, or false.
    """
    def isSubtree(self, T1, T2):
        if(T2 == None):
            return True
        if(T1 == None):
            return False
            
        return self.isIdentical(T1,T2) or self.isSubtree(T1.left,T2) or self.isSubtree(T1.right, T2)

    def isIdentical(self, T1, T2):
        if(T1 == None) and (T2 == None):
            return True
        if(T1 == None) or (T2 == None):
            return False
        
        if(T1.val != T2.val):
            return False
            
        return self.isIdentical(T1.left, T2.left) and self.isIdentical(T1.right,T2.right)


```

