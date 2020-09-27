# arithmetic-slices

### 原题： https://leetcode.com/problems/arithmetic-slices/

A sequence of numbers is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequences:

1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
The following sequence is not arithmetic.

1, 1, 2, 5, 7
 
A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.

A slice (P, Q) of the array A is called arithmetic if the sequence:
A[P], A[P + 1], ..., A[Q - 1], A[Q] is arithmetic. In particular, this means that P + 1 < Q.

The function should return the number of arithmetic slices in the array A.

 
Example:

A = [1, 2, 3, 4]

return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.

# 解

当 A[i] - A[i-1] == A[i-1] - A[i-2]，那么 [A[i-2], A[i-1], A[i]] 构成一个等差递增子区间。而且在以 A[i-1] 为结尾的递增子区间的后面再加上一个 A[i]，一样可以构成新的递增子区间。

dp[2] = 1
[0, 1, 2]
dp[3] = dp[2] + 1 = 2
[0, 1, 2, 3], // [0, 1, 2] 之后加一个 3
[1, 2, 3]     // 新的递增子区间
dp[4] = dp[3] + 1 = 3
[0, 1, 2, 3, 4], // [0, 1, 2, 3] 之后加一个 4
[1, 2, 3, 4],    // [1, 2, 3] 之后加一个 4
[2, 3, 4]        // 新的递增子区间
综上，在 A[i] - A[i-1] == A[i-1] - A[i-2] 时，dp[i] = dp[i-1] + 1

最后求和

```c#
public class Solution {
    public int NumberOfArithmeticSlices(int[] A) {
        if(A == null || A.Length <3) return 0;
        
        int[] sum = new int[A.Length];
        
        for(int i = 2; i < A.Length; i++){
            if(A[i] - A[i - 1] == A[i - 1] - A[i - 2]){
                sum[i] = sum[i - 1] + 1;
            }
        }
        
        return sum.Sum();          //可以直接得到和
    }
}

```


