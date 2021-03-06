# Binary Tree Preorder Traversal

### 原题： https://leetcode.com/problems/binary-tree-preorder-traversal/

Given a binary tree, return the preorder traversal of its nodes' values.

Example:

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]

**这种题能不用递归就不用递归**

## 解（循环）

画图研究过程
![anim](https://github.com/MisterBooo/LeetCodeAnimation/blob/master/0144-Binary-Tree-Preorder-Traversal/Animation/Animation.gif)

```c#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public IList<int> PreorderTraversal(TreeNode root) {
        List<int> res = new List<int>();
        if(root == null) return res;
        
        Stack<TreeNode> s = new Stack<TreeNode>();
        s.Push(root);
        while (s.Count>0) {
            TreeNode node = s.Pop();
            res.Add(node.val);
            if (node.right != null) s.Push(node.right);
            if (node.left != null) s.Push(node.left);
        }

        
        return res;
    }
}

```


## 解
递归

```c#
public class Solution {
    public IList<int> PreorderTraversal(TreeNode root) {
        List<int> res = new List<int>();
        
        if(root != null){
            res.Add(root.val);
        }
        else{
            return res;
        }
        if(root.left != null){
            foreach(var val in PreorderTraversal(root.left)){
                res.Add(val);
            }
        }
        if(root.right != null){
            foreach(var val in PreorderTraversal(root.right)){
                res.Add(val);
            }
        }
        
        return res;
        
    }
}

```
