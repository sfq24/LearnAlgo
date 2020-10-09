# merge-k-sorted-lists

### 原题： https://leetcode.com/problems/merge-k-sorted-lists/
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

 

Example 1:

Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
Example 2:

Input: lists = []
Output: []
Example 3:

Input: lists = [[]]
Output: []


好多种解法

# 解：
循环
注意如果用foreach（list in lists）则不能改变list，所以需要用index来循环
**必须记住此处处理head的方法**： 先初始化一个head，续新node时用head.next = new ListNode(val); head = head.next;
否则可能会多个尾巴

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
    public ListNode MergeKLists(ListNode[] lists) {
        ListNode head = new ListNode(0);
        ListNode res = new ListNode(0, head);
        
        ListNode curr = new ListNode(int.MaxValue);
        
        while(curr != null){
            curr = null;
            int temp = -1;
            for(int i = 0; i< lists.Length; i++){
                if(lists[i] == null) continue;
                if(curr == null || lists[i].val < curr.val) {
                    //Console.WriteLine(lists[i].val);
                    curr = new ListNode(lists[i].val);
                    temp = i;
                }
                
            }
            if(curr == null) break;
            
            head.next =new ListNode(curr.val);
            head = head.next;
            if(temp != -1) lists[temp] = lists[temp].next;
        }
        return res.next.next;

    }
}

```


