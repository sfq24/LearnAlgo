# pacific-atlantic-water-flow

### 原题： https://leetcode.com/problems/pacific-atlantic-water-flow/

Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

Note:

The order of returned grid coordinates does not matter.
Both m and n are less than 150.
 

Example:

Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).

**题目意思不太对。 matrix中数字指的是浪高，看浪能不能流出边界到达两洋**

## 解
分别从四个边界DFS，两洋分别用matrix标记，如果看到比自己高的浪说明可以从此而来，进行DFS。递归终点会是浪高的点。
最后遍历一遍所有elem，两洋标记都为1说明符合要求。

```c#
public class Solution {
    int[][] directions = {new int[]{1,0}, new int[]{-1,0}, new int[]{0,1}, new int[]{0,-1}};
    
    public IList<IList<int>> PacificAtlantic(int[][] matrix) {
        List<IList<int>> res = new List<IList<int>>();
        if(matrix == null || matrix.Length == 0 || matrix[0].Length == 0) return res;
        int[,] pacific = new int[matrix.Length, matrix[0].Length];
        int[,] atlantic = new int[matrix.Length, matrix[0].Length];
        
        for(int i = 0; i < matrix.Length; i++){
            DFS(matrix, i, 0, pacific);
            DFS(matrix, i, matrix[0].Length - 1, atlantic);
        }
        
        for(int i = 0; i < matrix[0].Length; i++){
            DFS(matrix, 0, i, pacific);
            DFS(matrix, matrix.Length - 1, i, atlantic);
        }
        
        for(int i =0; i < matrix.Length; i++){
            for(int j=0; j < matrix[0].Length; j++){
                if(pacific[i,j] == 1 && atlantic[i,j] == 1){
                    res.Add((new int[]{i,j}).ToList());
                }
            }
        }
        
        return res;
    }
    
    private void DFS(int[][] matrix, int row, int col, int[,] ocean){
         if(ocean[row, col] == 1) return;
        
        ocean[row, col] = 1;
        
        foreach(var dir in directions){
            if(row + dir[0] < 0 || row + dir[0] >= matrix.Length || col + dir[1] < 0 || col + dir[1] >= matrix[0].Length) continue;
            if(matrix[row + dir[0]][col + dir[1]] >= matrix[row][col]){
                DFS(matrix, row + dir[0], col + dir[1], ocean);
            }
        }
    }
}

```


