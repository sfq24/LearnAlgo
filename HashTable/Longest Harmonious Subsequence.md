#  Longest Harmonious Subsequence

### 原题： https://leetcode.com/problems/longest-harmonious-subsequence/

We define a harmounious array as an array where the difference between its maximum value and its minimum value is exactly 1.

Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.

Example 1:

Input: [1,3,2,2,5,2,3,7]
Output: 5
Explanation: The longest harmonious subsequence is [3,2,2,2,3].

超多种解法

考虑用HashTable解。
一种是先建立table，再循环一遍找num和nums + 1的和。
另一种是一边循环一边比。


## 解
循环两遍

```c# 
public class Solution {
    public int FindLHS(int[] nums) {
        Dictionary<int,int> dict = new Dictionary<int,int>();
        int res = 0;
        foreach(var num in nums){
            if(!dict.Keys.Contains(num)){
                dict.Add(num, 1);
            }
            else{
                dict[num] += 1;
            }
        }
        
        foreach(int num in dict.Keys){
            if(dict.Keys.Contains(num + 1)){
                res = Math.Max(res, dict[num] + dict[num + 1]);
            }
        }
        
        return res;
    }
}
```


