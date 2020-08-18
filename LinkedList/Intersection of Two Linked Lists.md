#  Intersection of Two Linked Lists

### 原题： https://leetcode.com/problems/intersection-of-two-linked-lists/

考虑快慢指针
参考动画： https://github.com/MisterBooo/LeetCodeAnimation/blob/master/0160-Intersection-of-Two-Linked-Lists/Animation/Animation.gif


## 解
不一定哪一个list短，所以两边循环追赶
```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode GetIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null) return null;
        
        ListNode Ahead = headA;
        ListNode Bhead = headB;
        
        while(Ahead != Bhead){
            if(Ahead == null){
                Ahead = headB;
            }
            else{
                Ahead = Ahead.next;
            }
            if(Bhead == null){
                Bhead = headA;
            }
            else{
                Bhead = Bhead.next;
            }
        }
        return Ahead;
    }
}

```


## 解： HashTable
待补充  
