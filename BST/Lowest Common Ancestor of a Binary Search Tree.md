#  Lowest Common Ancestor of a Binary Search Tree

### 原题： https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

Given binary search tree:  root = [6,2,8,0,4,7,9,null,null,3,5]


 

Example 1:

Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
Example 2:

Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
 

Constraints:

All of the nodes' values will be unique.
p and q are different and both values will exist in the BST.

利用BST性质:
1. Left subtree of a node N contains nodes whose values are lesser than or equal to node N's value.
2. Right subtree of a node N contains nodes whose values are greater than node N's value.
3. Both left and right subtrees are also BSTs.

##解 记递推
```c# 
public class Solution {
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        while(root!=null){
            if(p.val > root.val && q.val > root.val){
                root = root.right;
            }
            else if(p.val < root.val && q.val < root.val){
                root = root.left;
            }
            else{
                return root;
            }
        }
        return null;
    }
}
```


```c# 
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */

public class Solution {
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(p.val > root.val && q.val > root.val){
            return LowestCommonAncestor(root.right, p ,q);
        }
        else if(p.val < root.val && q.val < root.val){
            return LowestCommonAncestor(root.left, p ,q);
        }
        else{
            return root;
        }
        
    }
    

}
```


