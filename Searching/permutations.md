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


