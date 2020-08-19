# Remove Nth Node From End of List


### 原题： https://www.lintcode.com/problem/remove-nth-node-from-end-of-list/description

Given a linked list, remove the nth node from the end of list and return its head.

Example
Example 1:
	Input: list = 1->2->3->4->5->null， n = 2
	Output: 1->2->3->5->null


Example 2:
	Input:  list = 5->4->3->2->1->null, n = 2
	Output: 5->4->3->1->null
  
  
也用快慢指针来解决，快指针先行n步，两指针再同步向前进，知道快指针到达末尾，慢指针处在倒数第n个元素之前一个元素


核心点在于：
1. 快指针先向前n步。注意corner case，n正好为长度，这时候快指针到null处了，报错。所以单独判断第n步状况
2. python语法


## 解
```python
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param head: The first node of linked list.
    @param n: An integer
    @return: The head of linked list.
    """
    def removeNthFromEnd(self, head, n):
        
        if head == None or head.next == None:
            return None
        
        dummy = ListNode(0, head)
        pre = head
        for i in range(1,n):
            head = head.next
        #处理第n步special case
        if head.next == None:
            return dummy.next.next
        else:
            head = head.next
        
        while(head.next!=None):
            head = head.next
            pre = pre.next
        
        pre.next = pre.next.next
        
        return dummy.next

```
