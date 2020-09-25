# integer-break

### 原题： https://leetcode.com/problems/integer-break/
Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

Example 1:

Input: 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
Example 2:

Input: 10
Output: 36
Explanation: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36.
Note: You may assume that n is not less than 2 and not larger than 58.

# 解：

dp数组表示最大积，
let's say i = 8, we are trying to fill dp[8]:if 8 can only be broken into 2 parts, the answer could be among 1 * 7, 2 * 6, 3 * 5, 4 * 4... 
but these numbers can be further broken. so we have to compare 1 with dp[1], 7 with dp[7], 2 with dp[2], 6 with dp[6]...etc

所以需要比较，当前最大，差分两项，拆出int×另一部分最大

```c#
public class Solution {
    public int IntegerBreak(int n) {
        int[] dp = new int[n + 1];
        
        dp[1] = 1;
        
        for(int i = 2; i <=n; i++){
            for(int j = 1; j < i; j++){
                dp[i] = Math.Max(dp[i], Math.Max(j * (i -j), j * dp[i - j]));
            }
        }
        
        return dp[n];
    }
}

```


