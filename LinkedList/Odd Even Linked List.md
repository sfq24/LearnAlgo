# Odd Even Linked List

### 原题： https://leetcode.com/problems/odd-even-linked-list/

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

Example 1:

Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
Example 2:

Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
 

画图明确解法，再实现。基本情况就是用一个odd指针，一个even指针向前进位，形成两个list，用另外一个list node存evenhead。最后把evenhead连到odd末尾

核心点在于：
1. corner case  []


## 解 

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
    public ListNode OddEvenList(ListNode head) {
        if(head == null) return null;
        ListNode evenhead;
        ListNode odd, even;
        
        odd = head;
        even = head.next;
        evenhead = even;
        
        while(even != null && even.next != null){
            odd.next = even.next;
            odd = odd.next;
            
            even.next = odd.next;
            even = even.next;

        }
        
        odd.next = evenhead;
        
        return head;
    }
}

```

