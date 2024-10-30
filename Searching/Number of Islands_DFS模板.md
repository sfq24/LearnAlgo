# Number of Islands

### 原题： https://leetcode.com/problems/number-of-islands/

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.


Example 1:

Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
Example 2:

Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3


BFS典型题
**注意初始化多维数组**
看见一个island就计数，然后把这个island用递归函数抹去

```c#
public class Solution {
    public int NumIslands(char[][] grid) {
        if(grid == null || grid.Length == 0 || grid[0].Length == 0) return 0;
        
        int islands = 0;
        for(int r = 0; r < grid.Length; r++){
            for(int c = 0; c < grid[0].Length; c++){
                if(grid[r][c] == '1'){
                    islands++;
                    SeeIsland(grid, r, c);
                }
            }
        }
        
        return islands;
    }
    
    private void SeeIsland(char[][] grid, int row, int col){
        if(row < 0 || row > grid.Length - 1 || col < 0 || col > grid[0].Length - 1 || grid[row][col] == '0') return;
        
        grid[row][col] = '0';
        SeeIsland(grid, row - 1, col);
        SeeIsland(grid, row + 1, col);
        SeeIsland(grid, row, col - 1);
        SeeIsland(grid, row, col + 1);
    }
}

```

## 延伸题目解析

https://leetcode.cn/problems/number-of-islands/solutions/211211/dao-yu-lei-wen-ti-de-tong-yong-jie-fa-dfs-bian-li-
