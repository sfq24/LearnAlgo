# surrounded-regions

### 原题： https://leetcode.com/problems/surrounded-regions/description/

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example:

X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
Explanation:

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

先用DFS处理边上区域，改为T，再把所有剩下的O改X，T改O


```c#
public class Solution {
    public void Solve(char[][] board) {
        if(board == null || board.Length == 0 || board[0].Length == 0) return;
        
        for(int i = 0; i < board[0].Length; i++){     //遍历最上最下两行的列
            DFS(board, 0, i);
            DFS(board, board.Length - 1, i);
        }
        
        for(int i = 0; i < board.Length; i++){        //遍历最左最右两列的行
            DFS(board, i, 0);
            DFS(board, i, board[0].Length -1);
        }
        //Console.WriteLine(board[board.Length -1][board[0].Length - 2]);
        
        for(int r = 0; r < board.Length ; r++){
            for(int c = 0; c < board[0].Length; c++){
                if(board[r][c] =='T'){
                    board[r][c] = 'O';
                }
                else if(board[r][c] =='O'){
                    board[r][c] = 'X';
                }
            }
        }
    }
    
    //相连的O全改成T
    private void DFS(char[][] board, int row, int col){                                   
        //if( row == board.Length && col ==board[0].Length - 2) Console.WriteLine("GO");
        if(row < 0 || row > board.Length - 1 || col < 0 || col > board[0].Length - 1 || board[row][col] != 'O') return;
        
        board[row][col] = 'T';
        
        DFS(board, row -1, col);
        DFS(board, row + 1, col);
        DFS(board, row, col + 1);
        DFS(board, row, col - 1);
    }
}

```


## fail 解： 待debug

全 O 阵fail

```c#
public class Solution {
    public void Solve(char[][] board) {
        if(board == null || board.Length == 0 || board[0].Length == 0) return;
        
        bool[,] seen = new bool[board.Length, board[0].Length];
        
        for(int r = 0; r < board.Length ; r++){
            for(int c = 0; c < board[0].Length; c++){
                if(board[r][c] == 'O' && DFS(board, r, c, seen)){
                    board[r][c] = 'X';
                }
            }
        }
    }
    
    private bool DFS(char[][] board, int row, int col, bool[,] seen){
        if(row < 0 || row > board.Length -1 || col < 0 || col > board[0].Length -1) return false;
        if(seen[row, col]) return true;
        
        seen[row, col] = true;
                
        if(board[row][col] == 'X'){
            return true;
        }
        else{
            return DFS(board, row, col - 1,seen) && DFS(board, row, col + 1, seen) && DFS(board, row - 1, col, seen) && DFS(board, row + 1, col,seen);
        }
        
        return true;
    }
}
```






