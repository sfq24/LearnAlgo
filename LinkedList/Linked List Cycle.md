# Linked List Cycle

### 原题： https://leetcode.com/problems/linked-list-cycle/

快慢指针的典型题

核心点在于：
1. 定义快慢指针，快的步长为2
2. 确定好终止条件


## 解
思考的时候考虑有cycle，fast将要追到slow的情况。 fast会在 slowMove = false的情况下追到slow
```c#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public bool HasCycle(ListNode head) {
        if(head == null || head.next ==null){
            return false;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        bool slowMove = false;
        while(fast != null){
            if(fast.next == null){
                return false;
            }
            if(fast.next == slow){
                return true;
            }
            if(slowMove){
                slow = slow.next;
                fast = fast.next;
                slowMove = false;
            }
            else{
                fast = fast.next;
                slowMove = true;
            }
        }
        return false;
    }
}

```


## 解： HashTable
待补充  