# longest-common-subsequence

### 原题： https://leetcode.com/problems/longest-common-subsequence/
Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.

 

If there is no common subsequence, return 0.

 

Example 1:

Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
Example 2:

Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
Example 3:

Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
 

Constraints:

1 <= text1.length <= 1000
1 <= text2.length <= 1000
The input strings consist of lowercase English characters only.

# 解
用dp[i,j]表示前i个text1和前j个text2的common subseq。注意转移方程

```c#
public class Solution {
    public int LongestCommonSubsequence(string text1, string text2) {
        if(text1 == null || text2 == null || text1.Length ==0 || text2.Length == 0) return 0;
        
        int[,] dp = new int[text1.Length + 1, text2.Length + 1];
        
        for(int i = 0; i < text1.Length; i++){
            for(int j = 0; j < text2.Length; j++){
                if(text1[i] == text2[j]){
                    dp[i + 1, j+1] = dp[i, j] + 1;
                }
                else{
                    dp[i + 1,j + 1] = Math.Max(dp[i,j + 1], dp[i + 1,j]);
                }
            }
        }
        return dp[text1.Length, text2.Length];
        
    }
}

```


