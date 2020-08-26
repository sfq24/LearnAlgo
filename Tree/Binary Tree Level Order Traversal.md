# Binary Tree Level Order Traversal
### 原题： https://www.lintcode.com/problem/binary-tree-level-order-traversal

Given a binary tree, return the level order traversal of its nodes' values.
(ie, from left to right, level by level).

Example
Given binary tree {3,9,20,#,#,15,7},

    3
   / \
  9  20
    /  \
   15   7

return its level order traversal as:

[
  [3],
  [9,20],
  [15,7]
]
Challenge
Using only 1 queue to implement it.


**注意python中强行用arrary代表queue**

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
    @param root: A Tree
    @return: Level order a list of lists of integer
    """
    def levelOrder(self, root):
        res = []
        queue = []
        if(root == None):
            return res
        
        queue.append(root)
        
        while(len(queue) > 0):
            count = len(queue)
            level = []
            for i in range (0,count):
                node = queue.pop(0)
                level.append(node.val)
                if(node.left):
                    queue.append(node.left)
                if(node.right):
                    queue.append(node.right)
            
            res.append(level)
            
        return res
        

```

