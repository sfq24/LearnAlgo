# Find Minimum in Rotated Sorted Array


### 原题： https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  [0,1,2,4,5,6,7] might become  [4,5,6,7,0,1,2]).

Find the minimum element.

You may assume no duplicate exists in the array.

Example 1:

Input: [3,4,5,1,2] 
Output: 1
Example 2:

Input: [4,5,6,7,0,1,2]
Output: 0


最小值可能出现在两个位置： 中间不连续的断点，最开头。

## 解： 笨拙方法

```c#
public class Solution {
    public int FindMin(int[] nums) {
        if(nums == null || nums.Length == 0)  return -1;
        
        int start = 0, end = nums.Length -1, mid;
        int min = nums[0];
        while(start + 1 < end){
            mid = start + (end - start)/2;
            
            if(nums[start] < nums[mid]){
                min = nums[start] < min ? nums[start]:min;
                start = mid;
            }
            else{
                min = nums[mid] < min ? nums[mid]:min;
                end = mid;
            }
        }
        
        if(nums[start] < nums[end]){
            return nums[start] < min ? nums[start]:min;
        }
        return nums[end] < min ? nums[end]:min;
    }
}

```

## 解： 更优方法：
优先移动end

```c#
public class Solution {
    public int FindMin(int[] nums) {
        if(nums == null || nums.Length == 0)  return -1;
        
        int start = 0, end = nums.Length -1, mid;
        while(start + 1 < end){
            mid = start + (end - start)/2;
            
            if(nums[end] > nums[mid]){
                end = mid;
            }
            else{
                start = mid;
            }
        }
        
        if(nums[start] < nums[end]){
            return nums[start];
        }
        return nums[end];
    }
}

```

