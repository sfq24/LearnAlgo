#  Intersection of Two Linked Lists

### 原题： https://leetcode.com/problems/intersection-of-two-linked-lists/

考虑快慢指针
参考动画： https://github.com/MisterBooo/LeetCodeAnimation/blob/master/0160-Intersection-of-Two-Linked-Lists/Animation/Animation.gif

# 核心问题：
完全可以用nodeA = nodeB来做判断

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

## 解
数数
看哪一条更长，提前跑，跑到一样长的时候一起跑，直到A和B相等就返回

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) {
            return null;
        }

        int n = 0;
        ListNode dummyA = new ListNode(0), dummyB = new ListNode(0);
        dummyA.next = headA;
        dummyB.next = headB;

        while (headA.next != null) {
            headA = headA.next;
            n++;
        }
        while (headB.next != null) {
            headB = headB.next;
            n--;
        }

        if (headA != headB) {
            return null;
        }

        headA = dummyA.next;
        headB = dummyB.next;
        
        if (n > 0) { // A longer
            while (n > 0) {
                headA = headA.next;
                n--;
            }
        } else {
            while (n < 0) {
                headB = headB.next;
                n++;
            }
        }

        while (headA != headB) {
            headA = headA.next;
            headB = headB.next;
        }

        return headA;

    }
}
```


## 解： HashTable
待补充  
