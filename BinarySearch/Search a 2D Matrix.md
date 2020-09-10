# Search a 2D Matrix


### 原题： https://leetcode.com/problems/search-a-2d-matrix/

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
Example 1:

Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
Example 2:

Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false

## 矩阵
matrix.Length 返回的是row，再用matrix[0].Length 得到 column。 
总长度row * column

遍历的时候需要用 matrix[mid/column][mid%column]

多处理几种边界情况：row = 0， column = 0. 未进入循环就退出（一共2元素）等


```c#
public class Solution {
    public bool SearchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.Length == 0) return false;

        int row = matrix.Length;
        int column = matrix[0].Length;
        if(column == 0) return false;
        int start = 0;
        int end = row * column -1;
        int mid;
        while(start + 1 < end){
            mid = start + (end - start)/2;
            
            if(matrix[mid/column][mid%column] < target){
                start = mid;
            }
            else{
                end = mid;
            }
        }
        
        if(matrix[end/column][end%column] == target || matrix[start/column][start%column] == target){
            return true;
        }
        
        return false;
    }
}

```


