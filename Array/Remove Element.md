# Remove Element

### 原题： https://leetcode.com/problems/remove-element

最关键的是理解in place。 即使是达到题目要求，实际nums.Length还是跟原来一样。所以题目强调： It doesn't matter what you leave beyond the new length.
所以只需要把nums中与val相同的跳过就好。
所以考虑用**双指针**：一个指针iterate原数列index，另一个为目标数列index。快指针只要遇到与val相同的elm就跳过

## 解
```c#
public class Solution {
    public int RemoveElement(int[] nums, int val) {
        if(nums.Length == 0 || val == null){
            return 0;
        }
        int m = 0;
        for(int i =0; i<nums.Length; i++){
            if(nums[i] != val){
                nums[m] = nums[i];
                m++;
            }
        }
        Console.WriteLine(nums.Length);
        return m;
    }
}
```

### 另解：
慢指针从后向前，每次从前向后指针遇到val，就与慢指针的值交换，慢指针向前移动。
注意慢指针代表的是个数，作为index要-1; 也要注意终止条件

```c#
public class Solution {
    public int RemoveElement(int[] nums, int val) {
        if(nums == null || nums.Length == 0){
            return 0;
        }
        int i = 0;
        int n = nums.Length;
        
        while(i<n){
            if(nums[i] == val){
                nums[i]=nums[n-1];
                n--;
            }
            else{
                i++;
            }
        }
        return n;
    }
}

```