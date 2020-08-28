# Construct Binary Tree from Preorder and Inorder Traversal

### 原题： https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/

Given preorder and inorder traversal of a tree, construct the binary tree.

Example
Given in-order [1,2,3] and pre-order [2,1,3], return a tree:
  2
 / \
1   3
Note
You may assume that duplicates do not exist in the tree.

## 解 递归
典型题，但比较难
tricky part是设置好递归的参数
preorder tree作用是找root， inorder作用是找left和right。

找到root在inorder中的index，用此来隔离区分左边树和右边树

在preorder tree中，root的下一个元素一定是左边node。但跳到右边node需要跳过所有的left tree分支（index-instart）。再向右一个就是right node


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
    public TreeNode BuildTree(int[] preorder, int[] inorder) {
        return Helper(preorder, 0, inorder, 0, inorder.Length -1);
    }
    
    private TreeNode Helper(int[] preorder, int prestart, int[] inorder, int instart, int inend){
        if(prestart > preorder.Length-1 || instart > inend) return null;    //终止条件
        
        TreeNode root = new TreeNode(preorder[prestart]);
        
        int index = instart;
        for(; index < inend; index++){
            if(inorder[index] == root.val){
                break;
            }
        }
        
        //关键点
        root.left = Helper(preorder, prestart+1, inorder, instart, index -1);
        root.right = Helper(preorder, prestart + index - instart +1, inorder, index + 1, inend);
        
        return root;
    }
}

```

