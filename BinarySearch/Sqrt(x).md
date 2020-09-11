# Sqrt(x)

### 原题： https://leetcode.com/problems/sqrtx/

Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

Example 1:

Input: 4
Output: 2
Example 2:

Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
             
## 解
越界情况处理不了？？？？？
Your input
2147395599
Output
2147395598
Expected
46339

```c#
public class Solution {
    public int MySqrt(int x) {
        if(x <= 1) return x;
        
        int start = 1, end = x, mid;
        
        while(start + 1 < end){
            mid = start + (end - start)/2;
            
            if(mid*mid == x) return mid;
            if(mid*mid > x){
                end = mid;
            }
            else{
                start = mid;
            }
        }
        return start;
    }
}

```


