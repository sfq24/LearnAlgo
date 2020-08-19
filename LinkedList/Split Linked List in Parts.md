# Split Linked List in Parts

### 原题： https://leetcode.com/problems/split-linked-list-in-parts/

Given a (singly) linked list with head node root, write a function to split the linked list into k consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]
Example 1:
Input:
root = [1, 2, 3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The input and each element of the output are ListNodes, not arrays.
For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null.
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but it's string representation as a ListNode is [].
Example 2:
Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
Note:

The length of root will be in the range [0, 1000].
Each value of a node in the input will be an integer in the range [0, 999].
k will be an integer in the range [1, 50].


正常解就行。 先得到长度，再算width，再一个一个创建子list

核心点在于：
1. c# Stack类型用法
2. corner case


## 解  Stack

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
    public ListNode[] SplitListToParts(ListNode root, int k) {
        ListNode curr = root;
        int length = 0;
        while(curr!= null){
            curr = curr.next;
            length++;
        }
        //Console.WriteLine(length);
        
        int width = length / k;
        int remainder = length % k;
        
        curr = root;
        ListNode[] result = new ListNode[k];
        
        for(int i =0 ; i < k ; i ++){
            ListNode head = new ListNode(0);
            ListNode write = head;
            for(int j = 0; j < width + (i < remainder? 1 : 0); j ++){          //记住此处用法
                
                write.next = new ListNode(curr.val);
                write = write.next;
                curr = curr.next;
            }
            
            result[i] = head.next;
        }
        
        return result;
    }
}

```

## 解2：
不创建新的子list，而是在原有list中加null，分割加入results

略

