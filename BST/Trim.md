# Trim a Binary Search Tree

### 原题： https://leetcode.com/problems/trim-a-binary-search-tree/

Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in [L, R] (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.



直接递归（分治？）

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
    public TreeNode TrimBST(TreeNode root, int L, int R) {
        if(root == null) return root;
        if(root.val < L) return TrimBST(root.right, L, R);
        if(root.val > R) return TrimBST(root.left, L, R);
        
        root.left = TrimBST(root.left, L, R);
        root.right = TrimBST(root.right, L, R);
        
        return root;
    }
}
```


