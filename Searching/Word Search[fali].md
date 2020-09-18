# Word Search

### 原题： https://leetcode.com/problems/word-search/

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


回溯题
**超时fail**

考虑动归?

```c#
public class Solution {
    int[][] directions = {new int[]{0,1}, new int[]{0,-1}, new int[]{1,0}, new int[]{-1,0}};
    
    public bool Exist(char[][] board, string word) {
        if(board == null || board.Length == 0 || board[0].Length == 0) return false;
        
        int[,] used = new int[board.Length, board[0].Length];
        
        for(int r = 0; r < board.Length; r++){
            for(int c = 0; c<board[0].Length; c++){
                if(Helper(board, word, r, c, used)) return true;
            }
        }
        return false;
        
    }
    
    
    private bool Helper(char[][] board, string word, int row, int col, int[,] used){

        if(row < 0 || row >= board.Length  || col < 0 || col >= board[0].Length || board[row][col] != word[0] || used[row, col] == 1) return false;
        
        if(word.Length == 1){
            if(board[row][col] == word[0]) return true;
            return false;
        } 

        bool res = false;
        used[row, col] = 1;
        foreach(var dir in directions){
            if(Helper(board, word.Substring(1), row + dir[0], col + dir[1], used)) res = true;
        }
        used[row, col] = 0;
        
        return res;
    }
}

```


