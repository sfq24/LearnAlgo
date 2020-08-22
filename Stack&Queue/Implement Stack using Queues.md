# Implement Stack using Queues

### 原题： https://leetcode.com/problems/implement-stack-using-queues/

Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.
Example:

MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false


两个queue倒换

**注意c#中queue的语法**

## 解
下为Push O（1），Pop O(n)解法。 若要反之，就先在非active queue上enqueue，再把active queue的元素倒换过来。

```c#
public class MyStack {

    /** Initialize your data structure here. */
    public MyStack() {
        
    }
    Queue<int> queue1 = new Queue<int>();
    Queue<int> queue2 = new Queue<int>();
    bool q1Active = true;
    /** Push element x onto stack. */
    public void Push(int x) {
        if(q1Active){
            queue1.Enqueue(x);
        }
        else{
            queue2.Enqueue(x);
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int Pop() {
        if(q1Active){
            while(queue1.Count > 1){
                queue2.Enqueue(queue1.Dequeue());
            }
            q1Active = false;
            return queue1.Dequeue();
        }
        else{
            while(queue2.Count > 1){
                queue1.Enqueue(queue2.Dequeue());
            }
            q1Active = true;
            return queue2.Dequeue();
        }
    }
    
    /** Get the top element. */
    public int Top() {
        int top;
        if(q1Active){
            while(queue1.Count > 1){
                queue2.Enqueue(queue1.Dequeue());
            }
            q1Active = false;
            top = queue1.Dequeue();
            queue2.Enqueue(top);
            return top;
        }
        else{
            while(queue2.Count > 1){
                queue1.Enqueue(queue2.Dequeue());
            }
            q1Active = false;
            top = queue2.Dequeue();
            queue1.Enqueue(top);
            return top;
        }
    }
    
    /** Returns whether the stack is empty. */
    public bool Empty() {
        return queue1.Count == 0 && queue2.Count == 0;
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.Push(x);
 * int param_2 = obj.Pop();
 * int param_3 = obj.Top();
 * bool param_4 = obj.Empty();
 */

```
