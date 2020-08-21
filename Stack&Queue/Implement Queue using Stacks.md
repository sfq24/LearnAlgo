# Implement Queue using Stacks

### 原题： https://leetcode.com/problems/implement-queue-using-stacks/

Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.
pop() -- Removes the element from in front of queue.
peek() -- Get the front element.
empty() -- Return whether the queue is empty.
Example:

MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false



## 解
容易想到2个stack来回倒换。但一定要画个图研究明白3个元素怎么处理。
一开始错误解是s1,s2分别做active，哪个不空就pop哪一个。然而不对。。。。。。

还是得倒腾两遍得到合适的queue。可以在push阶段操作，也可以在pop阶段

```c#
public class MyQueue {

    Stack<int> s1 = new Stack<int>();
    Stack<int> s2 = new Stack<int>();

    /** Initialize your data structure here. */
    public MyQueue() {
       
    }
    
    
    /** Push element x to the back of queue. */
    public void Push(int x) {
        while(s1.Count != 0){
            s2.Push(s1.Pop());
        }
        s2.Push(x);
        while(s2.Count != 0){
            s1.Push(s2.Pop());
        }
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int Pop() {
        return s1.Pop();
    }
    
    /** Get the front element. */
    public int Peek() {
        return s1.Peek();
    }
    
    /** Returns whether the queue is empty. */
    public bool Empty() {
        return s1.Count == 0 && s2.Count == 0;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.Push(x);
 * int param_2 = obj.Pop();
 * int param_3 = obj.Peek();
 * bool param_4 = obj.Empty();
 */

```
