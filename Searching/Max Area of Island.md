# Max Area of Island

### 原题： https://leetcode.com/problems/max-area-of-island/
Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

Example 1:

[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.
Example 2:

[[0,0,0,0,0,0,0,0]]
Given the above grid, return 0.
Note: The length of each dimension in the given grid does not exceed 50.


BFS典型题
**注意初始化多维数组**

```c#
public class Solution {
    public int MaxAreaOfIsland(int[][] grid) {
       
        if(grid == null || grid.Length == 0 || grid[0].Length == 0) return 0;
        int[,] seen = new int[grid.Length, grid[0].Length];
        int res = 0;
        
        for(int r=0; r < grid.Length; r++){
            for(int c=0; c<grid[0].Length; c++){
                res = Math.Max(res, Area(grid, r, c, seen));
            }
        }
        return res;
    }
    
    private int Area(int[][] grid, int row, int col, int[,] seen){
        int[][] directions = new int[][]{
            new int[]{1,0}, new int[]{0,1}, new int[]{0,-1}, new int[]{-1,0}
        };
        
        if(row < 0 || row > grid.Length - 1 || col < 0 || col > grid[0].Length-1 || seen[row,col] == 1 || grid[row][col] == 0){
            return 0;
        }
        int area = 1;
        seen[row,col] = 1;
        
        foreach(var dir in directions){
            area += Area(grid, row + dir[0], col + dir[1], seen);
        }
        
        return area;
    }
}

```


