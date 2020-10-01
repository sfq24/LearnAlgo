# Mlongest-palindromic-substring

### 原题： https://leetcode.com/problems/longest-palindromic-substring/
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

# 解
二维动规。 只要知道d[i,j] 是回文， 那么如果s[i-1] == s[j+1]，那么d[i-1, j+1]也是回文
要十分注意：
1. Substring(pos, len)
2. 循环顺序： 因为要先知道d[i,j]才能知道d[i-1, j+1]，所以要i从后向前运算

```c#
public class Solution {
    public string LongestPalindrome(string s) {
        if(s == null) return "";
        if(s.Length < 2) return s;
        
        string res = "";
        
        //dp[i,j] is True when s.Substring(i, j + 1 - i) is Palindrome
        bool[,] dp = new bool[s.Length, s.Length];
        
        for(int i = s.Length - 1; i >=0; i--){
            for(int j = i; j < s.Length; j++){
                dp[i,j] = (s[i] == s[j] && (j - i < 3 || dp[i + 1, j - 1]));         //包含了偶数相同的情况
                
                if(dp[i, j] && (j - i + 1) > res.Length){
                    res = s.Substring(i, j + 1 - i);
                }
            }
        }
        
        return res;
    }
            
}

```


