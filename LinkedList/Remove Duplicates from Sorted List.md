# Remove Duplicates from Sorted List

### 原题： https://leetcode.com/problems/remove-duplicates-from-sorted-list/

如果下一个元素与当前元素值相同就跳过

核心点在于：
1. while终止条件判断. **每个元素取用next前必须判断null**
2. 用dummy node返回head


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
    public ListNode DeleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(0,head);
        while(head != null && head.next != null){
            ListNode post = head.next;
            if(post.val == head.val){
                head.next = post.next;
            }
            else{
                head = head.next;
            }
        }
        return dummy.next;
    }
}

```