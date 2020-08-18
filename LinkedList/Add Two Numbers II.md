# Add Two Numbers II

### 原题： https://leetcode.com/problems/add-two-numbers-ii/

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:

Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7

最粗暴是reverse，算完和，再reverse
本质上可以考虑利用stack结构

核心点在于：
1. c# Stack类型用法
2. corner case


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
    public ListNode AddTwoNumbers(ListNode l1, ListNode l2) {
        Stack<int> s1 = new Stack<int>();
        Stack<int> s2 = new Stack<int>();
        while(l1 != null){
            s1.Push(l1.val);
            l1 = l1.next;
        }
        while(l2 != null){
            s2.Push(l2.val);
            l2 = l2.next;
        }
        
        int flag = 0;
        
        ListNode result = null;
        while(s1.Count > 0 && s2.Count > 0){
            int sum = s1.Pop() + s2.Pop() + flag;
            flag = sum / 10;
            sum %= 10;
            result = new ListNode(sum, result);
        }
        
        Stack<int> remain = s1.Count > 0 ? s1 : s2;
        
        while(remain.Count>0){
            int sum = remain.Pop();
            if(flag > 0){
                sum++;
                if(sum > 9){
                    sum = 0;
                    flag = 1;
                }
                else{
                    flag = 0;
                }
            }
            result = new ListNode(sum, result);
        }
        
        if(flag > 0){
            result = new ListNode(1, result);
        }
        
        return result;
    }
}

```

