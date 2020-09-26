# decode-ways

### 原题： https://leetcode.com/problems/decode-ways
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.

Example 1:

Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
Example 2:

Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).


注意一大堆corner case
采用以下做法可以简单涵盖所以cases

```c#
public class Solution {
    public int NumDecodings(string s) {
        if(s == null || s.Length == 0 || s[0]=='0') return 0;
        int[] dp = new int[s.Length + 1];
        
        dp[0] = 1;
        dp[1] = s[0] == '0' ? 0 : 1;
        for(int i = 2; i <= s.Length; i++){
            if(s[i - 1] - '0' >=1 && s[i - 1] - '0' <=9){
                dp[i] = dp[i - 1];
            }
            
            if(((s[i-2] - '0') * 10 + (s[i -1] - '0') <= 26) && ((s[i-2] - '0') * 10 + (s[i -1] - '0') >= 10)){
                dp[i] += dp[i - 2];
            }
        }
        
        return dp[s.Length];
    }
}

```


