# Next Greater Element II

### 原题： https://leetcode.com/problems/next-greater-element-ii

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

Example 1:
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.

**注意如何新建一个array，初始化所有元素为相同值**
**注意用一个循环循环两遍的技巧**


## 最优解：
倒向解：
  注意看solution相关动画
```c#
public class Solution {
    public int[] NextGreaterElements(int[] nums) {
        int length = nums.Length;
        int[] res = Enumerable.Repeat(-1, length).ToArray();
        Stack<int> stack = new Stack<int>();
        
        for(int i = 2 * length - 1; i >=0; i--){
            while(stack.Count != 0 && nums[i%length] >= nums[stack.Peek()]){
                stack.Pop();
            }
            res[i%length] = (stack.Count == 0) ? -1:nums[stack.Peek()];
            stack.Push(i%length);
        }
        
        return res;
    }
}
```


## 解
正向解：

非常类似于daily temperature。
运用stack解。
因为有loop循环两遍。关键点在于第二次的退出条件。

corner case：[5，4，3，2，1]

```c#
public class Solution {
    public int[] NextGreaterElements(int[] nums) {
        if(nums == null) return null;
        int length = nums.Length;
        int[] res = Enumerable.Repeat(-1,length).ToArray();
        int max = -1;
        
        Stack<int> stack = new Stack<int>();
        
        for(int i=0; i < length; i++){
            if(max < nums[i]) max = nums[i];
            while(stack.Count != 0 && nums[i] > nums[stack.Peek()]){
                int preIndex = stack.Pop();
                res[preIndex] = nums[i];
            }
            stack.Push(i);
        }

        for(int j = 0; j<length; j++){
            //Console.WriteLine(j + "  " + stack.Count);
            while(stack.Count != 0 && nums[j] > nums[stack.Peek()]){
                int preIndex = stack.Pop();
                res[preIndex] = nums[j];
                
            }
            if(nums[j] == max) return res;        //必须在while loop外面
            //不再向stack中加元素
        }
        return res;
    }
}


```
