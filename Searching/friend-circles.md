# friend-circles

### 原题： https://leetcode.com/problems/friend-circles/

There are N students in a class. Some of them are friends, while some are not. Their friendship is transitive in nature. For example, if A is a direct friend of B, and B is a direct friend of C, then A is an indirect friend of C. And we defined a friend circle is a group of students who are direct or indirect friends.

Given a N*N matrix M representing the friend relationship between students in the class. If M[i][j] = 1, then the ith and jth students are direct friends with each other, otherwise not. And you have to output the total number of friend circles among all the students.

Example 1:

Input: 
[[1,1,0],
 [1,1,0],
 [0,0,1]]
Output: 2
Explanation:The 0th and 1st students are direct friends, so they are in a friend circle. 
The 2nd student himself is in a friend circle. So return 2.
 

Example 2:

Input: 
[[1,1,0],
 [1,1,1],
 [0,1,1]]
Output: 1
Explanation:The 0th and 1st students are direct friends, the 1st and 2nd students are direct friends, 
so the 0th and 2nd students are indirect friends. All of them are in the same friend circle, so return 1.

 

Constraints:

1 <= N <= 200
M[i][i] == 1
M[i][j] == M[j][i]


跟islands题不一样：
1001
0110
0111
1011
的结果应该是1.

直接用一个一维数组做标记，只记录这个人是否访问到。
到每一个人，在DFS中看他的朋友关系，将其朋友进行DFS。这样只要跟这个人有direct/indirect关系的人都会被标记。未标记的就是另一circle，主循环会再去DFS。

```c#
public class Solution {
    public int FindCircleNum(int[][] M) {
        if(M == null || M.Length == 0 || M[0].Length == 0) return 0;
        
        int res = 0;
        int[] visited = new int[M.Length];
        
        for(int i = 0; i < M.Length; i++){
            if(visited[i] == 0){
                DFS(M, i, visited);
                res++;
            }

        }
        return res;
    }
    
    private void DFS(int[][] M, int i, int[] visited){
        visited[i] = 1;
        for(int k = 0; k < M.Length; k++ ){
            if(visited[k] == 0 && M[i][k] == 1){
                DFS(M, k, visited);
            }
        }
        

    }
    
}

```


