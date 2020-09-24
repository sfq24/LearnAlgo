# range-sum-query-immutable

### 原题： https://leetcode.com/problems/range-sum-query-immutable/
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example:

Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
 

Constraints:

You may assume that the array does not change.
There are many calls to sumRange function.
0 <= nums.length <= 10^4
-10^5 <= nums[i] <= 10^5
0 <= i <= j < nums.length


注意 nums为null情况

```c#
public class NumArray {
    
    int[] nums = null;
    int[] sum = null;
    public NumArray(int[] nums) {
        if(nums == null || nums.Length ==0) return;
        nums = nums;
        sum = new int[nums.Length];
        sum[0] = nums[0];
        for(int i = 1; i< nums.Length; i++){
            sum[i] = sum[i - 1] + nums[i];
        }
    }
    
    public int SumRange(int i, int j) {
        if(i == 0) return sum[j];
        return sum[j] - sum[i -1];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.SumRange(i,j);
 */

```


