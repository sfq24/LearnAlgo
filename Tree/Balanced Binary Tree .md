# Balanced Binary Tree 

### 原题： https://www.lintcode.com/problem/balanced-binary-tree/

给定一个二叉树,确定它是高度平衡的。对于这个问题,一棵高度平衡的二叉树的定义是：一棵二叉树中每个节点的两个子树的深度相差不会超过1。 

只能递归做

注意python中语法

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
    @param root: The root of binary tree.
    @return: True if this Binary tree is Balanced, or false.
    """
    result = True
    
    def MaxDepth(self, root):
        if(root==None): return 0
        
        l = self.MaxDepth(root.left)
        r = self.MaxDepth(root.right)
        if(abs(l - r) > 1):
            self.result = False
            return -1
        return 1 + max(l,r)
        
    def isBalanced(self, root):
        # write your code here
        if(self.MaxDepth(root) == -1):
            self.result = False
        return self.result


```

