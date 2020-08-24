# Daily Temperatures

### 原题： https://leetcode.com/problems/daily-temperatures/

Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures T = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0].

Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100].


暴力解法略

用stack实现巧妙解法：
让Stack存严格递减的index，直到遇到比index最顶元素大的index，再一个一个与stack中元素比较，只要比stack元素大，就算dist=current index - stack.Pop(), 加入到result 数组中。
尚未遇到比自己大的元素，会在result数组中保持为0，随着temp遍历，知道遇到比自己大的元素再更新。

Stack中相当于存着尚未发现比自己的大的元素的index，等待着跟随temp遍历，直到找到比自己大的元素再更新results

## 解


```c#
public class Solution {
    public int[] DailyTemperatures(int[] T) {
        int length = T.Length;
        int[] res = new int[length];  //init to all be 0！！！
        
        Stack<int> stack = new Stack<int>();
        
        for(int i = 0; i < length; i++){
            while(stack.Count != 0 && T[i] > T[stack.Peek()]){
                int preIndex = stack.Pop();
                res[preIndex] = i - preIndex;
            }
            stack.Push(i);
                
        }
        return res;
    }
}


```
