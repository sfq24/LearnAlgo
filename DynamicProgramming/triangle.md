# triangle

### 原题： https://leetcode.com/problems/triangle

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

动规典型题
多种做法

# 解 从底向上

最原始想法：直接利用triangle本身，因为算完一层后面的数就不需要了，所以不怕更改
从倒数第二层向上算从下往上到节点的minSum

最后返回[0][0]

```c#
public class Solution {
    public int MinimumTotal(IList<IList<int>> triangle) {
        int rows = triangle.Count;
        if (rows == 0)
            return 0;
        int index = rows - 2;
        while (index >= 0) {
            for (int k = 0; k < index + 1; k++)
                triangle[index][k] += Math.Min(triangle[index+1][k], triangle[index+1][k+1]);
            index--;
        }
        return triangle[0][0];
    }
}
```
改进：用一个一维数组，长度为可能的最大长度triangle.Count， 一行一行向前递进，每个元素需要下面一行的结果，已经知道了，满足DP条件
```c#
public class Solution {
    public int MinimumTotal(IList<IList<int>> triangle) {
        int[] f = new int[triangle.Count];
        
        for(int i = 0; i < triangle.Count; i++){
            f[i] = triangle[triangle.Count - 1][i];
        }
        
        for(int r = triangle.Count - 2; r >= 0; r--){
            for(int c = 0; c <= r; c++){
                f[c] = Math.Min(f[c], f[c + 1]) + triangle[r][c];
            }
        }
        
        return f[0];
    }
}
```

Python 版本： 
https://leetcode.com/problems/triangle/discuss/38735/Python-easy-to-understand-solutions-(top-down-bottom-up).


