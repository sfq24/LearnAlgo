# Linked List

每个元素不只是存有val，还存有指向下一个元素的指针

## 分类
 * 单向 ： 指针指向下一个元素
 * 双向 ： 指向下一个元素和上一个元素

## 实现
```c#
public class LinkedList {
    public int val;
    public LinkedList next;

    public LinkedList(int val, LinkedList next){
        this.val = val;
        this.next = next;
    }
}
```

## 反转链表：
单向链表
链表的基本形式是：1 -> 2 -> 3 -> null，反转需要变为 3 -> 2 -> 1 -> null。这里要注意：

访问某个节点 curt.next 时，要检验 curt 是否为 null。
要把反转后的最后一个节点（即反转前的第一个节点）指向 null。

```c#
public class Solution {
    public LinkedList Reverse(LinkedList head) {
        LinkedList pre = null;
        while(head != null){
            LinkedList post = head.next;
            head.next = pre;
            pre = head;
            head = post;
        }
        reutrn pre;
    }
}

```

双向链表：
要点在于互换pre 和 post 指针

```c#
public class Solution {
    public DListNode reverse(DListNode head) {
        DListNode curr = null;
        while (head != null) {
            curr = head;
            head = curr.next;
            curr.next = curr.prev;
            curr.prev = head;
        }
        return curr;
}

```

## 解题一般方法
1. 先判断node是否为null，才能用node.next 
2. 快慢指针： 定义两个指针前进速度不一样。 比如找到LinkedList中间元素，让慢指针步长为1，快指针步长为2。或，判断LinkedList是否有环，可以看快指针能否追上慢指针。
3. Dummy Node：
建立一个dummy node指向head，以防需要修改（如删除）head导致信息丢失。 dummy.next = head
一般最后返回dummy.next
