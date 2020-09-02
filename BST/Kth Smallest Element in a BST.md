# Kth Smallest Element in a BST

### 原题： https://leetcode.com/problems/kth-smallest-element-in-a-bst/

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Example 1:

Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
Example 2:

Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

 

Constraints:

The number of elements of the BST is between 1 to 10^4.
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.



## 解1：
中序遍历，得到的是按序排的序列。其中k-1个元素就是第k小的

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
    public int KthSmallest(TreeNode root, int k) {
        List<int> res = new List<int>();
        
        res = InOrderList(root, res);
        return res[k-1];
    }
    
    public List<int> InOrderList(TreeNode root, List<int> list){
        if(root == null) return list;

        InOrderList(root.left, list);          //理解此处
        list.Add(root.val);
        InOrderList(root.right, list);
        
        return list;
    }
}
```


## 解： 迭代 （需要记住）
```c#  

public class Solution {
    public int KthSmallest(TreeNode root, int k) {
        Stack<TreeNode> s = new Stack<TreeNode>();
        
        while(true){
            while(root != null){
                s.Push(root);
                root = root.left;
            }
            root = s.Pop();
            
            if(--k == 0) return root.val;
            root = root.right;
            
        }

    }
}
```

