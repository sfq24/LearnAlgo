# Search in Rotated Sorted Array

### 原题： https://leetcode.com/problems/search-in-rotated-sorted-array/

You are given an integer array nums sorted in ascending order, and an integer target.

Suppose that nums is rotated at some pivot unknown to you beforehand (i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

If target is found in the array return its index, otherwise, return -1.

 

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
Example 3:

Input: nums = [1], target = 0
Output: -1
 

Constraints:

1 <= nums.length <= 5000
-10^4 <= nums[i] <= 10^4
All values of nums are unique.
nums is guranteed to be rotated at some pivot.
-10^4 <= target <= 10^4

start，mid，end把数列分两半，必定有一半有序。target在有序区间的判断条件是 start《 target 《 mid， 或者 mid 《 target 《 end。
据此二分。
另外判断需要改成 >=, <=，否则在开头和结尾的target会被漏掉


```c# 
public class Solution {
    public int Search(int[] nums, int target) {
        if(nums == null || nums.Length == 0) return -1;
        
        int start = 0, end = nums.Length -1, mid;
        
        while(start + 1 < end){
            mid = start + (end - start)/2;
            
            if(nums[start] < nums[mid]){        //start to mid sorted
                if(nums[start] <= target && nums[mid] >= target){
                    end = mid;
                }
                else{
                    start = mid;
                }
            }
            else{                               //mid to end sorted
                if(nums[mid] <= target && nums[end] >= target){
                    start = mid;
                }
                else{
                    end = mid;
                }
            }
        }
        
        if(nums[start] == target) return start;
        if(nums[end] == target) return end;
        
        return -1;
    }
}
```


