# Valid Parentheses

### 原题： https://leetcode.com/problems/valid-parentheses/

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

## 解
自己多写几个corner case！！！
用stack实现配对

```c#
public class Solution {
    public bool IsValid(string s) {
        if(s == null || s == "") return true;
        
        Stack<char> stack = new Stack<char>();
        
        foreach(char ch in s){
            if(ch == '(' || ch == '{' || ch == '['){
                stack.Push(ch);
            }
            else{
                if(stack.Count == 0) return false;     //corner case
                if(ch ==')' && stack.Pop() != '(') return false;
                if(ch =='}' && stack.Pop() != '{') return false;
                if(ch ==']' && stack.Pop() != '[') return false;
            }
        }
        if(stack.Count > 0) return false;                      //corner case
        return true;
    }
}

```
