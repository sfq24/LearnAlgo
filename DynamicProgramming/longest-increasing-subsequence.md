# longest-increasing-subsequence

### 原题： https://leetcode.com/problems/longest-increasing-subsequence/

Given an unsorted array of integers, find the length of longest increasing subsequence.

Example:

Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
Note:

There may be more than one LIS combination, it is only necessary for you to return the length.
Your algorithm should run in O(n2) complexity.

# 解
注意到： 只要一个元素比之前所有元素都大，那么就一定让子序列长度加1.
dp[i] 表示i处最长子序列
所以让每个元素与之前的所有元素对比
最后返回dp中最大的值


```c#
public class Solution {
    public int LengthOfLIS(int[] nums) {
        if(nums == null || nums.Length == 0 ) return 0;
        
        int[] dp = new int[nums.Length];
        
        for(int i = 0; i < nums.Length; i++){
            int max = 1;
            for(int j = 0; j < i; j++){
                if(nums[i] > nums[j]){
                    max = Math.Max(max, dp[j] + 1);
                }
            }
            dp[i] = max;
        }
        
        return dp.Max();
    }
}

```


