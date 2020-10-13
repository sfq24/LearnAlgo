# combination-sum-ii

### 原题： https://leetcode.com/problems/combination-sum-ii/

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
Example 1:

Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
Example 2:

Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]


应该可以用DP解

# 解：
DFS
注意理解如何去重：
**如果 i > pos 并且 can[i] = can[i-1]说明，以此数字开头的所有组合已经寻找过了，再找就是重复，所以要跳过**

```c#
public class Solution {
    public IList<IList<int>> CombinationSum2(int[] candidates, int target) {
        Array.Sort(candidates);
        List<IList<int>> res = new List<IList<int>>();
        SumHelper(candidates,res,new List<int>(),0,target);
        return res;
    }
    
    private void SumHelper(int[] candidates, List<IList<int>> res, List<int> list, int pos, int target){
        if(target < 0){
            return;
        }
        if(target == 0){
            res.Add(new List<int>(list));
            return;
        }
        for(int i = pos; i<candidates.Length; i++){
            if(i!=pos && candidates[i] == candidates[i-1]){
                continue;
            }
            list.Add(candidates[i]);
            SumHelper(candidates,res,list,i+1,target-candidates[i]);
            list.RemoveAt(list.Count-1);
        }
    }
}

```


