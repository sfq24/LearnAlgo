# Combinations

### 原题： https://leetcode.com/problems/combinations/

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

You may return the answer in any order.

Example 1:

Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
Example 2:

Input: n = 1, k = 1
Output: [[1]]
 

Constraints:

1 <= n <= 20
1 <= k <= n

最tricky的地方见注释

```c#
public class Solution {
    public IList<IList<int>> Combine(int n, int k) {
        List<IList<int>> res = new List<IList<int>>();
        
        Helper(k, n, 1, new List<int>(), res);
        
        return res;
    }
    
    private void Helper(int k, int n, int curr, List<int> comb, List<IList<int>> res){
        if(comb.Count == k){
            res.Add(new List<int>(comb));
            return;
        }
        
        for(int i = curr; i <=n; i++){
            if(comb.Contains(i)){
                continue;
            }
            
            comb.Add(i);
            Helper(k, n, i + 1, comb, res);           //迭代的是i+1，不是curr + 1
            comb.RemoveAt(comb.Count - 1);
        }
    }
}

```


