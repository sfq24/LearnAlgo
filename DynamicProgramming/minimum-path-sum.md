# minimum-path-sum

### 原题： https://leetcode.com/problems/minimum-path-sum/

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.


二维数组记录状态，向下推就好

```c#
public class Solution {
    public int MinPathSum(int[][] grid) {
        if(grid == null || grid.Length == 0) return 0;
        int[,] dp = new int[grid.Length, grid[0].Length];
        
        for(int r = 0; r < grid.Length; r++){
            for(int c = 0; c < grid[0].Length; c++){
                if(r == 0 && c == 0){
                    dp[r,c] = grid[r][c];
                }
                else if(r == 0){
                    dp[r,c] = dp[r,c-1] + grid[r][c];
                }
                else if(c == 0){
                    dp[r,c] = dp[r-1, c] + grid[r][c];
                }
                else{
                    dp[r,c] = Math.Min(dp[r - 1, c], dp[r, c - 1]) + grid[r][c];
                }
            }
        }
        
        return dp[grid.Length - 1, grid[0].Length - 1];
    }
}

```


