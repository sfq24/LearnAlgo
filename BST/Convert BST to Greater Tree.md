# Trim a Binary Search Tree

### 原题： https://leetcode.com/problems/convert-bst-to-greater-tree/

Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

Example:

Input: The root of a Binary Search Tree like this:
              5
            /   \
           2     13

Output: The root of a Greater Tree like this:
             18
            /   \
          20     13


最直观解法还是递归。 效率也还可以，跟stack解法一样。

## 解 递归
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
    private int sum = 0;
    public TreeNode ConvertBST(TreeNode root) {
        if(root == null) return root;
        root.right = ConvertBST(root.right);
        sum += root.val;
        root.val = sum;
        root.left = ConvertBST(root.left);
        
        return root;
    }
}
```


## 解 iteration 用stack，更优
```c# 
public class Solution {

    public TreeNode ConvertBST(TreeNode root) {
        int sum = 0;
        TreeNode res = root;
        Stack<TreeNode> s = new Stack<TreeNode>();
        
        while(s.Count != 0 || root != null){
            while(root != null){
                s.Push(root);
                root = root.right;
            }
            
            var node = s.Pop();
            sum += node.val;
            node.val = sum;
            
            root = node.left;
            
        }
        
        return res;
    }
}

```
