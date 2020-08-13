# Remove Duplicates from Sorted Array

### 原题： https://leetcode.com/problems/remove-duplicates-from-sorted-array

依然考虑**双指针**，跳过重复元素。

核心点在于：
1. corner case 判断：
null，只有1个元素等
2. 终止条件
3. 返回值是否+1问题


## 解1
遇到重复元素，就把所有后面（直到最大元素之前）的元素前移. 退出条件为快指针遇到最大元素。
后来发现，快指针j永远比慢指针i快一步，所以直接用j-1代替i。
算法无法handle全相同array，所以需要作为corner case单独处理
mem usage < 98.87%
```c#
public class Solution {
    public int RemoveDuplicates(int[] nums) {
        if(nums == null || nums.Length == 0){
            return 0;
        }
        if(nums.Length == 1 || nums[0] == nums[nums.Length-1]){      //全相同array的处理
            return 1;
        }
        
        //int i = 0;
        int j = 1;
        
        while(nums[j] < nums[nums.Length-1]){            //本来定义了max存最大元素，之后直接用nums[nums.Length-1]
            if(nums[j] == nums[j-1]){
                for(int s = j; s < nums.Length-1; s++){
                    nums[s]=nums[s+1];
                }
            }
            else{
                //i++;
                j++;
            }
        }
        return j+1;
    }
}
```

### 另解 (更优）：
同remove elements。 快指针j相同就跳过，否则就慢进位更新

```c#
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }
    return i + 1;
}

```
