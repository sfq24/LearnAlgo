# Subsets

### 原题： https://leetcode.com/problems/subsets/

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]


DFS典型题，模板背。
Java

```java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        Arrays.sort(nums);
        dfs(nums, 0, new ArrayList<Integer>(), results);
        return results;
    }
    
    // 1. 递归的定义
    // 以 subset 开头的，配上 nums 以 index 开始的数所有组合放到 results 里
    private void dfs(int[] nums,
                     int index,
                     List<Integer> subset,
                     List<List<Integer>> results) {
        // 3. 递归的出口
        if (index == nums.length) {
            results.add(new ArrayList<Integer>(subset));
            return;
        }
        
        // 2. 递归的拆解
        // (如何进入下一层)
        
        // 选了 nums[index]
        subset.add(nums[index]);
        dfs(nums, index + 1, subset, results);
        
        // 不选 nums[index]
        subset.remove(subset.size() - 1);
        dfs(nums, index + 1, subset, results);
    }
}
  
  ```

**DFS 模板**      针对有重复元素的subsets

```c#
 class Solution {
     public IList<IList<int>> subsetsWithDup(int[] nums) {
         IList<IList<int>> res = new List<IList<int>>();   //C# 中generic type不能implict，所以<>中必须还用IList
        
         dfs(res, new List<int>(), nums, 0);
         return res;
     }

     private void dfs(IList<IList<int>> res, List<int> temp, int [] nums, int start){
        /*此处判断是否拿到一个可行解*/
        res.Add(new List<int>(temp));           //注意此处语法，如果直接加temp,得到的是temp的ref，导致最后res所有元素都是temp最后状态
        //或者用ToList（）得到新list
        //res.add(temp.ToList());

        /*深度优先搜索*/
        for(int i = start; i < nums.length; i++){
            /*可行解的约束条件*/
            if(i > start && nums[i] == nums[i-1]) //含有重复元素的子集
                continue; 
            /*找到解的一部分元素，作为根元素*/
            temp.Add(nums[i]);
            /*添加枝叶*/
            dfs(list, temp, nums, i + 1);
            /*枝叶出栈时需要的操作，必有的是退出枝叶*/
            temp.RemoveAt(temp.size() - 1);           //用RemoveAt准确删除最后一个元素
        }
    } 
}
```

# 解

## Java
1. List的初始化和传导
2. add，remove
3. list.add(new ArrayList<>(tempList));

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}

private void backtrack(List<List<Integer>> list , List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
    for(int i = start; i < nums.length; i++){
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```


注意C# 语法，初始化array of arrays

```c#
public class Solution {
    public IList<IList<int>> Subsets(int[] nums) {
       
        IList<IList<int>> res = new List<IList<int>>();
        if(nums == null || nums.Length == 0) return res;
        
        dfs(nums, 0, new List<int>(), res);
        
        return res;
    }
    
    public void dfs(int[] nums, int index, List<int> path, IList<IList<int>> res){
        res.Add(path.ToList());
       
        for(int i = index; i<nums.Length; i++){
            path.Add(nums[i]);
            
            dfs(nums, i + 1, path, res);
            path.RemoveAt(path.Count-1);
        }
    }
    
    
}

```


