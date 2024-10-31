# Shortest Path in Binary Matrix


### 原题： https://leetcode.com/problems/shortest-path-in-binary-matrix/

In an N by N square grid, each cell is either empty (0) or blocked (1).

A clear path from top-left to bottom-right has length k if and only if it is composed of cells C_1, C_2, ..., C_k such that:

Adjacent cells C_i and C_{i+1} are connected 8-directionally (ie., they are different and share an edge or corner)
C_1 is at location (0, 0) (ie. has value grid[0][0])
C_k is at location (N-1, N-1) (ie. has value grid[N-1][N-1])
If C_i is located at (r, c), then grid[r][c] is empty (ie. grid[r][c] == 0).
Return the length of the shortest such clear path from top-left to bottom-right.  If such a path does not exist, return -1.

 

Example 1:

Input: [[0,1],[1,0]]


Output: 2

Example 2:

Input: [[0,0,0],[1,1,0],[1,1,0]]


Output: 4

 

Note:

1 <= grid.length == grid[0].length <= 100
grid[r][c] is 0 or 1


BFS模版：
```java
class Solution {

    private static int[][] directions = {{0,1}, {0, -1}, {1, -1}, {1, 0}, {1, 1}, {-1, -1}, {-1, 0}, {-1, 1}};
    public int shortestPathBinaryMatrix(int[][] grid) {
        if (grid[0][0] == 1) return -1;

        Queue<int[]> queue = new LinkedList<>();

        int distance = 0;

        queue.add(new int[]{0,0});

        while (!queue.isEmpty()){ // 求最短路径 使用BFS
            int size = queue.size();

            distance++;

            while (size-- > 0) {
                int[] pos = queue.remove();

                int row = pos[0], col = pos[1];

                if (grid[row][col] == 1 || grid[row][col] == 2) {
                    continue;
                }

                grid[row][col] = 2;         //标记走过

                if (row == grid.length - 1 && col == grid[0].length - 1) {
                    return distance;
                }

                for (int i = 0; i < 8; i++){
                    int newX = pos[0] + directions[i][0];
                    int newY = pos[1] + directions[i][1];
                    if (0 <= newX && newX < grid.length && 0 <= newY && newY < grid[0].length && grid[newX][newY] == 0){
                        queue.add(new int[]{newX, newY});
                    }
                }
            }
            
        }
        return -1; // 如果最后终点的值还是0，说明没有到达
    }
}
```




BFS典型题，需要一步一步向后推。
注意C# 语法，初始化array of arrays


# 解 动规

```c#
public class Solution {
    public int NumSquares(int n) {
        if(n == 0) return 0;
        int[] dp = new int[n+1];
        
        dp[0] = 0;
        for(int i  = 1; i <= n; i++){
            dp[i] = int.MaxValue;
            for(int j = 1; j <= n; j++){
                if(j*j <= i){
                    dp[i] = Math.Min(dp[i], 1 + dp[i - j*j]);
                }
            }
        }
        
        return dp[n];
    }
}

```



# 解 BFS
优化：考虑倒着往queue里放元素？



```c#
public class Solution {
    public int ShortestPathBinaryMatrix(int[][] grid) {
        if(grid == null || grid.Length == 0 || grid[0].Length == 0) return -1;
        
        Queue<KeyValuePair<int,int>> queue = new Queue<KeyValuePair<int,int>>();
        
        queue.Enqueue(new KeyValuePair<int,int>(0,0));      //queue存坐标
        
        int[][] directions = {new int[]{1,1}, new int[]{1,0}, new int[]{-1,-1}, new int[]{-1,0}, new int[]{0,1}, new int[]{0,-1}, new int[]{1,-1}, new int[]{-1,1}};
        int pathLength = 0;
        
        while(queue.Count > 0){
            int queueSize = queue.Count;
            
            pathLength++;             //新的一层，pathLength + 1
            while(queueSize-- > 0){        //在层内遍历
                var pair = queue.Dequeue();
                int row = pair.Key, col = pair.Value;
                
                if(grid[row][col] == 1) continue;
                
                grid[row][col] = 1;    //标记走过
              
                if(row == grid.Length -1 && col == grid.Length - 1) return pathLength;      //终止条件
            
                foreach(var dir in directions){
                    int nrow = row + dir[0];           //需要用新var
                    int ncol = col + dir[1];
                    if(nrow < 0 || nrow > grid.Length -1 || ncol < 0 || ncol > grid.Length - 1) continue;
                
                    queue.Enqueue(new KeyValuePair<int,int>(nrow, ncol));
                }
            }
            
            
        }
        
        return -1;
    }
}

```


