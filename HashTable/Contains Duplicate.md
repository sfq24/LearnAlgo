# Contains Duplicate

### 原题： https://leetcode.com/problems/path-sum/

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

Example 1:

Input: [1,2,3,1]
Output: true
Example 2:

Input: [1,2,3,4]
Output: false
Example 3:

Input: [1,1,1,3,3,4,3,2,4,2]
Output: true

暴力解肯定不行
最差也得先sort一遍在循环一遍比相邻元素

需要用hashset
可以先装逼用个Linq

```c# 
public class Solution {
    public bool ContainsDuplicate(int[] nums) {
        HashSet<int> set = new HashSet<int>();
        
        foreach(int i in nums){
            if(set.Contains(i)) return true;
            set.Add(i);
        }
        return false;
    }
}
```

直接用Linq。。。。。。。演示完了正常解
```c#  

public class Solution {
    public bool ContainsDuplicate(int[] nums) {
        return nums.Length != nums.Distinct().Count();
        //return nums.Length != nums.Distinct().ToArray().Length;
    }
}

```

