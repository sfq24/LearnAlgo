# backpack

### 原题： https://www.lintcode.com/problem/backpack

在n个物品中挑选若干物品装入背包，最多能装多满？假设背包的大小为m，每个物品的大小为A[i]

你不可以将物品进行切割。

样例 1:
	输入:  [3,4,8,5], backpack size=10
	输出:  9

样例 2:
	输入:  [2,3,5,7], backpack size=12
	输出:  12

# 解 从底向上

状态bp[i][w]表示 表示将前i种物品装进限重为w的背包可以获得的最大价值

最后返回 dp[A.length][m]

```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        
        if(A == null || A.length == 0) return 0;
        
        int[][] dp = new int[A.length + 1][m+1];
        
        for(int i = 0; i < A.length; i++){
            for(int w = 0; w <= m; w++){
                if(w >= A[i]){
                    dp[i + 1][w] = Math.max(dp[i][w], dp[i][w - A[i]] + A[i]);
                }
                else{
                    dp[i + 1][w] = dp[i][w];
                }
            }
        }
        
        return dp[A.length][m];
    }
}

```



