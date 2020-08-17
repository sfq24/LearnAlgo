# Swap Nodes in Pairs


### 原题： https://leetcode.com/problems/swap-nodes-in-pairs/

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.

 

Example:

Given 1->2->3->4, you should return the list as 2->1->4->3.


三个指针pre, curr, post倒换

核心点在于：
1. 终止条件：
2. 由于几个指针错位，需要画图搞明白变换之后哪个指针是哪个
3. 由于条件判断，需要dummy node进行第一次进入循环时迭代，也存住head最后返回


## 解1
```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode SwapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode dummy = new ListNode(0,head);
        ListNode pre = dummy;
        ListNode curr = dummy;
        ListNode post = dummy;
        
        while(curr.next != null && curr.next.next != null){
            //move forward                                         //先移动，否则最后一次循环会退出
            pre = curr;
            curr = curr.next;
            post = curr.next;
            //Console.WriteLine("test");
            
            pre.next = post;
            curr.next = post.next;
            post.next = curr;
            

        }
        
        return dummy.next;
    }
}

```

### 另解 递归 （最优）：


```c#
public class Solution {
    public ListNode SwapPairs(ListNode head) {
        if(head == null || head.next == null) return head;
        
        ListNode last = head.next;
        head.next = SwapPairs(last.next);
        last.next = head;
        
        return last;
    }
}

```
