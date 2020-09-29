# partition-equal-subset-sum

### 原题： https://leetcode.com/problems/partition-equal-subset-sum/
Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

Note:

Each of the array element will not exceed 100.
The array size will not exceed 200.
 

Example 1:

Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
 

Example 2:

Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.


实际上是背包问题。看看能不能pick一些item使总重量为Sum的一半

```c#
public class Solution {
    public bool CanPartition(int[] nums) {
        if(nums == null || nums.Length == 0) return false;
        
        if(nums.Sum() % 2 == 1) return false;
        
        int W = nums.Sum() / 2;
        
        bool[,] dp = new bool[nums.Length + 1, W + 1];            //dp[i][j]=true if the sum jj can be formed by array elements in subset \text{nums[0]} .. \text{nums[i]}nums[0]..nums[i],otherwise false
        
        dp[0,0] = true;
        
        for(int i = 1; i <= nums.Length; i++){
            int curr = nums[i - 1];
            
            for(int j = 0; j <= W; j++){
                if(j < curr){
                    dp[i,j] = dp[i -1, j];
                }
                else{
                    dp[i,j] = dp[i-1,j] || dp[i - 1, j - curr];
                }
            }
        }
        
        return dp[nums.Length, W];
    }
}

```


