# permutations

### 原题： https://leetcode.com/problems/permutations/

Given a collection of distinct integers, return all possible permutations.

Example:

Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]

回溯法

```c#
public class Solution {
    public IList<IList<int>> Permute(int[] nums) {
        List<IList<int>> res = new List<IList<int>>();
        
        if(nums == null || nums.Length == 0) return res;
        Helper(nums, new List<int>(), res);
        return res;
    }
    
    private void Helper(int[] nums, List<int> temp, List<IList<int>> res){
        if(temp.Count == nums.Length){
            res.Add(new List<int>(temp));
            return;
        }
        
        for(int i=0; i< nums.Length; i++){
            if(!temp.Contains(nums[i])){
                temp.Add(nums[i]);
                Helper(nums, temp, res);
                temp.RemoveAt(temp.Count - 1);
            }

        }
    }
}
```


Permutation 2
https://leetcode.com/problems/permutations-ii/submissions/

注意：
With inputs as [1a, 1b, 2a],
If we don't handle the duplicates, the results would be: [1a, 1b, 2a], [1b, 1a, 2a]...,
so we must make sure 1a goes before 1b to avoid duplicates
By using nums[i-1]==nums[i] && !used[i-1], we can make sure that 1b cannot be choosed before 1a



```c#
public class Solution {
    public IList<IList<int>> PermuteUnique(int[] nums) {
        List<IList<int>> res = new List<IList<int>>();
        
        if(nums == null || nums.Length < 1) return res;
        
        Array.Sort(nums);     //必须有， [3,3,0,3]
        Helper(nums, new bool[nums.Length], new List<int>(), res);
        
        return res;
    }
    
    private void Helper(int[] nums, bool[] used, List<int> curr, List<IList<int>> res){
        if(curr.Count == nums.Length){
            res.Add(new List<int>(curr));
            return;
        }
        
        for(int i = 0; i < nums.Length; i++){
            if(used[i]) continue;
            if(i>0 && nums[i - 1] == nums[i] && !used[i-1]) continue;         //因为之前的重复元素一定已经算过了，所以不能重复算
            used[i] = true;
            curr.Add(nums[i]);
            Helper(nums, used, curr, res);
            used[i] = false;
            curr.RemoveAt(curr.Count - 1);
        }
    }
}
```


